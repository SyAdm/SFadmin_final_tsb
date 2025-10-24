## Zabbix-server

### Общая информация

На [оф. сайте](https://www.zabbix.com/ru/download?zabbix=7.4&os_distribution=ubuntu&os_version=22.04&components=server_frontend_agent&db=mysql&ws=apache) есть конфигуратор для выбора платформы.
Для своего проекта я выбрал следующую конфигурацию:

1. Версия Zabbix = 7.4 (самая актуальная на момент написания статьи)
2. Дистрибутив ОС = Ubuntu
3. Версия ОС = 22.04 Jammy (amd64, arm64)
4. Компоненты заббикс - Server, Frontend, Agent
5. База данных = PostgreSQL
6. Веб-сервер = Apache

<img width="1134" height="494" alt="image" src="https://github.com/user-attachments/assets/b1a62a0d-f540-489c-bd32-d3d813761325" />


### Подготовка и установка

1. Требуется установленная СУБД - [PostgreSQL](https://www.postgresql.org/download/linux/ubuntu/)
2. Далее переходим к установке Zabbix сервера

Далее переходим к установке и конфигурированию Zabbix сервера:

a. Заходим под root-ом
Start new shell session with root privileges.
```
sudo -s
```
b. Установите репозиторий Zabbix
```
wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu22.04_all.deb
dpkg -i zabbix-release_latest_7.4+ubuntu22.04_all.deb
apt update
```
c. Установите Zabbix сервер, веб-интерфейс и агент
```
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
d. Создайте базу данных

Установите и запустите сервер базы данных.
Ссылка на оф сайт: https://www.postgresql.org/download/linux/ubuntu/
Выполните следующие комманды на хосте, где будет распологаться база данных.
```
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
```
На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.
```
zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```
e. Настройте базу данных для Zabbix сервера
Отредактируйте файл /etc/zabbix/zabbix_server.conf
```
DBPassword=password (пароль от пользователя postgresql который имеет доступ к базе zabbix)
```
f. Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.
```
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```
g. Open Zabbix UI web page
The default URL for Zabbix UI when using Apache web server is http://host/zabbix

Готово!

<img width="1920" height="992" alt="image" src="https://github.com/user-attachments/assets/1880b3ac-4c0b-49d8-b12d-0698029095b4" />
<img width="1920" height="992" alt="image" src="https://github.com/user-attachments/assets/a317606c-b568-46b8-a1c3-4dc0fdcf45f3" />
