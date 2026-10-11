# golang 数组与切片的区别


golang 的数组与切片有两大区别：
+ 初始化：数组需要明确指定大小，切片不需要
+ 函数传递：数组是值传递，切片是地址传递

## 初始化

### 数组
```
a := [...]int{1,2,3}   
a := [3]int{1,2,3}
```

### 切片
```
a:= []int{1,2,3}  
a := make([]int, 5) 
a := make([]int, 5, 10)
```

## slice的数据结构：
go源码slice的数据结构定义：
```
type slice struct {
    array unsafe.Pointer
    len   int
    cap   int
}
```

slice 有三个字段：
+ 指向真实 *array* 地址的指针 *ptr* 
+ *slice* 的长度 *len* 
+ 容量 *cap*

## 特性
通过例子说明 slice 和 array 的一些特性。

### 函数传递
数组需要明确指定大小，切片不需要。数组是值传递，切片是地址传递

```
	a := [...]int{1, 2, 3, 4, 5, 6}
	fmt.Println("star deal array, orginal data is:")
	fmt.Println(a)
	aMaxIndex := len(a) - 1
	fmt.Printf("aMaxIndex:%d\r", aMaxIndex)
	for i, e := range a {
		if i == aMaxIndex {
			a[0] += e
			fmt.Printf("index is 0, val is :%d\r", a[0])
		} else {
			a[i+1] += e
			fmt.Printf("index is:%d ,val is :%d\r", i+1, a[i+1])
		}
	}
	fmt.Println("deal result is:")
	fmt.Println(a)

	s := []int{1, 2, 3, 4, 5, 6}
	fmt.Println("star deal slice, orginal data is:")
	fmt.Println(s)
	sMaxIndex := len(s) - 1
	fmt.Printf("aMaxIndex:%d\r", sMaxIndex)
	for i, e := range s {
		if i == sMaxIndex {
			s[0] += e
			fmt.Printf("index is 0, val is :%d\r", s[0])
		} else {
			s[i+1] += e
			fmt.Printf("index is:%d ,val is :%d\r", i+1, s[i+1])
		}
	}
	fmt.Println("deal result is:")
	fmt.Println(s)
```

输出：
```
star deal array, orginal data is:
[1 2 3 4 5 6]
aMaxIndex:5
index is:1 ,val is :3
index is:2 ,val is :5
index is:3 ,val is :7
index is:4 ,val is :9
index is:5 ,val is :11
index is 0, val is :7
deal result is:
[7 3 5 7 9 11]
star deal slice, orginal data is:
[1 2 3 4 5 6]
aMaxIndex:5
index is:1 ,val is :3
index is:2 ,val is :6
index is:3 ,val is :10
index is:4 ,val is :15
index is:5 ,val is :21
index is 0, val is :22
deal result is:
[22 3 6 10 15 21]
```

这个是比较复杂的值传递和地址传递的例子，可以看到：
+ array在循环时每次拿到的值（*e*）是传递数组的值
+ slice在循环时每次拿到的值（*e*）是传递地址的值

所以最后a 和 s 的值会不一样。

### slice append的时候内存地址的改变情况

通过一个例子：
```
package main

import (
   "fmt"
   "unsafe"
)

func main() {
   //说先定义一个切片，只限定长度为1
   s := make([]int, 1)

   //打印出slice的长度，容量以及内存地址
   fmt.Printf("len :%d cap:%d array ptr :%v \n", len(s), cap(s), *(*unsafe.Pointer)(unsafe.Pointer(&s)))

   for i := 0; i < 5; i++ {
      s = append(s, i)
      fmt.Printf("len :%d cap:%d array ptr :%v \n", len(s), cap(s), *(*unsafe.Pointer)(unsafe.Pointer(&s)))
   }
   //打印出slice
   fmt.Println("array:", s)
}
```

输出：
```
len :1 cap:1 array ptr :0xc042062080 
len :2 cap:2 array ptr :0xc0420620c0 
len :3 cap:4 array ptr :0xc0420600e0 
len :4 cap:4 array ptr :0xc0420600e0 
len :5 cap:8 array ptr :0xc0420880c0 
len :6 cap:8 array ptr :0xc0420880c0 
array: [0 0 1 2 3 4]
```

可以看出来在append的过程中，内存地址有些是一样的，有些是不一样的，容量也是如此。

每次cap改变的时候指向array内存的指针都在变化。因为当在使用 *append* 的时候，如果 *cap==len* ，这个时候就会新开辟一块更大内存，然后把之前的数据复制过去。

最后一句输出slice元素的时候为什么会多了一个0呢？是因为make初始化时，都会初始化成对应数据类型的原值。

### cap的扩大规律
go 在 append 的时候放大 cap 是有规律的。在 cap 小于1024的情况下是每次扩大到 `2 * cap` ，当大于1024之后就每次扩大到 `1.25 * cap` 。
```
package main

import (
    "fmt"
    "unsafe"
)

func main() {
    //说先定义一个切片，只限定长度为1
    s := make([]int, 1)

    //打印出slice的长度，容量以及内存地址
    fmt.Printf("len :%d cap:%d array ptr :%v \n", len(s), cap(s), *(*unsafe.Pointer)(unsafe.Pointer(&s)))

    for i := 1; i < 1024*2; i++ {
        s = append(s, i)
        fmt.Printf("len :%d cap:%d array ptr :%v \n", len(s), cap(s), *(*unsafe.Pointer)(unsafe.Pointer(&s)))
    }
    //打印出slice
    fmt.Println("array:", s)
}
```

输出太多，截一部分：
```
...
len :1019 cap:1024 array ptr :0xc000184000 
len :1020 cap:1024 array ptr :0xc000184000 
len :1021 cap:1024 array ptr :0xc000184000 
len :1022 cap:1024 array ptr :0xc000184000 
len :1023 cap:1024 array ptr :0xc000184000 
len :1024 cap:1024 array ptr :0xc000184000 
len :1025 cap:1280 array ptr :0xc000188000 
len :1026 cap:1280 array ptr :0xc000188000 
len :1027 cap:1280 array ptr :0xc000188000 
len :1028 cap:1280 array ptr :0xc000188000
...
```


