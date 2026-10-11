# Part I


此仓库是公众号【**高性能服务器开发**】文章汇总，如需下载全部文章，可以在公众号回复关键字“**文章下载**”即可得到下载链接。分享和转发文章时请保留作者信息，部分文章来源于网络，侵权请联系删除。

> 我也专门建立了读者交流群，想加群的读者可以加我微信easy_coder

在线阅读站点1：https://balloonwj.github.io/cpp-guide-web/

在线阅读站点2: http://balloonwj.gitee.io/cpp-guide-web/

备份站点：http://101.37.25.166/blog/

> **如需下载该站点源码用于自己搭建站点，可以在【高性能服务器开发】微信公众号后台回复关键字“站点下载”即可得到下载链接。**



![](http://haokiu.seaxiang.com/haokiu/415f8b5f0a6f9458d3560b4bdade475d.png)

## Part I
* [C++必知必会的知识点](https://haokiu.com/blog/6176f55c32444820a0055fadcf89273c)
    * [如何成为一名合格的C/C++开发者？](https://haokiu.com/blog/79cb378b756e457cbcb3a3c669a8e4c0)
    * [不定参数函数实现var_arg系列的宏](https://haokiu.com/blog/e3f33300987a43d08044b27dbbc5e9ec)
    * [你一定要搞明白的C函数调用方式与栈原理](https://haokiu.com/blog/2d2976c6ad824a1b9e2c44ffad106432)
    * [深入理解C/C++中的指针](https://haokiu.com/blog/ec8d1fd1cfc24923bdb71accca3fc1e4)
    * [详解C++11中的智能指针](https://haokiu.com/blog/913fb3f31d024baf871726b2f22cdfde)
    * [C++17结构化绑定](https://haokiu.com/blog/b08571a528324d72b376f4ccb2a6dad3)
    * [C++必须掌握的pimpl惯用法](https://haokiu.com/blog/4a2f5d00bb404b68a468bd72dfe357f8)
    * [用Visual Studio调试Linux程序](https://haokiu.com/blog/f64c601f237d4cac97445aa4b0e07369)
    * [如何使用Visual Studio管理和阅读开源项目代码](https://haokiu.com/blog/9a2768ae509d48689a05cf010b262b09)
    * [利用cmake工具生成Visual Studio工程文件](https://haokiu.com/blog/cf3a65cd7c2a40d1a4dbfd708c471c01)


* [多线程](https://haokiu.com/blog/dd345ae60ca14a61866fcc2f232aed74)
    * [后台C++开发你一定要知道的条件变量](https://haokiu.com/blog/3418f291fe18455999e74a1f1dbad72a)
    * [整型变量赋值是原子操作吗？](https://haokiu.com/blog/c5ae7c2ab16046b2b12deffde01da947)


* [网络编程](https://haokiu.com/blog/6e60982d515240e4b34e2f0e22647f58)
    * [bind 函数重难点解析](https://haokiu.com/blog/48af9bced29e4786944b5661c4155665)
    * [connect 函数在阻塞和非阻塞模式下的行为](https://haokiu.com/blog/f82abb8bce8a4c85b9b8c665cb9fe48d)
    * [select 函数重难点解析](https://haokiu.com/blog/2369cd70c2354e9c844815c14f31134c)
    * [Linux epoll 模型（含LT 模式和 ET 模式详解）](https://haokiu.com/blog/e4e0126749ad480399c46665753f03e4)
    * [socket 的阻塞模式和非阻塞模式](https://haokiu.com/blog/7a9421787c4a4e7482e4f3ea6234c7ac)
    * [非阻塞模式下 send 和 recv 函数的返回值](https://haokiu.com/blog/7050b3d426bf44b29c25c3d30ae77006) 
    * [服务器开发通信协议设计介绍](https://haokiu.com/blog/27166845330344e4bf4f9a385e69fc94)
    * [TCP 协议如何解决粘包、半包问题](https://haokiu.com/blog/7b86f55ffdcd4434a17beb9dbf7b9527)
    * [网络通信中收发数据的正确姿势](https://haokiu.com/blog/ec34cfea56f74c0d9a622ef5cbc4f812)
    * [服务器端发数据时，如果对端一直不收，怎么办？](https://haokiu.com/blog/bb7da7e0bc524808b2a072fb43da3a8e)
    
* [程序员必知必会的网络命令](https://haokiu.com/blog/2137687badbe411cac56094071bcc338)
    * [利用telnet命令发电子邮件](https://haokiu.com/blog/966ed73cc54b4cf5bdae1e1e5adba616)
    * [做Java或者C++开发都应该知道的lsof命令](https://haokiu.com/blog/a21d8fb5077b4bdfacf0cd5f4583f1cc)
    * [Linux网络故障排查的瑞士军刀nc命令](https://haokiu.com/blog/501d5d7dacf24f4098180740dba82434)
    * [Linux tcpdump使用详解](https://haokiu.com/blog/6eecf1781f7d4e1691c367ebf702d4d2)
    * [从抓包的角度分析connect函数的连接过程](https://haokiu.com/blog/f3b5fbeb80e645c9b5bd3d1feea7b387)
    * [服务器开发中网络数据分析与故障排查经验漫谈](https://haokiu.com/blog/b7d459605e1d4d46adba41bdb0c66b78)


 ## Part II     
* [高性能服务器框架设计](https://haokiu.com/blog/95e6ea6c39e345bf8177b77fb2d24548)
    * [主线程与工作线程的分工](https://haokiu.com/blog/450c6c7995774bec88a383c0ce41cfdc)
    * [Reactor模式](https://haokiu.com/blog/23cb111095cb47f3b6115efccd11086d)
    * [实例：一个服务器程序的架构介绍](https://haokiu.com/blog/f6db032966024846bbd5dbc28868bb17)
    * [错误码系统的设计](https://haokiu.com/blog/32ba3bce20124dd380cdde0bba6ef5b9)
    * [日志系统的设计](https://haokiu.com/blog/1549ab1669fe40dda14c41a84df83415)
    * [如何设计断线自动重连机制](https://haokiu.com/blog/1469709fbebd462cb012819cdfb07156)
    * [心跳包机制设计详解](https://haokiu.com/blog/82046162d4f74d3b9745ef1e8f8cdf57)
    * [业务数据处理一定要单独开线程吗](https://haokiu.com/blog/d7e436585f754029be5279a858049912)
    * [C++ 高性能服务器网络框架设计细节](https://haokiu.com/blog/10dc93cb0ce148d1906354635024bb25)
    
* [服务器开发案例实战](https://haokiu.com/blog/5d978400ccba478eaaa6a166b4ffba8d)
    * [从零实现一个http服务器](https://haokiu.com/blog/2ec66b5605c8455e833f06d2a23fff09)
    * [从零实现一款12306刷票软件](https://haokiu.com/blog/42f423476e5d4262bcb032f3cf4c40d3)
    * [从零实现一个邮件收发客户端](https://haokiu.com/blog/e1e38f7ff0e941c8ad6e51923070551d)
    * [从零开发一个WebSocket服务器](https://haokiu.com/blog/f8c9189db8404c76867e71440f136a2c)
    * [从零学习开源项目系列（一）从一款多人联机实时对战游戏开始](https://haokiu.com/blog/416ada8e33704bdcadd3202dd2413740)
    * [从零学习开源项目系列（二）最后一战概况](https://haokiu.com/blog/92d9492b21aa444d81eb4f31c1bfabb1)
    * [从零学习开源项目系列（三） CSBattleMgr服务源码研究](https://haokiu.com/blog/86a8b9de9c914f8ab93a3d36b455838b)
    * [从零学习开源项目系列（四）LogServer源码探究](https://haokiu.com/blog/fea618d6d104410cb5df6bc54d9529f2)

## Part III
* [TeamTalk IM源码分析](https://haokiu.com/blog/0da28a69a69242919c3333dc8e970a8f)
    * [01 TeamTalk介绍](https://haokiu.com/blog/8c53924ed21041948dff215384cdb81d)
    * [02 服务器端的程序的编译与部署](https://haokiu.com/blog/23af895a60264bfe949c3636689d3f83)
    * [03 服务器端的程序架构介绍](https://haokiu.com/blog/74f8790b79af42ab856a668b8927b38a)
    * [04 服务器端db_proxy_server源码分析](https://haokiu.com/blog/5481b95ce7c64f8c99c98e3c59d74314)
    * [05 服务器端msg_server源码分析](https://haokiu.com/blog/27deab1b64f24c839058b60bd3826f79)
    * [06 服务器端login_server源码分析](https://haokiu.com/blog/1866caff3acc4baeb8666ea706d7ba7d)
    * [07 服务器端msfs源码分析](https://haokiu.com/blog/0055f7fa607b4b2180cd0eb3924eff5c)
    * [08 服务器端file_server源码分析](https://haokiu.com/blog/c5f5c9828a6f472d9768cffc2f548784)
    * [09 服务器端route_server源码分析](https://haokiu.com/blog/d337b00514f346dcb055e1a411da83d8)
    * [10 开放一个TeamTalk测试服务器地址和几个测试账号](https://haokiu.com/blog/601f5e2b4c0a4303a540259d9d394d0b)
    * [11 pc客户端源码分析](https://haokiu.com/blog/ee4c77c4daf64f5f821d76808ec0b8b3)


* [libevent源码深度剖析](https://haokiu.com/blog/5d2f8fa20fdc4018a34afe19f8c23987)
    * [libevent源码深度剖析01](https://haokiu.com/blog/8aa77e3ff7e54bdb8899e32f75300864)
    * [libevent源码深度剖析02](https://haokiu.com/blog/d62a9a215b334817945e5814d92a423a)
    * [libevent源码深度剖析03](https://haokiu.com/blog/88dcf812d9464727bdfa54410657cfaa)
    * [libevent源码深度剖析04](https://haokiu.com/blog/7fd5744edc6741c18b5cb6187e662e40)
    * [libevent源码深度剖析05](https://haokiu.com/blog/1f6a82cdb17742a49514907b604e44c1)
    * [libevent源码深度剖析06](https://haokiu.com/blog/fc115cade0c049a8ab14e737a22b37fe)
    * [libevent源码深度剖析07](https://haokiu.com/blog/1fa932a07dd84e9fbdde728e110c098f)
    * [libevent源码深度剖析08](https://haokiu.com/blog/4a5e0c5a568b4187b207ec0ada2dbdfb)
    * [libevent源码深度剖析09](https://haokiu.com/blog/e65e0c91ca7e45ad9ad3081edbd423f8)
    * [libevent源码深度剖析10](https://haokiu.com/blog/f567712a9375435692b3217e444f19e5)
    * [libevent源码深度剖析11](https://haokiu.com/blog/136973dd819b459bac605bcb1a25571c)
    * [libevent源码深度剖析12](https://haokiu.com/blog/1f455bc4e89944fe8fb0ca8f3bbcdc1b)
    * [libevent源码深度剖析13](https://haokiu.com/blog/b05b12b227ee4ce494fe99d9116d6a23)

* [leveldb源码分析](https://haokiu.com/blog/c898014e5b304df0bade6b12d638467a)
    * [leveldb源码分析1](https://haokiu.com/blog/1776ae3c50104b7ea0c90cf31322958a)
    * [leveldb源码分析2](https://haokiu.com/blog/c955baadcc824d20acb455e1078a257c)
    * [leveldb源码分析3](https://haokiu.com/blog/34fc58749a224c92be698a0d9cd27b99)
    * [leveldb源码分析4](https://haokiu.com/blog/f4dfd0e7e33240c9807a11402d34ddb3)
    * [leveldb源码分析5](https://haokiu.com/blog/81982087975a4f49913e723952169670)
    * [leveldb源码分析6](https://haokiu.com/blog/3e005b6becda44edaa67dc81f32d5499)
    * [leveldb源码分析7](https://haokiu.com/blog/b3a81cdfb8624332bd1f184097675b32)
    * [leveldb源码分析8](https://haokiu.com/blog/8554dc1843294f5fa7955b748c61710f)
    * [leveldb源码分析9](https://haokiu.com/blog/899ada7f72f249e6938aef7f300eaf1a)
    * [leveldb源码分析10](https://haokiu.com/blog/603a94de7932474cbf7478a2d7b94ebf)
    * [leveldb源码分析11](https://haokiu.com/blog/0159e326ba0e4917878529ee1ae3af48)
    * [leveldb源码分析12](https://haokiu.com/blog/cd6a8ad07c9f4c479a1e88591f05cd70)
    * [leveldb源码分析13](https://haokiu.com/blog/f110bd8130344cbf801fc30d4d7a7ce9)
    * [leveldb源码分析14](https://haokiu.com/blog/5a5f7db3f4fc4684a0c7ddb21dd6ea40)
    * [leveldb源码分析15](https://haokiu.com/blog/bd56540c7f464f2e8e9392c3903b27f5)
    * [leveldb源码分析16](https://haokiu.com/blog/383f27c1087943b39b255aa993d7b9ac)
    * [leveldb源码分析17](https://haokiu.com/blog/0d1705067c1d403889b748a57e0b3af5)
    * [leveldb源码分析18](https://haokiu.com/blog/9276872cee384cebb6d1c912acedf0a2)
    * [leveldb源码分析19](https://haokiu.com/blog/2d765b7b763343038b1df047545b2017)
    * [leveldb源码分析20](https://haokiu.com/blog/0da12c5829764cdc8a508c0a05e99a3e)
    * [leveldb源码分析21](https://haokiu.com/blog/1d4ede18ded04a569baee5550226fa6f)
    * [leveldb源码分析22](https://haokiu.com/blog/08d56462861f4df7b247921ba14a88e2)

* [Memcached源码分析](https://haokiu.com/blog/d10283bf526c437a9e64e40d5afa25c4)
    * [00 服务器资源调整](https://haokiu.com/blog/8f65d01cc42d4c8782d95eed02dd4eb5)
    * [01 初始化参数解析](https://haokiu.com/blog/778cf564240e4d19ad39e0e271d66b3d)
    * [02 网络监听的建立](https://haokiu.com/blog/9a03435a987949d28e30905f7a0c839b)
    * [03 网络连接建立](https://haokiu.com/blog/2a422d9fa3fe4cddbcbef326866d8943)
    * [04 内存初始化](https://haokiu.com/blog/c82fe349df914fb8943e4aa3231c9cad)
    * [05 资源初始化](https://haokiu.com/blog/f56b1e30eede4a21b7fd293a33a1e47a)
    * [06 get过程](https://haokiu.com/blog/9dbcb2b8ef6b4cdbab38c3845d520ef0)
    * [07 cas属性](https://haokiu.com/blog/4d2fa7e9284a4e7fb742bdda30d20da6)
    * [08 内存池](https://haokiu.com/blog/63c41390d91c4392a0d3cc433c49a4ac)
    * [09 连接队列](https://haokiu.com/blog/596315b99d2f40dba9c9ea13e975bd9d)
    * [10 Hash表操作](https://haokiu.com/blog/857ca75e1a154abc91281759ea864d5c)
    * [12 set操作](https://haokiu.com/blog/a795d0b698914f3898a0896633cd92ad)
    * [13 do_item_alloc操作](https://haokiu.com/blog/50d829bedab44857aaf08cfd61e6c952)
    * [14 item结构](https://haokiu.com/blog/3fee4e4314af42ee9fa58cda4aa0b839)
    * [15 Hash表扩容](https://haokiu.com/blog/3ba1e9453dcc49edb8ee1597bb133cdd)
    * [16 线程交互](https://haokiu.com/blog/314f7e41e35f43db9facbca467726a7a)
    * [17 状态机](https://haokiu.com/blog/4547681a8a0d42759accab81b61267ab)
    
* [游戏开发专题](https://haokiu.com/blog/c1e71fdf335346f5aadad6e1d1dc3e55)
    * [1 游戏服务器开发的基本体系与服务器端开发的一些建议](https://haokiu.com/blog/867310d7f5a74f758c1745b3083cfcc8)
    * [2 网络游戏服务器开发框架设计介绍](https://haokiu.com/blog/288a2c3a9e374a3ebf898cfa184e2921)
    * [3 游戏后端开发需要掌握的知识](https://haokiu.com/blog/16d1fbc7aa204ddba0ef394895d2c2b6)
    * [4 关于游戏服务端架构的整理](https://haokiu.com/blog/a7ec43bdee96498694f118163763c921)
    * [5 各类游戏对应的服务端架构](https://haokiu.com/blog/47a72212e86d4b6a8fe0516f8ff1cf65)
    * [6 从腾讯QQgame高性能服务器集群架构看“分而治之”与“自治”等分布式架构设计原则](https://haokiu.com/blog/84414d52b22b4cdaa7a7cf4beb0e1585)
    * [7 QQ游戏百万人同时在线服务器架构实现](https://haokiu.com/blog/64368e0e78ea4a568fff21e1511c0f43)
    * [8 大型多人在线游戏服务器架构设计](https://haokiu.com/blog/5b23fbec804b470cb12e3c20af54d1d0)
    * [9 百万用户级游戏服务器架构设计](https://haokiu.com/blog/db5f58a948804f718159e858bf744da9)
    * [10 十万在线的WebGame的数据库设计思路](https://haokiu.com/blog/ace809ec27124ecc987bcd4c7eec569f)
    * [11 一种高性能网络游戏服务器架构设计](https://haokiu.com/blog/8d180ec3ae3e409bac6e8a67811f54bc)
    * [12 经典游戏服务器端架构概述](https://haokiu.com/blog/d7795d37211b43728424c7c4f7469b67)
    * [13 游戏跨服架构进化之路](https://haokiu.com/blog/3a513d0ec4fc47e2b3830ec79beb1572)

## Part IV
* [程序员面试题精讲](https://haokiu.com/blog/c092595334ac4b29914e418b3aae0648)
    * [腾讯后台开发实习生技能要求](https://haokiu.com/blog/5f118ee0e1be49a8a754072ecb9b441a)
    * [聊聊如何拿大厂的 offer](https://haokiu.com/blog/61401d1e68344e7b94c634f9b00cdbe4)
    * [网络通信题目集锦](https://haokiu.com/blog/eb4b0ccb7b2942b989b3655d832bb0e0)
    * [我面试后端开发经理的经历](https://haokiu.com/blog/b9e6c063ac4a43aca14c01cc45b2f8fa)
    * [Linux C/C++后端开发面试问哪些问题](https://haokiu.com/blog/8570010b5d82422da83500ab481816be)

* [职业规划](https://haokiu.com/blog/01f6fc4ce7c54057a2379aab6b98843f)
    * [给工作 4 年迷茫的程序员们的一点建议](https://haokiu.com/blog/049d41c798c54956b4c2b094aacec413)
    * [聊聊技术人员的常见的职业问题](https://haokiu.com/blog/1908cdb9f5c747b996136e3b3e408b8d)
    * [写给那些傻傻想做服务器开发的朋友](https://haokiu.com/blog/7f969a868ee54e84982aa97c89e7cdbd)

* [自我提升与开源代码](https://haokiu.com/blog/e50a72b7fb4e47a9904a05621e5b692f)
    * [2020 年好好读一读开源代码吧](https://haokiu.com/blog/ea1d963411184ea88648b092380ee687)

* [后端开发相关的书籍](https://haokiu.com/blog/624d2104f4a54c50940f5de425c06ab0)
    * [后台开发应该读的书](https://haokiu.com/blog/b46f16d0f9f8415e94eb76455deea0f0)

* [程序员的简历](https://haokiu.com/blog/15d5370937664a8d84891f5e983b87f4)
    * [程序员如何写简历](https://haokiu.com/blog/9c853d8576774df7ad52d79d740d95f1)

* [程序员的薪资与年终奖那些事儿](https://haokiu.com/blog/18d3e73501ef4be092520d6f5991517f)
    * [技术面试与HR谈薪资技巧](https://haokiu.com/blog/d949dd8f005d45c7b6c71ea9a87a0712)
    * [聊一聊程序员如何增加收入](https://haokiu.com/blog/cbd700214d4e4bc691c5f33f6e905343)
    * [谈一谈年终奖](https://haokiu.com/blog/0f72f7a83bbb4b4fb76a05dc63f5480c)

* [程序员的烦心事](https://haokiu.com/blog/e11a027d307841d9b515ac4b1670037c)
    * [拒绝了一家公司的offer后，他们的副总和hr总监同时打电话来询问拒绝原因并极力要求加入，我该不该去？](https://haokiu.com/blog/40c71c6aa54540abb1c141d82ca0cd49)
    * [我是一名程序员，结婚时女友要求我用两年的工资作为彩礼，我该不该答应？](https://haokiu.com/blog/5b6afa35b0644098b8b4d0c853f20358)

* [作者的故事](https://haokiu.com/blog/745f468dc9234e4f95ac9d848e64fa0b)
    * [我的 2019](https://haokiu.com/blog/fce122b624fd44a88df285c221d765b8)
    * [我是如何年薪五十万的](https://haokiu.com/blog/7a566da932f2481388ca678c2dc2c1ac)


> 如果您在阅读上述文章的过程中有任何问题或者建议，可以加我微信easy_coder交流。

Enjoy it!
