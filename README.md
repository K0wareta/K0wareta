# Привет, я Артём 👋

[![vyazka.su](https://img.shields.io/website?url=https%3A%2F%2Fvyazka.su&style=for-the-badge&label=vyazka.su&up_message=online)](https://vyazka.su)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/artem-siainov-626390440)
[![Habr Career](https://img.shields.io/badge/Habr%20Career-6C8DBE?style=for-the-badge&logo=habr&logoColor=white)](https://career.habr.com/kowareta)
[![GitLab](https://img.shields.io/badge/GitLab-FC6D26?style=for-the-badge&logo=gitlab&logoColor=white)](https://gitlab.com/K0wareta)

---

[![SadServers Level](https://img.shields.io/badge/SadServers-Beginner-00838F?style=for-the-badge&labelColor=FFC400&logo=docker&logoColor=1A237E&logoSize=auto)](https://sadservers.com)
[![Codewars](https://www.codewars.com/users/Kowareta/badges/large)](https://www.codewars.com/users/Kowareta)

---

**SRE / DevOps-инженер** · Москва · 2+ года в продакшене · English C1

Строю и сопровождаю инфраструктуру: мониторинг и алертинг, базы данных и бэкапы,
CI/CD, управление конфигурацией. Последние два года отвечал за 200+ хостов
в нескольких дата-центрах для семи продуктовых команд (фискальные сервисы).

---

## 🐾 Пэт-проект: [vyazka.su](https://vyazka.su)

Шуточный «Tinder для собак и кошек». Продукт здесь вторичен — проект показывает
полный путь от коммита до работающего сервиса в Kubernetes на живом проде.

- **Облако и IaC:** k3s на прерываемой ВМ в Yandex Cloud. Terraform создаёт сеть, ВМ, Object Storage и автостоп по бюджету, Ansible ставит k3s, Vault, WireGuard и делает hardening. Обходится примерно в 2 200 ₽/мес вместо ~4 000 ₽/мес за один только мастер Managed Kubernetes
- **GitOps:** Argo CD app-of-apps (16 Application), свои Helm-чарты на общем library-чарте
- **CI/CD:** GitLab CI: pre-commit, gitleaks, pytest на настоящих PostgreSQL/RabbitMQ/Valkey, сборка kaniko, автодеплой коммитом `tag@digest` в git и smoke-проверка версии на проде
- **Наблюдаемость:** kube-prometheus-stack, Loki + Alloy, 21 правило алертов с юнит-тестами promtool в CI, доставка в почту и Telegram
- **Данные и события:** PostgreSQL под CloudNativePG с WAL-архивом, бэкапами в S3 и учением PITR; transactional outbox → RabbitMQ (publisher confirms, dead-letter) → идемпотентный воркер с дедупликацией в Valkey
- **Безопасность:** секреты только в Vault → External Secrets, SSH и Kubernetes API только через WireGuard, kubectl-сертификаты на 8 часов через CSR
- **Процесс:** 250+ merge request'ов, 9 ADR, регулярные аудиты безопасности

📦 Репозиторий и CI — на GitLab: [gitlab.com/vyazka/vyazka-project](https://gitlab.com/vyazka/vyazka-project) · 📄 [Страница для HR](https://vyazka.su/about/hr)

---

## 🛠 Опыт

### Фискальные облачные сервисы · SRE / DevOps-инженер
`июнь 2024 — сентябрь 2026` · production-инфраструктура фискальных сервисов: **200+ хостов** в нескольких ЦОД, **7 продуктовых команд**, окружения dev и prod. Вся инфраструктура описана кодом на SaltStack и Terraform.

#### 📟 Мониторинг и алертинг
- **Перепроектировал алертинг** на Prometheus/Alertmanager: приоритеты P1/P3/P5, разделение по окружениям, проектам и командам, маршрутизация в Telegram, Opsgenie и Grafana IRM. Убрал дубли, ложные и недоходящие алерты: каждая из 7 команд получает только алерты своих сервисов
- **Единая схема мониторинга nginx для 100+ сервисов:** унифицировал зоны во всех vhost, ввёл алерты на 4xx/5xx, upstream errors, 429, время ответа и ошибки reload с разделением на prod/dev и приоритеты
- **Автообнаружение целей в нескольких ЦОД:** конфиг Prometheus генерируется по ролям хостов через salt mine, поэтому новые серверы попадают в мониторинг без ручных правок
- Подключил и обновил 15+ экспортеров (MongoDB, Sentry, Apache, statsd, cAdvisor, Nomad и другие), добавил recording rules для учёта CPU, памяти и дисков по проектам. Разбирал инциденты и писал постмортемы

#### 🚚 Переезд в новый ЦОД
- **Перевёз production:** кластеры MariaDB и **Patroni с обновлением PostgreSQL 11 → 17**, Docker-хосты, Nomad и keepalived на Ubuntu 24.04. Пароли при переезде вынес из кода в Vault
- **Перенёс кластеры Nomad (dev и prod) и 20+ Docker-хостов** на новое железо, обновил GlusterFS 9 → 11, вывел из эксплуатации серверы на CentOS 7
- **Мигрировал все stateful-сервисы dev-окружения:** Cassandra, MySQL/MariaDB, PostgreSQL, Kafka, RabbitMQ, Redis, MongoDB. Пользователи, права и базы, которые раньше заводились руками, теперь описаны в коде, и окружение воспроизводимо

#### 🔁 CI/CD и работа с разработкой
- **Стандартизировал CI/CD для 40+ микросервисов** на Python и JS: единая схема версионирования образов, раздельные registry для test и prod, общие шаблоны деплоя, переезд сервисов на новый кластер Nomad
- **Убрал токены из образов:** сборка бэкенда через Docker BuildKit secrets для доступа к приватному Nexus
- **Перенёс CI-инфраструктуру разработки** (Jenkins, Gerrit, GitLab Runner) на новые серверы и описал Jenkins целиком в SaltStack: плагины, ноды, пользователи. Сборочные воркеры развернул в Nomad через Terraform, до 8 параллельно
- Готовил тестовые базы под запросы команд, помогал разработчикам с доступами и падающими сборками

#### 🛡 Надёжность и качество
- **Резервное копирование на Bareos:** PostgreSQL (pg_basebackup с реплики), MySQL, MongoDB, Jenkins, Consul, серверы продуктовых команд
- **Линтинг инфраструктурного кода** в GitLab CI: yamllint и salt-lint только по изменённым файлам
- **Структурированные JSON-логи** Kafka и RabbitMQ с доставкой в ELK через GELF и Logstash, ревизия устаревших пайплайнов
- **DNS-зоны компании в коде:** Terraform + Google Cloud DNS

---

## 🧰 Стек

**Оркестрация и контейнеры**
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![k3s](https://img.shields.io/badge/k3s-FFC61C?style=flat-square&logo=k3s&logoColor=black)
![Nomad](https://img.shields.io/badge/Nomad-00CA8E?style=flat-square&logo=nomad&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat-square&logo=argo&logoColor=white)
![Envoy Gateway](https://img.shields.io/badge/Envoy%20Gateway-AC6199?style=flat-square&logo=envoyproxy&logoColor=white)
![cert-manager](https://img.shields.io/badge/cert--manager-326CE5?style=flat-square)

**IaC и конфигурация**
![Terraform](https://img.shields.io/badge/Terraform-844FBA?style=flat-square&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![SaltStack](https://img.shields.io/badge/SaltStack-2F7A77?style=flat-square&logo=salt&logoColor=white)

**Облако и сеть**
![Yandex Cloud](https://img.shields.io/badge/Yandex%20Cloud-5282FF?style=flat-square&logo=yandexcloud&logoColor=white)
![nginx](https://img.shields.io/badge/nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Consul](https://img.shields.io/badge/Consul-F24C53?style=flat-square&logo=consul&logoColor=white)
![keepalived](https://img.shields.io/badge/keepalived-555555?style=flat-square)
![WireGuard](https://img.shields.io/badge/WireGuard-88171A?style=flat-square&logo=wireguard&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)
![Let's Encrypt](https://img.shields.io/badge/Let's%20Encrypt-003A70?style=flat-square&logo=letsencrypt&logoColor=white)

**CI/CD**
![GitLab CI](https://img.shields.io/badge/GitLab%20CI-FC6D26?style=flat-square&logo=gitlab&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
![Gerrit](https://img.shields.io/badge/Gerrit-EEEEEE?style=flat-square&logo=gerrit&logoColor=black)
![Nexus](https://img.shields.io/badge/Nexus-1B1C30?style=flat-square&logo=sonatype&logoColor=white)

**Наблюдаемость**
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Alertmanager](https://img.shields.io/badge/Alertmanager-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Loki](https://img.shields.io/badge/Loki-F2CC0C?style=flat-square&logo=grafana&logoColor=black)
![Alloy](https://img.shields.io/badge/Alloy-F46800?style=flat-square&logo=grafana&logoColor=white)
![Zabbix](https://img.shields.io/badge/Zabbix-D40000?style=flat-square&logo=zabbix&logoColor=white)
![ELK](https://img.shields.io/badge/ELK-005571?style=flat-square&logo=elasticsearch&logoColor=white)
![Sentry](https://img.shields.io/badge/Sentry-362D59?style=flat-square&logo=sentry&logoColor=white)

**Базы данных и очереди**
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Patroni](https://img.shields.io/badge/Patroni-336791?style=flat-square)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Cassandra](https://img.shields.io/badge/Cassandra-1287B1?style=flat-square&logo=apachecassandra&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Valkey](https://img.shields.io/badge/Valkey-6983FF?style=flat-square)

**Бэкапы и хранилища**
![Bareos](https://img.shields.io/badge/Bareos-0074BC?style=flat-square)
![GlusterFS](https://img.shields.io/badge/GlusterFS-555555?style=flat-square)
![S3](https://img.shields.io/badge/S3%20Object%20Storage-569A31?style=flat-square&logo=amazons3&logoColor=white)

**Безопасность**
![Vault](https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black)
![External Secrets](https://img.shields.io/badge/External%20Secrets-326CE5?style=flat-square)

**Языки и основа**
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

---

## 🎓 Образование

Высшее, МАИ, «Прикладная информатика» (2020–2024)

---

## 📬 Контакты
[![Telegram](https://img.shields.io/badge/Telegram-@hatedbylifeitself-26A5E4?style=flat-square&logo=telegram&logoColor=white)](https://t.me/hatedbylifeitself)
[![Email](https://img.shields.io/badge/Email-vacancy.a.syainov@mail.ru-005FF9?style=flat-square&logo=maildotru&logoColor=white)](mailto:vacancy.a.syainov@mail.ru)
****
