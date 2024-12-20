# Taski

## Описание проекта
Веб-приложение трекер задач. Позволяет пользователям создавать, редактировать, удалять задачи, а также отмечать их выполнение.

## Использованные технологии
- Python 3.9
- Django 3.2.3
- Django REST Framework 3.12.4
- PostgreSQL
- Docker
- Nginx
- Gunicorn
- Node.js


## Установка и запуск проекта на удалённом сервере

1. Настройте Nginx. Выполните команду `sudo nano /etc/nginx/sites-enabled/default`    
* Если на вашем сервере порт `8000` занят, можете указать другой, например `9000`
    ```
    server {
        server_name ВАШ_ДОМЕН;

        location /api/ {
            proxy_set_header Host $http_host;
            proxy_pass http://127.0.0.1:8000;
        }

        location /admin/ {
            proxy_set_header Host $http_host;
            proxy_pass http://127.0.0.1:8000;
        }

        location / {
            proxy_set_header Host $http_host;
            proxy_pass http://127.0.0.1:8000;
        }
    }
    ```

2. На сервере создайте папку проекта `taski`, скопируйте в неё файл `docker-compose.yml`
[Как это сделать?](https://help.reg.ru/support/servery-vps/oblachnyye-servery/rabota-s-serverom/kopirovaniye-faylov-cherez-ssh#0)

3. Авторизуйтесь в Docker `docker login -u <ваш-username>`

4. Выполните команду `docker compose -f docker-compose.yml up -d` и дождитесь окончания запуска контейнеров

5. Выполните миграции `docker compose -f docker-compose.yml exec backend python manage.py migrate`

6. Выполните команды `docker compose exec backend python manage.py collectstatic` и    
    `docker compose exec backend cp -r /app/collected_static/. /backend_static/static/` для сбора статики бэкенда.


## Автор: Иван Данилин
GitHub: [0VVaRRa0](https://github.com/0VVaRRa0)    
Gmail: vvarra.work@gmail.com
