# Create New Mysql Volume

    - docker volume create <volume name>

# Create New Mysql Network

    - docker network create <network name>

# MySql Docker-compose.ym

```
version: "3.8"
services:
  database:
    image: mysql:lastest
    restart: always
    ports:
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin
    volumes:
      - mysql:/var/lib/mysql
    networks:
      - backend

networks:
  backend:
    external: true

volumes:
  mysql:
  external: true

```
