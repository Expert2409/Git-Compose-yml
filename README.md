# Git-Compose-yml

version: "3.8"

services:
  mysql:
    image: mysql:5.7
    container_name: mysql-db
    environment:
      MYSQL_ROOT_PASSWORD: ADMIN
      MYSQL_DATABASE: MYDB
    ports:
      - "3306:3306"
    networks:
      - twotier
    volumes:
      - container-data:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-u", "root", "-pADMIN"]
      interval: 10s
      timeout: 5s
      retries: 10
      start_period: 60s

  flask-app:
    build:
      context: .
    container_name: flask-app
    environment:
      MYSQL_ROOT_PASSWORD: ADMIN
      MYSQL_DB: MYDB
      MYSQL_HOST: mysql-db
-- INSERT --                                                                                                                        3,10          Top








