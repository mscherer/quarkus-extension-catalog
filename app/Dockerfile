FROM quay.io/app-sre/nginx:stable-alpine
ARG REGISTRY_VERSION

LABEL name="quarkus-registry" \
      vendor="Red Hat" \
      summary="Nginx container to host the Quarkus Extension Registry" \
      description="Nginx container to host the Quarkus Extension Registry" \
      author="Quarkus Team <quarkus-dev@googlegroups.com>" \
      maintainer="Quarkus Team <quarkus-dev@googlegroups.com>"

ENV LANG=en_US.utf8

RUN rm /etc/nginx/nginx.conf /etc/nginx/conf.d/default.conf
ADD nginx.conf /etc/nginx/nginx.conf.tmp
RUN envsubst '$REGISTRY_VERSION' < /etc/nginx/nginx.conf.tmp > /etc/nginx/nginx.conf\
    && rm /etc/nginx/nginx.conf.tmp \
    && chmod -R 777 /var/log/nginx /var/cache/nginx/ /var/run/ \
    && chmod 644 /etc/nginx/*

COPY ./json/ /usr/share/nginx/html/