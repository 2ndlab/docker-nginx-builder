ARG NGINX_VERSION=1.19.8

FROM nginx:${NGINX_VERSION}-alpine

RUN \
        apk add --no-cache --virtual .nginx-deps \
            gcc \
            libc-dev \
            make \
            openssl-dev \
            pcre-dev \
            zlib-dev \
            linux-headers \
            libxslt-dev \
            gd-dev \
            geoip-dev \
        && \
        apk add --no-cache --virtual .utils-deps \
            curl

RUN \
        curl -fSL "http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz" -o nginx.tar.gz \
        && mkdir -p /usr/src/ && tar -zxC /usr/src -f nginx.tar.gz \
        && cd /usr/src && mv /usr/src/nginx-${NGINX_VERSION} /usr/src/nginx 

RUN \
        CONFARGS=$(nginx -V 2>&1 | sed -n -e 's/^.*arguments: //p') \
        CONFARGS=${CONFARGS/-Os -fomit-frame-pointer -g/-Os} \
        && export CONFARGS=$CONFARGS; \
        && echo $CONFARGS