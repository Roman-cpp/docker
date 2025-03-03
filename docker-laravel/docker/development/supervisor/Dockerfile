FROM php:8.3-fpm-alpine

# Установка supervisord
RUN apk update && apk add --no-cache supervisor

# Создание директорий для логов и сокета
RUN mkdir -p /var/log/supervisor /var/run/supervisor && \
    chown -R www-data:www-data /var/log/supervisor /var/run/supervisor

# Установка зависимостей для PostgreSQL
RUN apk add --no-cache \
    postgresql-dev

# Установка PHP-расширений
RUN docker-php-ext-install pdo_pgsql
# Копирование конфигурации Supervisord
# COPY supervisord.conf /etc/supervisord.conf

# Настройка рабочей директории
WORKDIR /var/www/html

# Запуск Supervisord
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
