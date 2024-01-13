# Docker compose file for phpmyadmin

```
version: "3.8"
services:
  database:
    image: mysql:latest
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

  phpmyadmin:
    image: phpmyadmin
    restart: always
    ports:
      - 8080:80
    environment:
      PMA_HOST: database
      PMA_PORT: 3306
    depends_on:
      - database
    networks:
      - backend

networks:
  backend:
    external: true

volumes:
  mysql:
  external: true

```
