# beego 让http请求跳转到 https


如果beego配置了https，那么可以让 让http请求跳转到 https，怎样配置 beego 的https，可以参考[beego 通过acms.sh 使用 https](https://haokiu.com/blog/qP3u4V)
```
//siteUrl 是网站地址，比如:https://haokiu.com
if "HTTP/1.1" == self.Ctx.Request.Proto && siteUrl != "" && strings.HasPrefix(siteUrl, "https") {
		//如果支持https，则所有http请求跳转到https
		self.redirect(siteUrl + self.Ctx.Request.URL.Path)
}
```

