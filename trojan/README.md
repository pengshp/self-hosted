Trojan features multiple protocols over TLS to avoid both active/passive detections and ISP QoS limitations.

Trojan is not a fixed program or protocol. It's an idea, an idea that imitating the most common service, to an extent that it behaves identically, could help you get across the Great FireWall permanently, without being identified ever. We are the GreatER Fire; we ship Trojan Horses.
An online documentation can be found [here](https://trojan-gfw.github.io/trojan/).

## Usage

### VPS Server

```bash
~$ docker pull pengshp/trojan:v1.16
~$ mkdir -p ~/docker/trojan/config
~$ cd ~/docker/trojan
~$ vim compose.yaml
---
services:
  trojan:
    image: pengshp/trojan:latest
    container_name: trojan-c
    volumes:
      - ./config:/config
    depends_on:
      - web
    network_mode: host
    restart: unless-stopped

  web:
    image: nginx:stable-alpine
    container_name: nginx-web
    volumes:
      - ./html:/usr/share/nginx/html:ro
    network_mode: host
    restart: unless-stopped
    environment:
      - NGINX_HOST=<tj.xxxx.com>
      - NGINX_PORT=80
```

```yaml
~$ vim config/config.json
{
    "run_type": "server",
    "local_addr": "0.0.0.0",
    "local_port": 443,
    "remote_addr": "127.0.0.1",
    "remote_port": 80,
    "password": [
        "password1",
        "password2"
    ],
    "log_level": 1,
    "ssl": {
        "cert": "/config/certificate.crt",
        "key": "/config/private.key",
        "key_password": "",
        "cipher_tls13": "TLS_AES_128_GCM_SHA256:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_256_GCM_SHA384",
        "prefer_server_cipher": true,
        "alpn": [
            "http/1.1",
            "h2"
        ],
        "alpn_port_override": {
            "h2": 81
        },
        "reuse_session": true,
        "session_ticket": false,
        "session_timeout": 600,
        "plain_http_response": "",
        "curves": "",
        "dhparam": ""
    },
    "tcp": {
        "prefer_ipv4": false,
        "no_delay": true,
        "keep_alive": true,
        "reuse_port": false,
        "fast_open": true,
        "fast_open_qlen": 20
    },
    "mysql": {
        "enabled": false,
        "server_addr": "127.0.0.1",
        "server_port": 3306,
        "database": "trojan",
        "username": "trojan",
        "password": "",
        "key": "",
        "cert": "",
        "ca": ""
    }
}
```

Up

```sh
~$ docker compose up -d
~$ docker compose logs -f
```

### LAN Client

compose.yaml

```yaml
---
services:
  trojan:
    image: pengshp/trojan:latest
    container_name: trojan-c
    volumes:
      - ./config:/config
    network_mode: host
    restart: unless-stopped
```

```json
~$ vim config/config.json
{
    "run_type": "client",
    "local_addr": "0.0.0.0",
    "local_port": 1080,
    "remote_addr": "example.com",
    "remote_port": 443,
    "password": [
        "password1"
    ],
    "log_level": 1,
    "ssl": {
        "verify": true,
        "verify_hostname": true,
        "cert": "",
        "cipher_tls13": "TLS_AES_128_GCM_SHA256:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_256_GCM_SHA384",
        "sni": "",
        "alpn": [
            "h2",
            "http/1.1"
        ],
        "reuse_session": true,
        "session_ticket": false,
        "curves": ""
    },
    "tcp": {
        "no_delay": true,
        "keep_alive": true,
        "reuse_port": false,
        "fast_open": true,
        "fast_open_qlen": 20
    }
}
```

Up

```bash
~$ docker compose up -d
~$ docker compose logs -f
```

<https://trojan-gfw.github.io/trojan/config>
