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
- [x] [Grafana](https://github.com/SyAdm/SFadmin_final_tsb/blob/main/part_1/server_1/Grafana.md)  
- [x] [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#pipx-install)
- [x] [Filebeat](https://www.elastic.co/docs/reference/beats/filebeat/filebeat-installation-configuration) (Step 1)
- [x] [OpenVPN-server (TCP)](https://www.cyberciti.biz/faq/howto-setup-openvpn-server-on-ubuntu-linux-14-04-or-16-04-lts/)  
- [x] Клонировать GitHub-репозиторий

**Сервер 2:**  
- [x] [nginx](ansible/playbooks/install_nginx.yml) (с помощью [роли](ansible/roles/nginx) ansible)
- [x] [Apache](ansible/playbooks/install_apache.yml) (с помощью [роли](ansible/roles/apache) ansible)
- [x] [PHP](ansible/playbooks/install_php.yml) (с помощью [роли](ansible/roles/php/tasks) ansible)
- [x] [Zabbix-agent](ansible/playbooks/install_zabbix_agent.yml) (с помощью [роли](ansible/roles/zabbix-agent) ansible)
- [x] bind (DNS) - не разворачивал, так как есть купленный личный домен tusher.ru, NS завернут на [cloudflare.com](https://dash.cloudflare.com/)
- [x] Почтовый сервер (Postfix/Exim) (развернут руками, без ролей)
- [x] [filebeat](ansible/playbooks/install_filebeat.yml) (с помощью [роли](ansible/roles/filebeat) ansible)

**Сервер 3:**  
- [x] [PostgreSQL 14](ansible/playbooks/install_postgresql_final.yml) (с помощью [роли](ansible/roles/postgresql) ansible)
- [x] [Zabbix-agent](ansible/playbooks/install_zabbix_agent.yml) (с помощью [роли](ansible/roles/zabbix-agent) ansible)
- [x] [ELK](ansible/playbooks/install_elk_docker_simple.yml) (Elasticsearch, Logstash, Kibana)  (с помощью [роли](ansible/roles/elk_docker) ansible)

**Общее:**  
- [x] Настроить OpenVPN-клиенты на сервере 2 и 3  
- [x] Все роли вынести в GitHub  
- [x] README с пометкой, что установлено вручную  
- [x] Проверить доступ извне: Zabbix, Grafana, Kibana, nginx  

---

## ✅ Часть 2 — Настройка сервисов
- [x] Настроить локальное время (chrony/ntp)  
- [x] Zabbix мониторит все сервера (Linux template)  
- [x] Zabbix мониторит PostgreSQL  
- [x] Zabbix мониторит ELK  
- [x] Зарегистрировать бесплатный домен - имеется купленный личный домен tusher.ru, NS завернут на [cloudflare.com](https://dash.cloudflare.com/)
- [x] Настроить bind (DNS-сервер) - не разворачивал, так как есть купленный личный домен tusher.ru, NS завернут на [cloudflare.com](https://dash.cloudflare.com/)
- [x] Прописать A/NS/MX-записи  
- [x] Проверить резолвинг серверов по именам  
- [x] Filebeat отправляет логи nginx/apache → ELK  
- [x] Проверить логи в Kibana  
- [x] Настроить почту (Postfix)  
- [x] Проверить отправку писем наружу - техпод Yandex Cloud не открыл мне порт 25
- [x] Убедиться, что сервер не open relay  
- [ ] Загрузить БД авиаперелётов в PostgreSQL  
- [ ] Установить pgAdmin (доступ только по VPN)  
- [ ] Настроить nginx как reverse proxy для 2 сайтов  
  - [ ] Сайт заказчика (форма обратной связи + SSL, порт 443)  
  - [ ] Второй сайт (CMS или статический контент)  
- [x] Создать Grafana dashboard: CPU, RAM, Disk usage всех хостов  

---

## ✅ Часть 3 — Финал + Docker + Визитка
- [x] Перенести Zabbix-server в Docker  
- [x] Перенести Grafana в Docker  
- [x] Перенести ELK в Docker  
- [ ] Поднять CMS (WordPress или другая) на nginx  
- [ ] Создать сайт-визитку: о себе + описание проекта  
- [x] Настроить форму обратной связи (через Postfix) - техпод Yandex Cloud не открыл мне порт 25
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

ansible/  
├── hosts.ini # Inventory  
├── site.yml # Общий запуск  
├── README.md # Документация  
├── playbooks  
└── roles  
    ├── apache  
    │   ├── handlers  
    │   ├── tasks  
    │   └── templates  
    ├── docker  
    │   ├── defaults  
    │   ├── handlers  
    │   └── tasks  
    ├── elk_docker  
    │   ├── files  
    │   ├── handlers  
    │   ├── tasks  
    │   └── templates  
    ├── filebeat  
    │   ├── handlers  
    │   ├── tasks  
    │   └── templates  
    ├── mailserver  
    ├── nginx  
    │   ├── tasks  
    │   └── templates  
    ├── openvpn_client  
    ├── php  
    │   ├── tasks  
    │   └── templates  
    ├── postgresql  
    │   ├── defaults  
    │   ├── files  
    │   ├── handlers  
    │   ├── tasks  
    │   └── templates  
    └── zabbix-agent  
        ├── defaults  
        ├── tasks  
        └── template  
37 directories
