# beego 通过acme.sh 使用 https


beego 通过 acme.sh 使用 https

## 安装acms.sh

```
curl  https://get.acme.sh | sh
```

## 生成证书

如果使用的是 beego 框架，需添加可访问的静态文件目录：

```
//acme.sh 自动验证网站目录，不使用https可以忽略
beego.SetStaticPath("/.well-known", ".well-known")
```

```
acme.sh  --issue  -d haokiu.com -d www.haokiu.com  --webroot  /usr/local/pixiublog/
```

## 设置pixiublog开机启动

### 1. 编写开机启动脚本

`vim /usr/lib/systemd/system/pixiublog.service`

```
[Unit]
Description=The pixiublog Process Manager
After=syslog.target network.target

[Service]
Type=forking
ExecStart=sh /usr/local/pixiublog/start.sh
ExecReload=/bin/kill -USR2 $MAINPID
ExecStop=/bin/kill -SIGINT $MAINPID

[Install]
WantedBy=multi-user.target
```

### 2. 设置开机启动

```
systemctl enable pixiublog
```


## 安装证书

```
acme.sh --install-cert -d haokiu.com \
--cert-file      /home/blog/cert/cert.pem  \
--key-file       /home/blog/cert/key.pem  \
--fullchain-file /home/blog/cert/fullchain.pem \
--reloadcmd     "systemctl restart pixiublog"
```

## beego app.conf 配置

```
EnableHTTPS = true
HTTPSPort = 443
HTTPSCertFile = "/home/blog/cert/fullchain.pem"
HTTPSKeyFile = "/home/blog/cert/key.pem"
```

## 参考

[acme.sh 使用](https://haokiu.com/blog/6D0DBH)
