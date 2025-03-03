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

# start composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# end composer

RUN groupadd --force -g 1000 www-data

# COPY . /var/www/html

# RUN composer install
# COPY --chown=www:www . /var/www

# RUN chown -R 775 /var/www/html
# RUN chmod -R 775 /var/www/html

EXPOSE 9000

CMD ["php-fpm"]
