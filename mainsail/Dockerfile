# builder stage to download static files
FROM busybox AS builder

ARG MAINSAIL_VER="https://github.com/meteyou/mainsail/releases/download/v0.2.6/mainsail-beta-0.2.6.zip"

RUN mkdir /mainsail
WORKDIR /mainsail

RUN wget -q -O mainsail.zip ${MAINSAIL_VER} && \
    unzip mainsail.zip

# nginx
FROM nginx:stable-alpine

COPY nginx_conf.d/* /etc/conf.d/
COPY  --from=builder /mainsail /usr/share/mainsail

