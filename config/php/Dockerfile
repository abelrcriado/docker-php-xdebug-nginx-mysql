FROM php:7.2-fpm
WORKDIR "/source"

RUN apt-get update \
    && apt-get -y install git unzip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get update \
    && apt-get install -y libicu-dev zlib1g-dev libpng-dev libmemcached-dev\
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \
    && docker-php-ext-install intl zip mysqli pdo pdo_mysql gd opcache

RUN cd /tmp \
    && git clone https://github.com/xdebug/xdebug.git \
    && cd xdebug \
    && ./rebuild.sh \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini

RUN echo 'alias ll="ls -l"' >> ~/.bashrc
RUN echo 'alias sf="php bin/console"' >> ~/.bashrc