# 目录


# 目录

* [第1章 语法变迁](http://haokiu.com/blog/c3984397f8e5480f81aaaeaf1b82ac23)
  * [1.1 Go1的诺言](http://haokiu.com/blog/3edad2cabde0428f9098185e6d62c870)
  * [1.2 Go1到Go1.10](http://haokiu.com/blog/7ec2e79995ed4c9f8b883cc07c8d78f9)
  * [1.3 Go1.10过渡到Go2](http://haokiu.com/blog/2756df043ed74a91bd57f134270e6cbc)
  * [1.4 Go2诞生](http://haokiu.com/blog/4f9267cc85a647979aa3803c5c435407)
* [第2章 模块化](http://haokiu.com/blog/8ef2da522892434187a81439c5d1dc2d)
  * [2.1 Go1的包机制](http://haokiu.com/blog/e07062bd3a82483893b16c9a014f22dc)
  * [2.2 基于vendor的版本管理(TODO)](http://haokiu.com/blog/ba3f4751a98a484f995283b9377b90d1)
  * [2.3 模块的设计⽬标(TODO)](http://haokiu.com/blog/0ade9d480b954dbc96381d011208c5f1)
  * [2.4 模块快速⼊⻔(TODO)](http://haokiu.com/blog/99154ed6163e4a40bcfdc5e7d5956c7d)
  * [2.5 子模块和多版本共存(TODO)](http://haokiu.com/blog/c868302e70ab472280a428d5583e15d2)
  * [2.6 镜像和私有仓库(TODO)](http://haokiu.com/blog/3681abb2d5e34af2be2ea2f170c6226f)
  * [2.7 模块化实践中的一些问题(TODO)](http://haokiu.com/blog/1fbab86b16734c59b0bff743e512dfb2)
* [第3章 错误处理(TODO)](http://haokiu.com/blog/615b0dd45d2e4323805039e0ffb41808)


<!--
1.
语言只定义了包的概念
包可以有不同的实现，比如基于zip的包集合

最早是没有gopath的
makefile时代的编译，和goroot是放在一起的
标准库包和用户包的分离

2.
gopath
intrnal
vendor

和std同名的包

3.
vendor的问题
本质原因是不同包中的类型不一样
vendor内的包对应新路径的包

4. 模块的设计⽬标

问题，有时候需要调试，临时修改以来包的代码，
但是修改之后会导致其它依赖此包的应用被影响，可以用replace吗

5. 模块快速⼊⻔
 go mod命令

6. go.mod 和 go.sum⽂件

7. go get重新⼊⻔

8. 语义化版本号

9. v1/v2/v3版本共存

10. ⼦模块

11. 最⼩化版本选择

12. 版本不相容和间接依赖

不相容是历史问题，临时调试修改依赖的包


14. 私有仓库/镜像
以前是每个pkg的go get需要DNS查网址，如果要定制指南修改hosts文件，
但是修改hosts文件将对其它应用产生影响。

-->
