FROM alpine:latest
RUN apk update
RUN apk add vsftpd openrc supervisor openssl
RUN openssl req -x509 -nodes -days 365 \
    -newkey rsa:2048 -subj "/C=SP/ST=Spain/L=Madrid/O=42/CN=127.0.0.1" \
	-keyout /etc/ssl/private/vsftpd.key \
	-out /etc/ssl/certs/vsftpd.crt

# We create a new user
RUN { echo "user"; echo "user"; } | adduser user

COPY srcs/vsftpd.conf /etc/vsftpd.conf
COPY srcs/run.sh .
COPY srcs/supervisord.conf /etc/supervisord.conf

EXPOSE 21 21000

RUN chmod +x run.sh

CMD sh run.sh