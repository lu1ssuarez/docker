# docker build -t luewell/laravel:5.5 .
FROM ubuntu:16.04

MAINTAINER Luis Enrique Suárez <https://luewell.com>

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -y \
    && apt dist-upgrade -y \
    && apt install -y curl \
    && apt install -y software-properties-common

RUN apt install -y apache2

RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php -y \
    && apt update -y

RUN apt install -y php7.1 libapache2-mod-php7.1 \
    && service apache2 restart

RUN apt install -y openssl \
    && apt install -y php7.1-pdo php7.1-pgsql php7.1-mysql php7.1-sqlite3 \
    && apt install -y php7.1-mbstring \
    && apt install -y php7.1-xml \
    && apt install -y mcrypt php7.1-mcrypt zip php7.1-zip php7.1-curl php7.1-gettext php7.1-gd php7.1-imagick

RUN phpenmod mcrypt \
    && phpenmod mbstring \
    && a2enmod rewrite \
    && a2enmod headers \
    && a2enmod ssl \
    && service apache2 restart

RUN echo "<?php phpinfo();" | tee /var/www/html/info.php

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt install -y nodejs

EXPOSE 80 443

CMD apachectl -D FOREGROUND
