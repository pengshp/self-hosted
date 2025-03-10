FROM alpine:3.19

ARG VERSION

LABEL maintainer="Neal <pengshp@gamil.com>" \
    version="${VERSION}-r6" \
    description="A simple HTTP Request & Response Service." \
    url="http://httpbin.org"

RUN set -xe \
    && sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --no-cache py3-httpbin py3-gunicorn

EXPOSE 80/tcp

CMD [ "gunicorn", "--bind", "0.0.0.0:80", "httpbin:app" ]
