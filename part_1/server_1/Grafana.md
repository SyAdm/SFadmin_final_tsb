# Grafana

## Общая информация

Далее по нашему ТЗ, требуется Grafana - красивая визуализация наших метрик, которые мы будем получать от разных источников, но, на данном этапе это Zabbix.
Есть один нюанс, по умолчанию Grafana использует базу данных SQLite, для малого бизнеса и нагрузи, этого достаточно.
Но, для своего проекта я решил сделать PostgreSQL, учитывая что СУБД у нас уже установлена, настроена и работает в данный момент для Zabbix сервера!

Конфигурация получилась такой:
1. Grafan v.12.2.1 *(редакция OOS, Enterprise мы не потянем)*
2. PostgreSQL v.14.19

## Подготовка и установка

1. Требуется установленная СУБД - [PostgreSQL](https://www.postgresql.org/download/linux/ubuntu/)
2. Создать базу данных и пользователя для Grafan-ы. 
3. Далее переходим к установке Grafana сервера

### Создать базу данных и пользователя для Grafan-ы

Подключаемся к psql:
```
psql -h 127.0.0.1 -U postgres -d postgres
```

Создаем пользователя, я назвал его grafana_user:
```
CREATE USER grafana_user WITH LOGIN NOSUPERUSER INHERIT NOCREATEDB NOCREATEROLE NOREPLICATION;
```

Задаем нужный нам пароль для нашего свежеипеченного пользователя:
```
ALTER ROLE grafana_user WITH PASSWORD '<GRAFANA_USER_PASSWORD>';
```

Осталось создать базу:

```
CREATE DATABASE grafana WITH OWNER = grafana_user ENCODING = 'UTF8' LC_COLLATE = 'en_US.UTF-8' LC_CTYPE = 'en_US.UTF-8' TABLESPACE = pg_default CONNECTION LIMIT = -1;
```

Если при создании базы выдаст ошибку вида:
***
	ERROR:  new collation (en_US.UTF-8) is incompatible with the collation of the template database (C.UTF-8)
	HINT:  Use the same collation as in the template database, or use template0 as template.
***
То ты просто создаёшь базу с локалью LC_COLLATE = 'en_US.UTF-8' но шаблонная база (template1), на основе которой PostgreSQL создаёт новые базы, использует другую локаль — C.UTF-8.
PostgreSQL запрещает смешивать разные локали между базой-источником (template1) и создаваемой, потому что это может нарушить сортировку и сравнение строк.
Решение, создать базу с указанием TEMPLATE template0 — это “чистая” база без предустановленных локалей!
	
Рабочая строчка создания базы будет такой:
```
CREATE DATABASE grafana WITH OWNER = grafana_user ENCODING = 'UTF8' LC_COLLATE = 'en_US.UTF-8' LC_CTYPE = 'en_US.UTF-8' TEMPLATE template0 TABLESPACE = pg_default CONNECTION LIMIT = -1;
```

### Далее переходим к установке и конфигурированию сервера Grafana

Чтобы установить Grafana из репозитория APT, выполните следующие шаги:

1. Установим необходимые пакеты
```
sudo apt-get install -y apt-transport-https software-properties-common wget
```
2. Импортируем ключ GPG:
```
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

3. Чтобы добавить репозиторий для стабильных версий, выполните следующую команду:
```
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

4. Выполните следующую команду для обновления списка доступных пакетов:
```
sudo apt-get update
```

5. Чтобы установить Grafana OSS, выполните следующую команду:
```
sudo apt-get install grafana
```
