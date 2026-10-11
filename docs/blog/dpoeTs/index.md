# golang 计算文件和字符串的 md5 值


go MD5 所需要的包在”crypto/md5”包中，需要先实例化一个MD5对象，然后在此基础上调用sum方法即可

## 文件的MD5

```go
md5 := md5.New()
io.Copy(md5,file)
MD5Str := hex.EncodeToString(md5.Sum(nil))
```

上面的代码实现了计算了文件MD5，其中file是multipart.File类型的，也可以是其他的已打开的其他文件类型。
当然也可以不使用io.copy，而是直接使用sum函数来计算：

```
md5 := md5.New()
MD5Str := hex.EncodeToString(md5.Sum(file))
```

这样是直接调用了sum函数来计算文件的值可能要比io.copy稍微慢一些。

## 字符串的MD5

有时候需要将已知的一段字符串加密，其实和文件加密大概是类似的，只需要调用write方法将字符串写入hash中：

```
md5 := md5.New()
md5.Write([]byte("hello,world!"))
MD5Str := hex.EncodeToString(md5.Sum(nil))
```
