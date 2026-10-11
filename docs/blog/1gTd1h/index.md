# 网站部署脚本


网站的部署脚本

```shell
#!/bin/sh

#部署目录
siteDir='/usr/local/pixiublog'

# 源代码目录
cd /root/pixiublog

echo "update code"

git pull

echo "build pixiublog"

go build main.go

echo "remove old"

rm -rf $siteDir/views

rm -rf $siteDir/static

rm -rf $siteDir/pixiublog

echo "mv new program to $siteDir"

cp main $siteDir/pixiublog

cp -rf views $siteDir/

cp -rf static $siteDir/

echo "kill the running program"

ps -ef | grep 'pixiublog' | grep -v grep | awk '{print $2}' | xargs kill -9

echo "start program"

cd $siteDir

nohup $siteDir/pixiublog >> $siteDir/console.log 2>&1 &
```
