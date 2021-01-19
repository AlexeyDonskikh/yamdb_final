# API YaMDB

![yamdb](https://github.com/AlexeyDonskikh/yamdb_final/workflows/yamdb/badge.svg)

REST API для сервиса YaMDb — базы отзывов о фильмах, книгах и музыке.
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».

# Развёртывание проекта 

Запустить приложение

    docker-compose up

Зайти в контейнер web:

    docker exec -it <CONTAINER ID> bash

Для выполнения миграций, загрузки статики и заполнения базы данных запустить entrypoint.sh

    bash entrypoint.sh

Для выхода из контейнера выполнить команду

    exit

Остановить работу и удалить контейнеры 

    docker-compose down

# Регистрация
Регистрация/авториация по email

Аутентификация по JWT-токену

# Пользовательские роли
Аноним — может просматривать описания произведений, читать отзывы и комментарии.

Аутентифицированный пользователь (user)— может читать всё, как и Аноним, дополнительно может публиковать отзывы и ставить рейтинг произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять свои отзывы и комментарии.

Модератор (moderator) — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.

Администратор (admin) — полные права на управление проектом и всем его содержимым. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.

Администратор Django — те же права, что и у роли Администратор.

# Алгоритм регистрации пользователей
Пользователь отправляет POST-запрос с параметром email на /api/v1/auth/email/.

YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email .

Пользователь отправляет POST-запрос с параметрами email и confirmation_code на /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).

Эти операции выполняются один раз, при регистрации пользователя. В результате пользователь получает токен и может работать с API, отправляя этот токен с каждым запросом.

После регистрации и получения токена пользователь может отправить PATCH-запрос на /api/v1/users/me/ и заполнить поля в своём профайле (описание полей — в /redoc).

Если пользователя создаёт администратор (например, через POST-запрос api/v1/users/...) — письмо с кодом отправлять не нужно.

# Ресурсы API YaMDb
Ресурс AUTH: аутентификация.

Ресурс USERS: пользователи.

Ресурс TITLES: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).

Ресурс CATEGORIES: категории (типы) произведений («Фильмы», «Книги», «Музыка»).

Ресурс GENRES: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.

Ресурс REVIEWS: отзывы на произведения. Отзыв привязан к определённому произведению.

Ресурс COMMENTS: комментарии к отзывам. Комментарий привязан к определённому отзыву.


### Актуальный адрес сайта

<http://84.201.138.108:9000/api/v1/>


# Автор проекта

Донских Алексей

[LinkedIn](https://www.linkedin.com/in/alexey-donskikh/ "LinkedIN автора")

[Telegram](https://www.t.me/donskikhalexey/ "@donskikhalexey")
