FROM php:fpm-buster

COPY ./docker/php/php.ini /usr/local/etc/php/

RUN apt-get update \
  && apt-get -y install git zip unzip vim

RUN docker-php-ext-install pdo_mysql

RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

COPY ./app/. /var/www/html
WORKDIR /var/www/html

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get install -y nodejs

RUN if [ -f "./composer.json" ]; then \
      composer install; \
    fi

CMD ["php-fpm"]