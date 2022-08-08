# yamdb_final

![yamdb_workflow.yml](https://github.com/Svetlana2207/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

# Ссылка на проект: https://51.250.96.115/admin/

# Документация к API проекта Yatube:
по адресу https://51.250.96.115/redoc/ будет доступна документация для API Yatube
 

### Проект YaMDb.
Описание:
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Возможности:
Просматривать, создавать новые, удалять и изменять отзывы.
Комментировать отзывы, смотреть, удалять и обновлять комментарии к отзывам.

### Как запустить проект в контейнере docker:

Заполнить переменные окружения .env
DB_ENGINE=
DB_NAME=
POSTGRES_USER=
POSTGRES_PASSWORD=
DB_HOST=
DB_PORT=
SECRET_KEY=
```

Запустить docker-compose командой:

docker-compose up -d --build
```

Собрать статику и выполнить миграции внутри контейнера, создать суперпользователя:

docker-compose exec web python manage.py migrate --noinput
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input


### Деплой на удаленном сервере:

Для запуска на удаленном сервере необходимо:

перенести файлы docker-compose.yaml и папку nginx на сервер, выполнив команду:

scp -r ./infra/* <username>@<server_ip>:/home/<username>/

на github, в настройках репозитория Secrets --> Actions создать и заполнить переменные окружения:

DOCKER_USERNAME # Имя пользователя на Docker Hub;
DOCKER_PASSWORD # Пароль от Docker Hub;
DB_ENGINE # Указать, что работаем с базой данных PostgresQl;
DB_NAME # Имя базы данных;
DB_HOST # Название контейнера базы данных; 
DB_PORT # Порт для подключения к базе данных;
POSTGRES_USER # Логин для подключения к базе данных;
POSTGRES_PASSWORD # Пароль для подключение к базе данных;
SECRET_KEY # Секретный ключ приложения;
USER # Имя пользователя на сервере;
HOST # Публичный IP-адрес сервера;
PASSPHRASE # Указать в том случае, если ssh-ключ защищен фразой-паролем;
SSH_KEY # Приватный ssh-ключ;
TELEGRAM_TO # ID телеграм-аккаунта;
TELEGRAM_TOKEN # Токен телеграм-бота.
``` 

После каждого пуша (git push) в главную ветку main:

будут автоматически запускаться тесты: 
проверка кода на соответствие стандарту PEP8 (с помощью пакате flake8) и запуск pytest из репозитория yamdb_final;
сборка и доставка докер-образа на Docker Hub;
автоматический деплой на боевой сервер;
отправка сообщения в Telegram при успешном завершении деплоя.
``` 


### Aвтор: [Svetlana2207](https://github.com/Svetlana2207)

