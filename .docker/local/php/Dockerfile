FROM php:8.0-fpm-buster

COPY ./php.ini /usr/local/etc/php/php.ini
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY . /app
WORKDIR /app

RUN apt-get update && apt-get install -y  \
  libzip-dev \
  libpng-dev \
  git \
  bash \
  libicu-dev \
  libonig5 \
  # nodejs \
  nodejs npm \
  # yarn \
  patch &&\
  rm -rf /var/lib/apt/lists/* &&\
  git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis && \
  # Install XDebug
  pecl install xdebug && \
  docker-php-ext-enable xdebug && \
  # Install PHP Extension
  docker-php-ext-install \
  pdo_mysql \
  bcmath \
  zip \
  opcache \
  gd \
  intl \
  redis 

RUN curl https://deb.nodesource.com/setup_12.x | bash
RUN curl https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get install -y nodejs \
yarn


WORKDIR /app
