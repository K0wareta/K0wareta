# Привет, я Артём 👋

[![Open to work](https://img.shields.io/badge/Open%20to%20work-DevOps%20%2F%20SRE-2EA44F?style=for-the-badge)](#-контакты)
[![vyazka.su](https://img.shields.io/website?url=https%3A%2F%2Fvyazka.su&style=for-the-badge&label=vyazka.su&up_message=online)](https://vyazka.su)
[![pipeline](https://gitlab.com/vyazka/vyazka-project/badges/main/pipeline.svg)](https://gitlab.com/vyazka/vyazka-project/-/pipelines)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/ВАШ_НИК)
[![Habr Career](https://img.shields.io/badge/Habr%20Career-6C8DBE?style=for-the-badge&logo=habr&logoColor=white)](https://career.habr.com/ВАШ_НИК)
[![GitLab](https://img.shields.io/badge/GitLab-FC6D26?style=for-the-badge&logo=gitlab&logoColor=white)](https://gitlab.com/ВАШ_НИК)

[![SadServers Level](https://img.shields.io/badge/SadServers-Beginner-00838F?style=for-the-badge&labelColor=FFC400&logo=docker&logoColor=1A237E&logoSize=auto)](https://sadservers.com)
[![Codewars](https://www.codewars.com/users/Kowareta/badges/large)](https://www.codewars.com/users/Kowareta)

**DevOps / SRE-инженер** · Москва · 2+ года в продакшене · English C1

Строю и сопровождаю инфраструктуру: мониторинг и алертинг, базы данных и бэкапы,
CI/CD, управление конфигурацией. Последние два года отвечал за 200+ хостов
в нескольких дата-центрах для семи продуктовых команд (фискальные сервисы).

🔎 **Ищу работу DevOps/SRE**: удалёнка (в том числе international), гибрид в Москве тоже подходит.

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

## 🛠 Опыт в продакшене

- **Мониторинг и алертинг:** перепроектировал алертинг на Prometheus/Alertmanager: приоритеты P1/P3/P5, маршрутизация в Telegram, Opsgenie и Grafana IRM, дедупликация
- **Базы данных:** переезд в другой ДЦ вместе с обновлением PostgreSQL 11 → 17 на Patroni. Ещё в работе были MySQL/MariaDB, MongoDB и Cassandra с бэкапами через Medusa
- **CI/CD:** пайплайны для 40+ микросервисов на GitLab CI и Jenkins
- **Конфигурация:** SaltStack (states, pillar, Jinja), больше тысячи коммитов в инфраструктурный репозиторий
- **Бэкапы и хранилища:** Bareos, GlusterFS
- **Сеть и балансировка:** nginx, Consul / consul-template, keepalived

## 🧰 Стек

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat-square&logo=argo&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-844FBA?style=flat-square&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![SaltStack](https://img.shields.io/badge/SaltStack-2F7A77?style=flat-square&logo=salt&logoColor=white)
![Yandex Cloud](https://img.shields.io/badge/Yandex%20Cloud-5282FF?style=flat-square&logo=yandexcloud&logoColor=white)
![GitLab CI](https://img.shields.io/badge/GitLab%20CI-FC6D26?style=flat-square&logo=gitlab&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Loki](https://img.shields.io/badge/Loki-F2CC0C?style=flat-square&logo=grafana&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)
![Vault](https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black)
![nginx](https://img.shields.io/badge/nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

## 🎓 Образование

Высшее, МАИ, «Прикладная информатика» (2020–2024)

---

## 📬 Контакты
[![Telegram](https://img.shields.io/badge/Telegram-@hatedbylifeitself-26A5E4?style=flat-square&logo=telegram&logoColor=white)](https://t.me/hatedbylifeitself)
[![Email](https://img.shields.io/badge/Email-a.syainov@mail.ru-005FF9?style=flat-square&logo=maildotru&logoColor=white)](mailto:a.syainov@mail.ru)

[![Telegram](https://img.shields.io/badge/Telegram-@hatedbylifeitself-26A5E4?style=flat-square&logo=telegram&logoColor=white)](https://t.me/hatedbylifeitself)
[![Email](https://img.shields.io/badge/Email-a.syainov@mail.ru-005FF9?style=flat-square&logo=maildotru&logoColor=white)](mailto:a.syainov@mail.ru)
