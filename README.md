# Проект Kittygram 

![Kittygram Workflow](https://github.com/lkofe1/kittygra_final/actions/workflows/main.yml/badge.svg)

## Описание
**Kittygram** — это социальная сеть для любителей котиков. Проект представляет собой полноценное веб-приложение, где пользователи могут регистрироваться, публиковать фотографии своих питомцев, указывать их характеристики (имя, достижения, возраст и цвет), а также просматривать карточки котиков других пользователей.

### Основные функции приложения:
* **Управление профилем:** Регистрация и аутентификация пользователей на базе токенов (Djoser).
* **Контент:** Добавление, редактирование, просмотр и удаление карточек питомцев.
* **Автоматизация (CI/CD):** Автоматический запуск тестов, проверка линтером, сборка свежих Docker-образов и деплой на удаленный сервер при каждом пуше в ветку `main`.

---

## Стек технологий
* **Backend:** Python 3.12, Django, Django REST Framework, Djoser, Gunicorn
* **Frontend:** React, HTML5, CSS3
* **Database:** PostgreSQL 13
* **Infrastructure:** Docker, Docker Compose, Nginx, Linux (Ubuntu)
* **CI/CD:** GitHub Actions, Telegram API

---

## Инструкция по локальному развертыванию

1. **Клонируйте репозиторий и перейдите в него:**
   ```bash
   git clone [https://github.com/lkofe1/kittygra_final.git](https://github.com/lkofe1/kittygra_final.git)
   cd kittygra_final

2. Настройте переменные окружения:
    В корневой директории проекта создайте файл .env и заполните его по шаблону, описанному в разделе ниже.

3. Запустите проект в Docker-контейнерах:
    sudo docker compose up -d --build

4. Выполните миграции бэкенда:
    sudo docker compose exec backend python manage.py migrate

5. Соберите статичные файлы приложения:
    sudo docker compose exec backend python manage.py collectstatic --no-input

# Теперь проект будет доступен локально по адресу: http://localhost


# Настройка окружения (Шаблон файла .env)
    Для успешного запуска проекта как локально, так и на сервере, создайте файл .env в корневой директории со следующими переменными:

# Настройки Django
    SECRET_KEY=ваш_секретный_ключ_django
    DEBUG=False
    ALLOWED_HOSTS=127.0.0.1,localhost,158.160.224.159,gateway,backend

# Настройки базы данных PostgreSQL
    DB_ENGINE=django.db.backends.postgresql
    POSTGRES_DB=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=ваш_пароль_к_базе
    DB_HOST=db
    DB_PORT=5432

# Настройка CI/CD (GitHub Actions)
    Процесс автоматизации разбит на следующие этапы:

    1. Тестирование: Проверка кода линтером flake8 и запуск встроенных Django-тестов на матрице версий Python (3.9, 3.10, 3.11, 3.12).

    2. Сборка и публикация: Сборка Docker-образов для бэкенда, фронтенда и Nginx (gateway) и их отправка на Docker Hub.

    3. Деплой: Автоматическое подключение к удаленному серверу по SSH, загрузка обновленных образов, применение миграций, сбор статики и перезапуск контейнеров.

    4. Уведомление: Отправка сообщения в Telegram со ссылкой на коммит и информацией об авторе пуша.

# Автор
    lkofe1 — Разработка инфраструктуры, контейнеризация приложений, настройка веб-сервера Nginx и конфигурация пайплайна CI/CD.
