FROM php:8.3-fpm

ARG NODE_VERSION=18

WORKDIR /var/www/html

RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    jpegoptim optipng pngquant gifsicle \
    git \
    curl \
    libpq-dev \
    libonig-dev \
    libzip-dev \
    libxml2-dev \
    zip \
    unzip \
    iputils-ping

RUN docker-php-ext-install pdo_pgsql mbstring exif pcntl bcmath gd

# start node
RUN curl -fsSL https://deb.nodesource.com/setup_$NODE_VERSION.x | bash - && \
    apt-get install -y nodejs

# end node
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN groupadd --force -g 1000 www-data


# start project
COPY . /var/www/html

COPY ./docker/production/php/8.3/php.ini /usr/local/etc/php/conf.d/php.ini

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN npm install

RUN npm run prod

RUN composer install --no-dev --optimize-autoloader

RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
# end project

EXPOSE 9000

CMD ["php-fpm"]
