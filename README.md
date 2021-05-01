# ssr-server

由于学校带宽限制，宿舍内是千兆的网，但是学生账号只能跑10Mbps，算下来平时也就1M左右的网速，就连看视频都卡。我们只好通过ssr代理到部门的服务器上，实现加速。

前不久部门更换服务器，于是我们使用了祖传的`https://github.com/shadowsocksr/shadowsocksr`ssr安装脚本，但是因为DNS污染以及各种墙的原因使得我们实在部署不了，最后通过更改脚本的方式成功部署。

方法其实非常简单，将所有需要下载的文件下载好之后，把脚本里边的`wget`改成`cp`即可。

顺便，把一些文字给汉化了。

## 如何使用

理论上，脚本部署好之后，之后是不需要再管的，但是为了保险起见还是把一些命令说明吧。

- 安装

```shell
chmod +x shadowsocksR.sh
sudo ./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
```

- 卸载

```shell
sudo ./shadowsocksR.sh uninstall
```

- 命令

```shell
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status
```

- 文件路径

```shell
配置文件路径：/etc/shadowsocks.json
日志文件路径：/var/log/shadowsocks.log
代码安装目录：/usr/local/shadowsocks
```

- 多用户

```shell
{
"server":"0.0.0.0",
"server_ipv6": "[::]",
"local_address":"127.0.0.1",
"local_port":1080,
"port_password":{
    "8989":"password1",
    "8990":"password2",
    "8991":"password3"
},
"timeout":300,
"method":"aes-256-cfb",
"protocol": "origin",
"protocol_param": "",
"obfs": "plain",
"obfs_param": "",
"redirect": "",
"dns_ipv6": false,
"fast_open": false,
"workers": 1
}
```

