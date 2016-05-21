FROM nginx:latest
MAINTAINER Christopher Smith <chris@x86-64.jp>

# Change this if you're in another timezone
ENV TZ=Asia/Tokyo

RUN apt-get update && apt-get dist-upgrade -y \
&& rm -rf /var/lib/apt/lists/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY trac.conf /etc/nginx/conf.d/trac.conf
COPY htpasswd /etc/nginx/trac.passwd
