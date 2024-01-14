change db host to mysql container name

# Dockerfile

```
    #1st build base php
    FROM php:8.1-fpm

    RUN apt-get update && apt-get install -y \
        curl \
        libonig-dev \
        libzip-dev \
        unzip \
        zip

    RUN docker-php-ext-install pdo_mysql && \
        docker-php-ext-install zip

    RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

    WORKDIR /var/www

    COPY . .

    ENV COMPOSER_ALLOW_SUPERUSER=1

    RUN composer update

    RUN cp .env.example .env

    RUN php artisan optimize

    CMD php artisan serve --host=0.0.0.0 --port=8000

```

# docker-compose file

```
    version: "3.8"
    services:
        app:
            build:
                context: .
                dockerfile: Dockerfile
            ports:
                - "8000:8000"
            environment:
                - DB_PORT=3306
                - DB_DATABASE=laravel
                - DB_USERNAME=root
                - DB_PASSWORD=root
            networks:
                - backend

    networks:
        backend:
            external: true

```

# Mysql

# Laravel without Docker

-   If
