<https://github.com/DNSCrypt/dnscrypt-proxy>

dnscrypt-proxy VERSION v2.1.5

### Usage
#### Docker Container
```sh
# Docker
$ docker run -d --name=dnscrypt --restart=on-failure -p 53:53/udp -p 53:53/tcp -v dns:/etc/dnscrypt-proxy pengshp/dnscrypt-proxy:2.1.5
```

or

#### docker-compose
```shell
$ mkdir config
$ wget -O ./config/dnscrypt-proxy.toml https://github.com/DNSCrypt/dnscrypt-proxy/raw/master/dnscrypt-proxy/example-dnscrypt-proxy.toml
```

docker-compose.yml
```yaml
version: "3.9"
services:

  dnscrypt-proxy:
    image: pengshp/dnscrypt-proxy:2.1.5
    container_name: dnscrypt-proxy
    ports:
      - "53:53/tcp"
      - "53:53/udp"
    volumes:
      #- ./config/dnscrypt-proxy.toml:/config/dnscrypt-proxy.toml
      - ./config:/etc/dnscrypt-proxy
    network_mode: bridge
    restart: on-failure
```

start a contanier
```shell
$ docker compose up -d

# log
$ docker compose logs -f
```

### LAN DNS Lookup
```sh
$ dig @192.168.1.10 +short bing.com
13.107.21.200
204.79.197.200
```
Have a good day!


