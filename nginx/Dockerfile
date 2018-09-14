FROM nginx:latest

MAINTAINER vitams

ADD nginx.conf /etc/nginx/
ADD upstream.conf /etc/nginx/conf.d/
ADD default.conf /etc/nginx/sites-available/

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80 443