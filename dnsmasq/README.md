dnsmasq is free software providing Domain Name System (DNS) caching, a Dynamic Host Configuration Protocol (DHCP) server.

PORT 53/udp

# Usage

## docker compose

```yaml
$ vim compose.yaml
services:
  dnsmasq:
    image: pengshp/dnsmasq:latest
    container_name: dnsmasq-c
    volumes:
      - type: bind
        source: ./config
        target: /etc/dnsmasq.d/
    network_mode: host
    restart: unless-stopped
    cap_add:
      - NET_ADMIN
```

## Start container

```shell
$ docker compose up -d
$ docker compose logs -f
```

## Add customized configuration

```shell
$ vim ./config/dns.conf
# global.conf

# 不要解析 /etc/resolv.conf
no-resolv

# 缓存的记录数，默认是150，调大一点，免得每次都要花时间重新询问
cache-size=1500

# 这个可以配置多个上游服务器
server=114.114.114.114
server=223.5.5.5
server=1.0.0.1
# 表示同时查询上游dns，哪个先返回就用哪一个
all-servers
```

## Restart container

```shell
$ docker compose restart
```

## DNS query

```shell
$ dig +short @127.0.0.1 jd.com
111.13.149.108
211.144.24.218
211.144.27.126
118.193.98.63
```
