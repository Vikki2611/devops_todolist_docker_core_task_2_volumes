# How to run the project

## Docker Hub repositories

MySQL image: https://hub.docker.com/r/vikkinech/mysql-local
App image: https://hub.docker.com/r/vikkinech/todoapp

## Project dependencies

The application dependencies are listed in `requirements.txt`
Make sure `requirements.txt` contains:

`mysql-connector-python==8.2.0`

Install dependencies locally if needed:

`pip install -r requirements.txt`

## Create Docker network

`docker network create app-net`

## Run MySQL container

```bash
  docker run -d \
  --name mysql-container \
  --network app-net \
  -e MYSQL_DATABASE=app_db \
  -e MYSQL_USER=app_user \
  -e MYSQL_PASSWORD=1234 \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -v mysql-data:/var/lib/mysql \
  vikkinech/mysql-local:1.0.0
```

## Run application container

```bash
  docker run -d \
  --name todoapp-container \
  --network app-net \
  -e DB_HOST=mysql-container \
  -p 8000:8000 \
  vikkinech/todoapp:2.0.0
```

## Run database migrations

Run migrations inside the app container:

`docker exec -it todoapp-container python manage.py migrate`

## Start Django server

The Django development server starts automatically when the app container runs.

If you need to start it manually inside the container:

`docker exec -it todoapp-container python manage.py runserver 0.0.0.0:8000`

## Open application in browser

http://localhost:8000



