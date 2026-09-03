# Kittygram

[![Main Kittygram workflow](https://github.com/Matvey53/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/Matvey53/kittygram_final/actions/workflows/main.yml)

Веб-приложение для публикации фотографий котиков: регистрация и вход по токену, лента, загрузка изображений, админка Django.

Рабочий адрес:

- Kittygram: https://kittygram.publicvm.com

## Стек

- Backend: Python 3.12, Django 5, Django REST Framework, Djoser, Gunicorn, PostgreSQL
- Frontend: React
- Инфраструктура: Docker, Docker Compose, Nginx
- CI/CD: GitHub Actions, Docker Hub, деплой по SSH, уведомление в Telegram

## Переменные окружения

Скопируйте `.env.example` в `.env` и заполните значения:

| Переменная | Описание |
| --- | --- |
| `SECRET_KEY` | Секретный ключ Django |
| `DEBUG` | `True` или `False` (сравнение без учёта регистра) |
| `ALLOWED_HOSTS` | Хосты через запятую, например `localhost,127.0.0.1,kittygram.publicvm.com` |
| `CSRF_TRUSTED_ORIGINS` | Trusted origins через запятую, например `https://kittygram.publicvm.com` |
| `USE_SQLITE` | `True` — SQLite для быстрых локальных проверок, иначе PostgreSQL |
| `DOCKER_USERNAME` | Логин Docker Hub (подставляется в имена образов) |
| `POSTGRES_DB` | Имя базы PostgreSQL |
| `POSTGRES_USER` | Пользователь PostgreSQL |
| `POSTGRES_PASSWORD` | Пароль PostgreSQL |
| `DB_HOST` | Хост БД (`db` в Docker, `127.0.0.1` локально) |
| `DB_PORT` | Порт PostgreSQL |

## Локальный запуск в Docker

Файл `docker-compose.yml` нужен только локально (в git не хранится). Пример:

```bash
cp .env.example .env
docker compose up -d --build
```

Приложение будет доступно на http://localhost:9000

## Продакшен

На сервере используется `docker-compose.production.yml` и образы с Docker Hub. Деплой выполняется GitHub Actions при пуше в `main`: тесты, сборка образов, `docker compose pull/up`, миграции, `collectstatic`.

Секреты репозитория: `DOCKER_USERNAME`, `DOCKER_PASSWORD`, `HOST`, `USER`, `SSH_KEY`, `TELEGRAM_TO`, `TELEGRAM_TOKEN`.

## Тесты

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r backend/requirements.txt
pytest
```

## Автор

[Matvey53](https://github.com/Matvey53)
