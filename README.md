# YaMDb

### Описание
Это групповой проект. Разработан в учебных целях.
Проект YaMDb собирает отзывы пользователей на произведения.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
### Технологии
Проект написан на python3 на базе django framework со встроенной api документацией Redoc.
Настроена авторизация по коду подтверждения и токену с использованием библиотеки jwt.
Разделение прав доступа через permissions.
Есть возможность фильтрации и поиска данных.
Написана команда import_csv с использованием библиотек csv и sqlite.
### Установка
Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/egorkomel/YaMDb
```

```
cd api_yamdb
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv env
```

```
source env/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```
Документация в redoc доступна после запуска проекта по адресу
```
http://127.0.0.1:8000/redoc/
```
### Примеры
#### Регистрация:
```
POST
http://127.0.0.1:8000/api/v1/auth/signup/
data:
{
    "username": "admin2",
    "email": "admin2@mail.ru"
}
Response
{
"email": "string",
"username": "string"
}

```
#### Получение токена:
```
POST
http://127.0.0.1:8000/api/v1/auth/token/
{
    "username": "admin2",
    "confirmation_code": "239123"
}
Response
{
"token": "string"
}
```
#### Произведения:
```
GET
http://127.0.0.1:8000/api/v1/titles/[<title id>/]
Response
{
"id": 0,
"name": "string",
"year": 0,
"rating": 0,
"description": "string",
"genre": [
{
"name": "string",
"slug": "string"
}
],
"category": {
"name": "string",
"slug": "string"
}
}

POST
http://127.0.0.1:8000/api/v1/titles/
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
Response

{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
PATCH, DEL
http://127.0.0.1:8000/api/v1/titles/<title id>/
```
#### Категории:
```
GET
http://127.0.0.1:8000/api/v1/categories/
Response
{
"count": 0,
"next": "string",
"previous": "string",
"results": [
{
"name": "string",
"slug": "string"
}
]
}
POST
http://127.0.0.1:8000/api/v1/categories/
{
"name": "string",
"slug": "string"
}
Response
{
"name": "string",
"slug": "string"
}
DEL
http://127.0.0.1:8000/api/v1/categories/<category id>/
```
#### Жанры:
```
GET
http://127.0.0.1:8000/api/v1/genres/
Response
{
"count": 0,
"next": "string",
"previous": "string",
"results": [
{
"name": "string",
"slug": "string"
}
]
}
POST
http://127.0.0.1:8000/api/v1/genres/
{
"name": "string",
"slug": "string"
}
Response
{
"name": "string",
"slug": "string"
}
DEL
http://127.0.0.1:8000/api/v1/genres/<genre id>/
```
#### Ревью:
```
GET
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/[<review id/]
{
"count": 0,
"next": "string",
"previous": "string",
"results": [
{
"id": 0,
"text": "string",
"author": "string",
"score": 1,
"pub_date": "2019-08-24T14:15:22Z"
}
]
}

POST
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/
{
"text": "string",
"score": 1
}
Response
{
"id": 0,
"text": "string",
"author": "string",
"score": 1,
"pub_date": "2019-08-24T14:15:22Z"
}
PATCH, DEL
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/
```
#### Комментарии:
```
GET
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/[<comment id>/]
{
"count": 0,
"next": "string",
"previous": "string",
"results": [
{
"id": 0,
"text": "string",
"author": "string",
"pub_date": "2019-08-24T14:15:22Z"
}
]
}

POST
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/
{
"text": "string"
}
Response
{
"id": 0,
"text": "string",
"author": "string",
"pub_date": "2019-08-24T14:15:22Z"
}
PATCH, DEL
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/comments/{comment_id}/```
```
#### Пользователи:
```
GET
http://127.0.0.1:8000/api/v1/users/
Response
{
"count": 0,
"next": "string",
"previous": "string",
"results": [
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
]
}
POST
http://127.0.0.1:8000/api/v1/users/
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
Response
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
Get user by username
GET
http://127.0.0.1:8000/api/v1/users/{username}/
Response
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
PATCH
http://127.0.0.1:8000/api/v1/users/{username}/
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
Response
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
DEL
http://127.0.0.1:8000/api/v1/users/{username}/

Get own user data
GET
http://127.0.0.1:8000/api/v1/users/me/
Response
{
"username": "string",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
PATCH
http://127.0.0.1:8000/api/v1/users/me/
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string"
}
Response
{
  "username": "string",
  "email": "user@example.com",
  "first_name": "string",
  "last_name": "string",
  "bio": "string",
  "role": "user"
}
```
#### Скрипт import_csv
Умеет читать данные из базы, записывать данные в базу, удалять данные из таблицы.
Скрипт проверяет наличие файла в `api_yamdb/static/data/`.
Прочитать данные из таблицы на основе файла
```
python manage.py import_csv --read category.csv
```
Записать данные в таблицу, на основе файла
```
python manage.py import_csv --write category.csv`
```
Удалить данные из таблицы на основе файла 
```
python manage.py import_csv --delete category.csv
```

### Разработчики:
Антон Козлов  
Егор Комелягин  
Левченко Анатолий  
