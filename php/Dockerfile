ARG php_version
ARG certs
ARG default_apache_conf
ARG ssl_apache_conf

FROM php:$php_version

ARG certs=$certs
ARG default_apache_conf=$default_apache_conf
ARG ssl_apache_conf=$ssl_apache_conf

# Download script to install PHP extensions and dependencies
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
      curl git zip unzip software-properties-common vim wget \
      && install-php-extensions \
      bcmath bz2 calendar exif gd intl ldap \
      mysqli pdo_mysql soap xsl zip sockets

# Install apache modules
RUN a2enmod ssl && a2enmod rewrite && a2enmod headers && a2enmod expires

# Install xDebug
# RUN pecl install xdebug-2.9.6
RUN pecl install xdebug

# Add php.ini
# RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
ADD ./custom_php.ini /usr/local/etc/php/php.ini

# Install Composer
RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet


COPY $certs /etc/apache2/ssl/
COPY $default_apache_conf /etc/apache2/sites-enabled/000-default.conf
COPY $ssl_apache_conf /etc/apache2/sites-enabled/ssl-default.conf
