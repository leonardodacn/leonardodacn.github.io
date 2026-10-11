# go ... 作用


`…`  是go的一种语法糖。

## 作用

1. 用于函数有多个不定参数的情况，可以接受多个不确定数量的参数
2. 打散slice进行传递


## 例子

### 一、接受多个不确定数量的参数

```
func println(args ...string) { //可以接受任意个string参数
    for _, v:= range args{
        fmt.Println(v)
    }
}

func main(){
		var strss= []string{
        "qwr",
        "234",
        "yui",
        "cvbc",
    }
    println(strss...) //切片被打散传入
}
```

结果：

```
qwr
234
yui
cvbc
```

### 二、打散slice进行传递

```
var strss= []string{
  "qwr",
  "234",
	"yui",
}
var strss2= []string{
  "qqq",
  "aaa",
  "zzz",
  "zzz",
}
strss=append(strss,strss2...) //strss2的元素被打散一个个append进strss
fmt.Println(strss)
```

结果：

```
[qwr 234 yui qqq aaa zzz zzz]
```

## 最后

如果没有’…’，面对上面的情况，无疑会增加代码量。
