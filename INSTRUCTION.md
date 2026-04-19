# How to run the project

## Docker Hub repositories

MySQL image: https://hub.docker.com/r/vikkinech/mysql-local
App image: https://hub.docker.com/r/vikkinech/todoapp

## Run MySQL container

docker run -d \
  --name mysql-container \
  -e MYSQL_DATABASE=app_db \
  -e MYSQL_USER=app_user \
  -e MYSQL_PASSWORD=1234 \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -v mysql-data:/var/lib/mysql \
  vikkinech/mysql-local:1.0.0

## Run app container

docker run -d \
  --name todoapp-container \
  -p 8000:8080 \
  vikkinech/todoapp:2.0.0

## Open application in browser

http://localhost:8000

