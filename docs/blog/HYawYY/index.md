# frp 使用


frp 是一个可用于内网穿透的高性能的反向代理应用，支持 tcp, udp, http, https 协议。本文简单的介绍frp的配置使用。

实现内网穿需要有一台公网服务器。本文将公网服务器称为服务端，内网服务器称为客户端。需要开启相关的端口。相关端口没开通，访问就会失败。

frp git地址:https://github.com/fatedier/frp
中文文档：https://github.com/fatedier/frp/blob/master/README_zh.md
frp下载地址：https://github.com/fatedier/frp/releases
本文使用软件：frp_0.21.0_linux_amd64.tar.gz
本文使用系统：centos7（公网一台，内网一台）

本文使用软件：frp_0.21.0_linux_amd64.tar.gz，frp的客户端和服务端都在同一个包里。

文件说明
  frps.ini: 服务端配置文件
  frps: 服务端软件
  frpc.ini: 客户端配置文件
  frpc: 客户端软件

### frps.ini配置

```
[common]
bind_port = 7000
# auth token
token = Qwert123
dashboard_port = 7500
# dashboard 用户名密码，默认都为 admin
dashboard_user = admin
dashboard_pwd = Qwert123
vhost_http_port = 7083
```

开启服务端服务
`./frps -c ./frps.ini`

可以用脚本来启动：

```
#!/bin/sh
nohup /usr/local/frp/frps -c /usr/local/frp/frps.ini &
```

### frpc.ini配置

```
[common]
#服务器ip地址
server_addr = 121.199.2.XXX
server_port = 7000

#开放api，提供reload服务
admin_addr = 127.0.0.1
admin_port = 7400

# auth token
token = Qwert123

[ssh]
type = tcp
local_ip = 127.0.0.1
#ssh端口
local_port = 22
remote_port = 1022
```

可以使用脚本来启动(start.sh)

```
#!/bin/sh
sudo nohup /usr/local/frp/frpc -c /usr/local/frp/frpc.ini &
```

如果更改配置文件，可以使用重新加载来更新配置(reload.sh)

```
#!/bin/sh
/usr/local/frp/frpc reload -c /usr/local/frp/frpc.ini &
```

配置完后就可以通过 ssh 121.199.2.XXX 1022 来连接到内网服务器。

## centos7开机启动

/usr/lib/systemd/system/frp.service

```
[Unit]
Description=the frp service
After=syslog.target network.target

[Service]
Type=forking

ExecStart=/usr/local/frp/start.sh
ExecReload=/bin/kill -USR2 $MAINPID
ExecStop=/bin/kill -SIGINT $MAINPID

[Install]
WantedBy=multi-user.target
```

执行：

```bsh
systemctl enable frp
systemctl start frp
```

转自：http://www.seaxiang.com/blog/frp
