FROM alpine:latest
LABEL maintainer="pengshp<pengshp@gmail.com>" \
    version="1.0" \
    description="youtube-dl for Docker"

RUN set -xe \
    && sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
ENV TZ='Asia/Shanghai'
RUN set -xe \
    && apk add --no-cache python3 youtube_dl ffmpeg


VOLUME /workdir

WORKDIR /workdir

CMD ["-f","best"]
ENTRYPOINT ["youtube-dl"]