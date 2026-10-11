# S3协议


S3是Simple Storage Service的缩写，即简单存储服务。亚马逊的名词缩写也都遵循这个习惯，例如Elastic Compute Cloud缩写为EC2等等。

S3说的玄乎一点可以叫云存储，通俗一点就是大网盘。其概念类似于分布式文家系统，同Google的GFS应该在一个层面。

目前的阿里的oss，腾讯的cos，七牛云存储都兼容aws的S3，所以要更换这些服务商之间提供的云存储非常容易，只需要简单的修改Access Key, Secrect Key等就行。

## S3的定义如下

Amazon S3 is a web service that enables you to store data in the cloud. You can then download the data or use the data with other AWS services, such as Amazon Elastic Cloud Computer (EC2).

看来除了做网盘只用，S3存储的数据还可以被其他的亚马逊高层服务直接引用，这一点比国内的简单的网盘提供商高不少，亚马逊大网盘是其整体Solution中的有机组成部分。

## 基本概念

### 1. bucket – 类比于文件系统的目录

A bucket is a [Container](http://lib.csdn.net/base/docker) for objects stored in Amazon S3. Every object is contained in a bucket. For example, if the object named photos/puppy.jpg is stored in the johnsmith bucket, then it is addressable using the URL http://johnsmith.s3.amazonaws.com/photos/puppy.jpg

似乎目录不能嵌套，也就是不能有子目录，官方的说法是起到namespace的作用，是访问控制的基本单位，其实丫还是个目录。

### 2. Object – 类比文件系统的文件

对象中带有对象名名，对象属性，对象本身最大5G，其实也还是个文件。

目前object有Versioning的属性（即对象不同历史版本的cache概念），这个是文件系统不具备的，在早期看到的S3资料中没有这一概念，应该是演进的结果，其面对的应该是有[版本控制](http://lib.csdn.net/base/git)的需求的用户。

### 3. Keys – 类比文件名

key的样式也是URL，记住亚马逊的服务都是使用Web Service或REST方式访问的。

例如，http://doc.s3.amazonaws.com/2006-03-01/AmazonS3.wsdl

其中‘doc’就是目录名（桶名），”2006-03-01/AmazonS3.wsdl”是文件名（对象名）。

如果引入了version则bucket + key + version唯一标示一个版本的文件。

### 4. Versioning – 类比CVS中的一个版本

同名文件的写入，并不覆盖已有文件而是增加了一个最新的文件版本。

同样的删除也不真正删除，而是mark了删除标记。

当最新版本mark为deleted之后，对该对象的get操作返回404错误，除非明确指定一个历史版本。

当然也可以指定版本永久删除其中一个拷贝。

### 5. Regions – 文件存储的地理位置 

这个也是文件系统中不存在的，就是不同的地理区域，用户可以指定将文件存在某个国家的服务器。我个人认为，这不是一个很好的概念，作为云的提供商，应该对于应用屏蔽这些部署细节。工程实现同技术理想还是有差距。目前其可以指定的server位置有美国、爱尔兰、新加坡等地。

## 接口API

常用的API就是读、写、增、删、改、查等等。使用标准的SOAP和REST定义。

尤其一提的是对于对象的获取，除了用http直接按照C/S方式获取之外，亚马逊支持BT协议，也就是说提供种子。从用户角度想，亚马逊会 charge更少的钱，但同时亚马逊自身也会减负。bt下载的速度就不太稳定了，基本取决于种子“质量”也就是取决于对文件感兴趣的人的多寡。例如命名为 “XX门”估计文件下载能够快很多。

## 参考

http://aws.amazon.com/s3/#functionality

http://docs.amazonwebservices.com/AmazonS3/2006-03-01/

http://developer.amazonwebservices.com/connect/forum.jspa?forumID=24
