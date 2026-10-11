# haokiu网站启动脚本


[haokiu](https://haokiu.com) 的启动脚本，配置 https 可以参考[beego 通过acms.sh 使用 https](https://haokiu.com/blog/qP3u4V)
```
#!/bin/sh
siteDir='/usr/local/pixiublog'

appName='pixiublogMain'

echo "kill the running program"

ps -ef | grep $appName | grep -v grep | awk '{print $2}' | xargs kill -9

echo "sleep 3 secons for app to shutdown"
sleep 3

echo "start program"

cd $siteDir

nohup $siteDir/$appName >> $siteDir/console.log 2>&1 &
```

