FROM nginx:1.19-alpine

WORKDIR /app

RUN apk update && apk add --no-cache sudo

RUN apk update && apk add --no-cache fcgiwrap

RUN adduser -D testuser \
    && echo "testuser ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN apk add --no-cache openssl

RUN mkdir /etc/nginx/ssl

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt -subj "/C=UA/ST=Kyiv/L=Kyiv/O=MyOrg/OU=MyOrg/CN=beloversecured.net"

COPY conf/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./crush_script.sh .

COPY ./shutdown_script.sh .

COPY ./404.html /usr/share/nginx/html

EXPOSE 80 443 22

CMD [ "nginx", "-g", "daemon off;" ]