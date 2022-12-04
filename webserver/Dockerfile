ARG PHP_VERSION=${PHP_VERSION:-8.1}
FROM php:${PHP_VERSION}-fpm-alpine

RUN apk -U upgrade
RUN apk add --no-cache rsync nodejs npm gcc freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev $PHPIZE_DEPS openssl-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install opcache gd pdo_mysql zip
RUN docker-php-ext-enable opcache gd zip
RUN wget https://getcomposer.org/download/latest-stable/composer.phar
RUN chmod a+x composer.phar
RUN mv composer.phar /usr/local/bin/composer
RUN npm install --global yarn

ARG ENV=${ENV:-production}

RUN if [ "$ENV" = "dev" ] ; then pecl install xdebug && docker-php-ext-enable xdebug; fi

CMD ["php-fpm"]