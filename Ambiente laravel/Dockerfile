FROM php:7.2-apache

LABEL maintainer="geovanne queiroz"

# install pre-requisites
RUN apt-get update

RUN apt-get install -y \
    git \
    zip \
    curl \
    sudo \
    unzip \
    libicu-dev \
    libbz2-dev \
    libpng-dev \
    libjpeg-dev \
    libmcrypt-dev \
    libreadline-dev \
    libfreetype6-dev \
    g++
#install extentions php
RUN docker-php-ext-install \
    bz2 \
    intl \
    iconv \
    bcmath \
    opcache \
    calendar \
    mbstring \
    pdo_mysql \
    zip 

# install composer
RUN curl -s https://getcomposer.org/installer | php && \
        mv composer.phar /usr/bin/composer

# import project
#COPY ./ /var/www/html/
RUN chown -R www-data:www-data /var/www/html \
        && chmod -R 755 /var/www/html
RUN a2enmod rewrite

# configure apache
COPY default /etc/apache2/sites-enabled/000-default.conf
#RUN a2ensite 000-default.conf && a2enmod rewrit


# set entrypoint
COPY entrypoint /usr/bin/
RUN chmod +x /usr/bin/entrypoint

EXPOSE 80

ENTRYPOINT [ "entrypoint"  ]

