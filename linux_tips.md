# Linux Tips

### proxy

1. download shadowsocks
```sh
$ pip3 install shadowsocks
```
2. make a config file, and launch with sslocal
config.json example
```json
{
    "server": "xxxx.com",
    "server_port": 52239,
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "password": "passowrd",
    "timeout": 600,
    "method": "aes-256-cfb",
    "fast_open": false
}
```
and
```sh
$ sslocal -c /path/to/config.json
```
3. add to rc.local
```sh
$ sudo echo "sudo /path/to/sslocal -c /path/to/config.json > /path/to/ss.log &" >> /etc/rc.local
```
4. set polipo
```sh
$ apt install polipo
```
and echo these to ``/etc/polipo/config`
```
logSyslog = true
logFile = /var/log/polipo/polipo.log

proxyAddress = "0.0.0.0"

socksParentProxy = "localhost:port"
socksProxyType = socks5
proxyPort = 8123

chunkHighMark = 50331648
objectHighMark = 16384

serverMaxSlots = 64
serverSlots = 16
serverSlots1 = 32
```
and
```sh
$ /etc/init.d/polipo restart
```

5. echo to .bashrc(or .zshrc)
```sh
$ echo "export http_proxy='http://localhost:8123'"
$ echo "export https_proxy='https://localhost:8123'"
$ echo "export no_proxy='localhost,127.0.0.1,192.168.*,.localdomain.com'"
```

### .bashrc

1. alias
```sh
$ alias ll="LC_COLLATE=C ls -alhG"
$ alias
```

### systemctl
