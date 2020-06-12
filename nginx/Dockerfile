FROM nginx:1.17.5-alpine

ADD ./*.conf /etc/nginx/conf.d/

RUN  sed -i -e 's/*.log/*\/*.log/g' /etc/logrotate.d/nginx \
  && sed -i -e 's/rotate 52/rotate 15\n\tdateext \n\tdateformat.%Y-%m-%d.log/g' /etc/logrotate.d/nginx 

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

WORKDIR /etc/nginx

CMD ["nginx"]
