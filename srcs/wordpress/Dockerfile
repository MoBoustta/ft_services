FROM	alpine:3.11

RUN     apk update
RUN     apk add nginx
RUN     apk add supervisor
RUN		apk add wget php7 php7-fpm php7-mysqli php7-mbstring php7-json php7-session
RUN		mkdir -p /usr/share/webapps/ && cd /usr/share/webapps/
RUN		wget https://wordpress.org/wordpress-5.6.tar.gz && tar -xzvf wordpress-5.6.tar.gz && rm wordpress-5.6.tar.gz
RUN		mkdir -p /var/www && mv /wordpress /var/www/
RUN     apk add telegraf --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted --no-cache
RUN     mkdir /etc/nginx/ssl
RUN     chown -R root:root /etc/nginx/ssl # set the user and group of $file to root.
RUN     chmod 600 /etc/nginx/ssl   # The owner has full read and write access to the file, while no other user can.
RUN     mkdir -p /etc/telegraf     # Needed for telegraf to be run.

COPY    srcs/telegraf.conf        /etc/telegraf/
COPY	srcs/wp-config.php			/var/www/wordpress/
COPY	srcs/start.sh				/
COPY    srcs/supervisord.conf       /etc/supervisord.conf
COPY    srcs/nginx.conf             /etc/nginx/nginx.conf
COPY    srcs/default.conf           /etc/nginx/conf.d/
COPY    srcs/localhost.key          /etc/nginx/ssl
COPY    srcs/localhost.crt          /etc/nginx/ssl
COPY    srcs/health.sh              /
EXPOSE	5050

RUN mkdir -p /run/nginx

CMD sh start.sh
