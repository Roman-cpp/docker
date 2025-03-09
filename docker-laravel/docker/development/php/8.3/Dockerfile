FROM php:8.3-fpm

ARG NODE_VERSION=18

ARG WWWUSER
ARG WWWGROUP

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

#start settings user

RUN groupadd -g $WWWGROUP app-user && \
    useradd -u $WWWUSER -g $WWWGROUP -m app-user

#end settings user

# start node
RUN curl -fsSL https://deb.nodesource.com/setup_$NODE_VERSION.x | bash - && \
    apt-get install -y nodejs

# end node
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# start composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
# end composer

EXPOSE 9000

CMD ["php-fpm"]
