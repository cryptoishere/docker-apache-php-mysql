ARG apache_version
ARG certs
ARG default_apache_conf
ARG ssl_apache_conf

FROM httpd:$apache_version

ARG certs=$certs
ARG default_apache_conf=$default_apache_conf
ARG ssl_apache_conf=$ssl_apache_conf

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
      curl nano

COPY $certs /usr/local/apache2/conf/
COPY $default_apache_conf /usr/local/apache2/conf/httpd.conf
# COPY $ssl_apache_conf /usr/local/apache2/conf/ssl-default.conf
