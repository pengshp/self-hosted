FROM alpine:3.20

ARG VERSION

LABEL org.opencontainers.image.author="pengshp <pengshp@gmail.com>" \
    org.opencontainers.image.version="${VERSION}" \
    org.opencontainers.image.description="A tool for securing communications between a client and a DNS resolver." \
    org.opencontainers.image.url="https://github.com/jedisct1/dnscrypt-proxy"


RUN set -xe \
    && sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --no-cache dnscrypt-proxy

VOLUME [ "/etc/dnscrypt-proxy" ]
USER dnscrypt

EXPOSE 53/tcp 53/udp

CMD ["-config","/etc/dnscrypt-proxy/dnscrypt-proxy.toml"]
ENTRYPOINT ["dnscrypt-proxy"]
