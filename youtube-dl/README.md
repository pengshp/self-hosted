# Usage
```shell
$ docker pull pengshp/youtube-dl
$ docker run --rm -v $(pwd)/dl:/workdir pengshp/youtube-dl:latest URL
```

# Use alias
```shell
$ alias dl='docker run --rm -v $(pwd)/dl:/workdir pengshp/youtube-dl:latest'
$ dl --help
```
# eg
```shell
~$ dl https://www.bilibili.com/video/BV1by4y117t5
[BiliBili] 1by4y117t5: Downloading webpage
[BiliBili] 1by4y117t5: Downloading video info page
[download] Destination: 【小诺】学姐叫你一起来天台跳个舞-1by4y117t5.flv
[download] 100% of 24.15MiB in 00:27.24KiB/s ETA 00:00
~$ ls dl
【小诺】学姐叫你一起来天台跳个舞-1by4y117t5.flv
```

# Use a proxy
```shell
$ dl --proxy socks5://127.0.0.1:1090 URL
```