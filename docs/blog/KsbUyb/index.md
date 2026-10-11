# curl https 地址报异常


用 acme.sh 生产了 Let's Encrypt 的https 证书，在浏览器访问没有问题，但在服务器访问出现下面的异常：
```
curl: (60) SSL certificate problem: unable to get local issuer certificate
More details here: https://curl.haxx.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```

网站用了beego，用 acme.sh 生成的证书。配置：
```
EnableHTTPS = true
HTTPSPort = 443
HTTPSCertFile = "/home/blog/cert/cert.pem"
HTTPSKeyFile = "/home/blog/cert/key.pem"
```

要将 cert.pem 替换为：fullchain.pem
```
EnableHTTPS = true
HTTPSPort = 443
HTTPSCertFile = "/home/blog/cert/fullchain.pem"
HTTPSKeyFile = "/home/blog/cert/key.pem"
```
