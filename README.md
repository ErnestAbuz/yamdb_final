# API_YAMDB. 
![example workflow](https://github.com/ErnestAbuz/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

<p align="center">
  <a>CI и CD проекта api_yamdb</a>
</p>

# Описание проекта.
Настройка Continuous Integration и Continuous Deployment для приложения API YAMDB:
- автоматический запуск тестов,
- обновление образов на Docker Hub,
- автоматический деплой на боевой сервер при пуше в главную ветку main.

## Запуск проекта:

Клонируем репозиторий
```
git clone https://github.com/ErnestAbuz/yamdb_final
cd yamdb_final
cd api_yamdb
```
Cоздаем и активируем виртуальное окружение:
```
python3 -m venv venv
source venv/Scripts/activate либо venv/bin/activate
```
Установим зависимости из файла requirements.txt:
```
pip install -r requirements.txt
```
Поднимаем контейнеры :
```
docker-compose up -d --build
```
Выполняем миграции:
```
docker-compose exec web python manage.py migrate
```
Создаем суперпользователя:
```
docker-compose exec web python manage.py createsuperuser
```
Собираем статику:
```
docker-compose exec web python manage.py collectstatic --no-input
```
Создаем дамп (резервную копию) базы данных:
```
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```
Останавливаем контейнеры:
```
docker-compose down -v
```

## Примеры запросов:

- Получение списка доступных сообществ:

- Запрос:
```
GET http://51.250.64.159:8000/api/v1/groups/
```

- Ответ:
```
[
  {
    "id": 0,
    "title": "string",
    "slug": "string",
    "description": "string"
  }
]
```

- Добавление нового комментария к публикации:

- Запрос:
```
POST http://51.250.64.159:8000/api/v1/posts/{post_id}/comments/
```

```
{
  "text": "Ваш текст"
}
```

- Ответ:
```
{
  "id": 1,
  "author": "author",
  "text": "Ваш текст",
  "created": "2022-07-24T17:15:00Z",
  "post": 1
}
```

## Технологии в проекте
- **Python**
- **Django Framework**
- **Django Rest Framework**
- **Django Rest Framework Simplejwt**
- **Docker**
- **REST API**
- **PostgreSQL**
- **Docker Compose**

## Разработчик
* [ErnestAbuz](https://github.com/ErnestAbuz)