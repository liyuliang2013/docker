FROM ubuntu:14.04

RUN mkdir /app
WORKDIR /app

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties curl
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install --yes --force-yes php5.6

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

RUN mkdir -p /usr/local/bin
RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
RUN chmod a+x /usr/local/bin/symfony

VOLUME ["/app"]
