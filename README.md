## Тестовое задание

Решение принимается в виде PR к текущему проекту.

Есть несколько рабочих сервисов, у каждого сервиса есть состояние работает/не работает/работает нестабильно.

Требуется написать API который:

1. Получает и сохраняет данные: имя, состояние, описание
2. Выводит список сервисов с актуальным состоянием
3. По имени сервиса выдает историю изменения состояния и все данные по каждому состоянию

Дополнительным плюсом будет

1. По указанному интервалу выдается информация о том сколько не работал сервис и считать SLA в процентах до 3-й запятой

Вывод всех данных должен быть в формате JSON

# Сервис
Проект предназначен для отслеживания и управления статусами различных сервисов. 
Он предоставляет API для обновления и получения статусов сервисов, а также 
вычисления уровня доступности (SLA) сервисов за заданный период времени.

## Возможности проекта
1. Обновление статуса сервиса - API позволяет обновлять статус сервиса и сохранять 
историю изменений.
2. Получение актуального статуса всех сервисов - API предоставляет список всех 
сервисов с их актуальными статусами.
3. Расчет уровня доступности (SLA) - API позволяет вычислить уровень доступности 
сервиса за указанный период времени на основе сохраненной истории статусов.

## Технологии
- FastAPI - для создания API
- SQLAlchemy - для работы с базой данных
- PostgreSQL - в качестве базы данных
- Alembic - для управления миграциями базы данных
- Poetry - для управления зависимостями и упаковки проекта
- Docker - для контейнеризации приложения

## Установка:

### Предварительные требования
- Docker
- Docker Compose

1. **Клонирование репозитория**

> git clone https://github.com/artem-sitd/ServiceStatusFastAPI.git

1.1 Редактирование переменных окружения:
- для работы в docker: необходимо переименовать файл `.env.docker.template` в `.env.docker` (**можете его не редактировать**)
- без docker: перейменовать файл `.env.template` в `.env`.

Переменные:
- `POSTGRES_USER` - имя пользователя postgresql (по умолчанию postgres)
- `POSTGRES_PASSWORD` - пароль пользователя 
- `POSTGRES_HOST` - название контейнера в docker или url (например localhost)
- `POSTGRES_DB` - название базы

2. **Сборка и запуск докер контейнеров**

> docker-compose up --build

3. **Можно пользоваться приложением.**

## Использование

API предоставляет следующие конечные точки:
- `GET /services` - Отдает список всех сервисов
- `POST /services` - Создает новый сервис в postgresql
- `POST /services/{name}` - Принимает статус сервиса, с указанием его имени - и записывает новый статус в бд
- `GET /service/sla` - Считает и выводит SLA сервиса по имени, start_time, end_time (передать в json body)
- `GET /service/history` - Показывает все сервисы с последним актуальным статусом
- `GET /service/history/{name}` - Показывает историю сервиса, указанного по имени

#### Документация API находится по адресу `localhost:8000/docs`
<img height="200" src="https://github.com/artem-sitd/ServiceStatusFastAPI/assets/22573129/4db378c0-f5f9-4d6f-8641-3e8bf0cd33ce">


## Структура проекта

- app/ - директория с исходным кодом приложения
- main.py - точка входа в приложение
- app/models.py - модели базы данных
- app/schemas.py - схемы Pydantic
- app/crud.py - маршруты API
- settings.py - настройки базы данных
- alembic/ - директория для миграций Alembic
- pyproject.toml - зависимости и настройки Poetry
- Dockerfile - инструкция по сборке Docker-образа
- docker-compose.yml - конфигурация Docker Compose










