FROM ubuntu:14.04

#install utilities tools
RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y unzip
RUN apt-get install -y curl

RUN apt-get install -y python-software-properties software-properties-common

# Update software list, install php-nginx & clear cache
RUN locale-gen en_US.UTF-8 && \
    export LANG=en_US.UTF-8 && \
    add-apt-repository -y ppa:ondrej/php && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --force-yes nginx \
    php5.6 php5.6-zip php5.6-fpm php5.6-cli php5.6-mysql php5.6-mcrypt php5.6-xml\
    php5.6-curl && \
    php5.6-xdebug && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
           /tmp/* \
           /var/tmp/*

COPY ./default                                          /etc/nginx/sites-enabled/default

# Configure nginx
RUN echo "daemon off;" >>                                               /etc/nginx/nginx.conf
RUN sed -i "s/sendfile on/sendfile off/"                                /etc/nginx/nginx.conf
RUN mkdir -p                                                            /var/www/html

# Workdir
WORKDIR /var/www/html



# Configure PHP
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/"                  /etc/php/5.6/fpm/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = America\/Argentina\/Buenos_Aires/"        /etc/php/5.6/fpm/php.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g"                 /etc/php/5.6/fpm/php-fpm.conf
##Updated for PHP 5.6
RUN sed -i "s/pid =.*/pid = \/var\/run\/php-fpm.pid/"                   /etc/php/5.6/fpm/php-fpm.conf
RUN sed -i "s/listen =.*sock/listen = \/var\/run\/php-fpm.sock/"        /etc/php/5.6/fpm/pool.d/www.conf
##
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/"                  /etc/php/5.6/cli/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = America\/Argentina\/Buenos_Aires/"        /etc/php/5.6/cli/php.ini
RUN phpenmod -v 5.6 mcrypt
RUN phpenmod -v 5.6 xdebug
RUN phpenmod -v 5.6 zip

#install composer
RUN curl -O https://getcomposer.org/composer.phar
RUN mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

RUN php-fpm5.6 -D
CMD service nginx start

