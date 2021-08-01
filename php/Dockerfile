FROM php:7.3-apache

# Download script to install PHP extensions and dependencies
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
      curl git zip unzip software-properties-common vim wget \
      && install-php-extensions \
      bcmath bz2 calendar exif gd intl ldap \
      mysqli pdo_mysql soap xsl zip sockets

# Update image
# RUN apt-get update && apt-get install -y

# Install modules
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

COPY ./proxy/certs/*.pem /etc/apache2/ssl/
COPY ./000-default.conf /etc/apache2/sites-enabled/000-default.conf
COPY ./default-ssl.conf /etc/apache2/sites-available/default-ssl.conf

# EXPOSE 80
# EXPOSE 443
