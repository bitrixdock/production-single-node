FROM phpdockerio/php56-fpm

MAINTAINER vitams

ADD local /etc/apt/apt.conf.d/local

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
    php5-memcached \
    php5-memcache \
    php5-mysql \
    php5-intl \
    php5-interbase \
    php5-gd \
    php5-imagick \
    php5-mcrypt \
    msmtp \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

ADD ./php.ini /etc/php5/fpm/conf.d/90-php.ini
ADD ./php.ini /etc/php5/cli/conf.d/90-php.ini

# MSMTP
ADD msmtprc /etc/msmtprc
RUN chmod 0600 /etc/msmtprc && \
    chown www-data:www-data /etc/msmtprc && \
    mkdir -p /var/log/msmtp/msmtp.log && \
    touch /var/log/msmtp/msmtp.log && \
    chmod 775 /var/log/msmtp/msmtp.log && \
    chown www-data:www-data /var/log/msmtp/msmtp.log

RUN usermod -u 1000 www-data

EXPOSE 9000