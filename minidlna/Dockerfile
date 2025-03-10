FROM alpine:3.19

ARG VERSION

LABEL org.opencontainers.image.author="pengshp <pengshp@gamil.com>" \
    org.opencontainers.image.description="a simple media server software, with the aim of being fully compliant with DLNA/UPnP-AV clients." \
    org.opencontainers.image.url="https://sourceforge.net/projects/minidlna/" \
    org.opencontainers.image.version="${VERSION}"

RUN set -xe  \
    && sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --no-cache minidlna \
    && mkdir -p /etc/minidlna \
    && mv /etc/minidlna.conf /etc/minidlna

VOLUME [ "/etc/minidlna","/media" ]

WORKDIR ["/media"]

EXPOSE 1900/udp 8200/tcp

CMD ["-d","-f","/etc/minidlna/minidlna.conf"]
ENTRYPOINT ["minidlnad"]


