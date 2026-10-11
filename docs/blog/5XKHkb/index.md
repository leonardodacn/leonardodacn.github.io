# 简单脚本实现服务监控


服务经常会重启失败，写了个简单的shell叫脚本，可以发现服务端口是否起来，没有发现监听端口会重启服务

### 1.监控脚本
```
if [ -z "`lsof -i:443 | grep LISTEN`" ];then
    echo -e "restart $(date +'%Y-%m-%d %H:%M:%S')"
    systemctl restart pixiublog
fi
```

### 2.系统定时任务
```
*/3 * * * * /usr/local/pixiublog/monitor.sh >> /usr/local/pixiublog/monitor.log 2>&1
```


