FROM ubuntu:18.04

ENV TZ=Asia/Seoul
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -y -qq update \ 
    && apt-get -y -qq install php php-fpm php-mysql mcrypt php-gd curl php-curl php-mbstring sendmail supervisor \
    && mkdir /run/php \
    && apt-get clean && rm -rf /tmp/* /var/tmp/*

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN sed -i -e 's/listen = \/run\/php\/php7.2-fpm.sock/listen = 0.0.0.0:9000/g' /etc/php/7.2/fpm/pool.d/www.conf \
    && sed -i -e 's/;security.limit_extensions = .php .php3 .php4 .php5 .php7/security.limit_extensions = .htm .html .php .php3 .php4 .php5 .php7/g' /etc/php/7.2/fpm/pool.d/www.conf \
    && sed -i -e 's/;daemonize = yes/daemonize = no/g' /etc/php/7.2/fpm/php-fpm.conf

WORKDIR /home/www

EXPOSE 9000

CMD ["/usr/bin/supervisord"]
