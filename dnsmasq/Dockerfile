FROM alpine:3.19

ARG VERSION

LABEL maintainer="Neal Peng<pengshp@gmail.com>" \
    version="${VERSION}" \
    url="https://dnsmasq.org/docs/dnsmasq-man.html" \
    desc="A lightweight DHCP and caching DNS server."

RUN  set -xe \
    && sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk add --no-cache dnsmasq
VOLUME [ "/etc/dnsmasq.d" ]

EXPOSE 53/udp

CMD ["--no-daemon","--conf-file=/etc/dnsmasq.conf"]
ENTRYPOINT ["dnsmasq"]
