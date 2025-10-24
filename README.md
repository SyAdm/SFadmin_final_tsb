# 🖥️ Репозиторий итогового проекта — Системный администратор на Linux

## 📌 Описание
Данный репозиторий содержит роли и плейбуки Ansible, а также документацию по итоговой аттестации курса **SkillFactory "Системный администратор Linux"**.  
Проект состоит из трёх частей:  
1. Развёртывание серверов.  
2. Настройка сервисов.  
3. Финал: Docker + CMS-визитка.  

---

## ✅ Часть 1 — Развёртывание серверов
- [x] Создать 3 ВМ на Ubuntu.  
- [x] Настроить SSH-ключи для доступа.  
- [x] Создать Ansible inventory (`hosts.ini`).  

**Сервер 1 (базовый):**  
- [x] [Zabbix-server](https://github.com/SyAdm/SFadmin_final_tsb/blob/main/part_1/server_1/Zabbix-server.md)  
- [x] Grafana  
- [x] Ansible  
- [x] Filebeat  
- [x] OpenVPN-server (TCP)  
- [x] Клонировать GitHub-репозиторий  

**Сервер 2:**  
- [ ] nginx  
- [ ] Apache  
- [ ] PHP  
- [ ] Zabbix-agent  
- [ ] bind (DNS)  
- [ ] Почтовый сервер (Postfix/Exim)  
- [ ] filebeat  

**Сервер 3:**  
- [ ] PostgreSQL 12  
- [ ] Zabbix-agent  
- [ ] ELK (Elasticsearch, Logstash, Kibana)  

**Общее:**  
- [ ] Настроить OpenVPN-клиенты на сервере 2 и 3  
- [ ] Все роли вынести в GitHub  
- [ ] README с пометкой, что установлено вручную  
- [ ] Проверить доступ извне: Zabbix, Grafana, Kibana, nginx  

---

## ✅ Часть 2 — Настройка сервисов
- [ ] Настроить локальное время (chrony/ntp)  
- [ ] Zabbix мониторит все сервера (Linux template)  
- [ ] Zabbix мониторит PostgreSQL  
- [ ] Zabbix мониторит ELK  
- [ ] Зарегистрировать бесплатный домен  
- [ ] Настроить bind (DNS-сервер)  
- [ ] Прописать A/NS/MX-записи  
- [ ] Проверить резолвинг серверов по именам  
- [ ] Filebeat отправляет логи nginx/apache → ELK  
- [ ] Проверить логи в Kibana  
- [ ] Настроить почту (Postfix)  
- [ ] Проверить отправку писем наружу  
- [ ] Убедиться, что сервер не open relay  
- [ ] Загрузить БД авиаперелётов в PostgreSQL  
- [ ] Установить pgAdmin (доступ только по VPN)  
- [ ] Настроить nginx как reverse proxy для 2 сайтов  
  - [ ] Сайт заказчика (форма обратной связи + SSL, порт 443)  
  - [ ] Второй сайт (CMS или статический контент)  
- [ ] Создать Grafana dashboard: CPU, RAM, Disk usage всех хостов  

---

## ✅ Часть 3 — Финал + Docker + Визитка
- [ ] Перенести Zabbix-server в Docker  
- [ ] Перенести Grafana в Docker  
- [ ] Перенести ELK в Docker  
- [ ] Поднять CMS (WordPress или другая) на nginx  
- [ ] Создать сайт-визитку: о себе + описание проекта  
- [ ] Настроить форму обратной связи (через Postfix)  
- [ ] Создать копию БД `dbname_fortests` в PostgreSQL  
  - [ ] Очистить таблицы `boarding_passes` и `bookings`  
- [ ] Дать доступ ментору в pgAdmin  
- [ ] Проверить, что filebeat и zabbix-agent работают  
- [ ] Сделать скриншоты контейнеров (Zabbix, Grafana, ELK)  
- [ ] Проверить доступность всех сервисов по доменам:  
  - [ ] `zabbix.mydomain.com`  
  - [ ] `grafana.mydomain.com`  
  - [ ] `kibana.mydomain.com`  
  - [ ] `resume.mydomain.com` (CMS-визитка)  

---

## 🛠️ Используемые технологии
- **Ansible** (автоматизация)  
- **Zabbix** (мониторинг)  
- **Grafana** (визуализация)  
- **ELK (Elasticsearch, Logstash, Kibana)** (логи)  
- **Filebeat** (сбор логов)  
- **PostgreSQL + pgAdmin** (БД и управление)  
- **nginx / Apache / PHP** (веб-серверы)  
- **OpenVPN** (VPN-доступ)  
- **Bind** (DNS)  
- **Postfix** (почтовый сервер)  
- **Docker** (контейнеризация сервисов)  
- **Certbot** (SSL-сертификаты)  

---

## 📂 Структура репозитория

ansible-infra/
├── roles/ # Ansible роли
├── playbooks/ # Плейбуки
├── hosts.ini # Inventory
├── site.yml # Общий запуск
├── README.md # Документация
