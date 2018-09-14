FROM phpdockerio/php56-cli

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
    cron \
    rsyslog \
    mysql-client \
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

# CRON
RUN set -ex \
    && mkfifo --mode 0666 /var/log/cron.log \
    && sed --regexp-extended --in-place \
    's/^session\s+required\s+pam_loginuid.so$/session optional pam_loginuid.so/' \
    /etc/pam.d/cron
ADD default.cron /etc/cron.d/default
RUN chmod 0644 /etc/cron.d/default
RUN touch /var/log/cron.log

RUN usermod -u 1000 www-data

CMD cron && tail -f /var/log/cron.log
