FROM alpine:3.6
MAINTAINER Mark Myers <marcusmyers@gmail.com>

ENV VAULT_VERSION=0.8.1

RUN apk add --update unzip \
      bash \
      ca-certificates \
    && rm -rf /var/cache/apk/*

ADD https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip /tmp
RUN cd /tmp \
    && unzip vault_${VAULT_VERSION}_linux_amd64.zip \
    && mv vault /usr/local/bin/vault \
    && rm -f vault_${VAULT_VERSION}_linux_amd65.zip

RUN mkdir -p /vault/logs && \
    mkdir -p /vault/data && \
    mkdir -p /vault/config

EXPOSE 8200

VOLUME ["/vault/logs"]
VOLUME ["/vault/data"]

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["server"]
