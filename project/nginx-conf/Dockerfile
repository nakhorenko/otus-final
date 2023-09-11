FROM nginx:1.24.0-alpine
# устанавливаем в контейнер openssl
RUN apk update && apk add openssl
RUN rm /etc/nginx/conf.d/default.conf 
# генерим сертификат 
RUN openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048 &&\
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/self.key -out /etc/ssl/certs/self.crt \
    -subj "/C=RU/ST=Moscow/O=Otus Code/OU=Org/CN=stud.otus"
# пробрасываем конфиг nginx и ssl-params
COPY nginx.conf /etc/nginx/conf.d 
COPY ssl-params.conf /etc/nginx/ssl-params.conf
