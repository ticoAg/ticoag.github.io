# Ubuntu

## 安装`shadowsocks-libev`

```sh
sudo apt-get update
sudo apt-get install shadowsocks-libev

# 确认服务已运行
sudo systemctl status shadowsocks-libev
```

## 配置域名和 SSL 证书

```sh
# 配置域名和 SSL 证书
sudo apt install certbot -y && pip install certbot -U
sudo certbot certonly --standalone -d yourdomain.com
sudo certbot renew --dry-run    # 90天到期 自动续期
```

## 安装`simple-obfs`, 修改插件配置

```sh
# 编辑 shadowsocks 配置文件，将 plugin_opts 修改
"plugin_opts": "obfs=tls;obfs-host=yourdomain.com;cert=/etc/letsencrypt/live/yourdomain.com/fullchain.pem;key=/etc/letsencrypt/live/yourdomain.com/privkey.pem"
# 重启ss-libev服务
sudo systemctl restart shadowsocks-libev
# 安装simple-obfs
apt-get install --no-install-recommends build-essential autoconf libtool libssl-dev libpcre3-dev libev-dev asciidoc xmlto automake -y
git clone https://github.com/shadowsocks/simple-obfs.git && cd simple-obfs && git submodule update --init --recursive
./autogen.sh && ./configure && make && make install
```

### 编辑配置文件 ss-libev

```sh
sudo vim /etc/shadowsocks-libev/multi-config.json
```

```json
{
    "server": ["::0", "0.0.0.0"],
    "mode": "tcp_and_udp",
    "port_password": {
        "port": "password"
    },
    "timeout": 86400,
    "method": "chacha20-ietf-poly1305",
    "plugin": "obfs-server",
    "plugin_opts": "obfs=tls;obfs-host=yourdomain.com;cert=/etc/letsencrypt/live/yourdomain.com/fullchain.pem;key=/etc/letsencrypt/live/yourdomain.com/privkey.pem"
}
```

## 使用 tmux 启动服务

```sh
tmux new -s ss-manager

ss-manager -c /etc/shadowsocks-libev/multi-config.json
```

## 配置 clash 节点

```yaml
proxies:
    - name: your-node-name
      type: ss
      server: yourdomain.com
      port: your-port
      cipher: chacha20-ietf-poly1305
      password: your-password
      plugin: obfs
      plugin-opts:
          mode: tls
          host: yourdomain.com
```



---
comments: true  #默认不开启评论
---
