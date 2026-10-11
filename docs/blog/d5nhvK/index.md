# docker apt-get


为了节省空间，docker 容器里面有很多命令是没有安装的，提示：
	Reading package lists... Done
	Building dependency tree
	Reading state information... Done
	E: Unable to locate package vim

### 更新apt-get源
这时候需要敲：`apt-get update`

这个命令的作用是：同步 /etc/apt/sources.list 和 /etc/apt/sources.list.d 中列出的源的索引，这样才能获取到最新的软件包。

### 安装vim
`apt-get install vim`

### 安装telnet
`apt-get install  telnet`

### 安装ifconfig
`apt-get install net-tools`
