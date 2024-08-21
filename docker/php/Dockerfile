FROM php:8.3-fpm

RUN apt-get update && apt-get install -y \
  tzdata \
  build-essential \
  libpng-dev \
  libjpeg62-turbo-dev \
  libfreetype6-dev \
  libwebp-dev \
  locales \
  zip \
  vim \
  unzip \
  git \
  curl \
  supervisor \
  cron \
  libxml2-dev

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql \
  pcntl \
  opcache \
  soap \
  bcmath

RUN docker-php-ext-configure gd \
  --with-freetype=/usr/include/ \
  --with-jpeg=/usr/include/ \
  --with-webp=/usr/include/
RUN docker-php-ext-install gd

ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV TZ America/Sao_Paulo
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer
WORKDIR /var/www/html
RUN groupadd -g 1000 user
RUN useradd -u 1000 -g user user
USER user
