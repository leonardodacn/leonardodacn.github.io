# golang 常用函数


### 1. 获取当前时间
```
时间戳(秒)：time.Now().Unix

日期：time.Now().Format("2006-01-02 15:04:05")

注意：参数必须是 2006-01-02 15:04:05 而不能是自定义的年月日时间
```

### 2. 字符串与int转换
```
i,_ := strconv.Atoi("3")

a := strconv.Itoa(32) 
```

### 3.结构体json序列化 
```
chatMsg := &ChatMsg{}

err := json.Unmarshal([]byte(msg), chatMsg) //json转结构体

buf, _ := json.Marshal(chatMsg) //结构体转json

return string(buf)
```

### 4.删除切片元素
```
mySlice := make([]int, 5) //创建一个初始元素个数为5的数组切片，元素初始值为0

mySlice = append(mySlice[:i], mySlice[i+1:]...) //删除下标为i的元素

mySlice = append(mySlice[:0], mySlice[1:]...) //删除第1个元素
```

### 5. url encode/decode
```
encodeUrl:= url.QueryEscape(urltest)

decodeUrl,err := url.QueryUnescape(encodeUrl) 
```

### 6. base64编码
```
encodeString := base64.StdEncoding.EncodeToString(input)

decodeBytes, err := base64.StdEncoding.DecodeString(encodeString)
```

### 7. 获取字符串长度
```
tips := "忍者"

len := len(tips) //len=6

len := utf8.RuneCountInString(tips) //len=2
```

### 8. SubString
```
func SubString(str string, start int32, end int32) string {

  result := []rune(str)

  length := int32(len(result))

  if start < 0 || start > length {
    return str
  } 

  if end < 0 || end > length {
    return str
  } 

  return string(result[start:end])

  }

result = SubString(result, 0, int32(len([]rune(result)))-1)//注意end参数的取值
```

### 9. 结构体类型断言
```
logger := &log.Logger{}

fl, ok := interface{}(logger).(*FileLogger)
```

1. 类型断言变量一定要是一个接口变量，否则报错 `invalid type assertion: xxx (non-interface type xxx on left)`;

2. 使用类型断言的思路，应该是接收到一个接口值，但不确定这个值具体的类型，然后通过类型断言来判断。

### 10. os常用函数
```
import (
    "os"
    "fmt"
    "time"
    "strings"
)
  
//os包中的一些常用函数
  
func main() {
  
    //获取主机名
    fmt.Println(os.Hostname());
  
    //获取当前目录
    fmt.Println(os.Getwd());
  
    //获取用户ID
    fmt.Println(os.Getuid());
  
    //获取有效用户ID
    fmt.Println(os.Geteuid());
  
    //获取组ID
    fmt.Println(os.Getgid());
  
    //获取有效组ID
    fmt.Println(os.Getegid());
  
    //获取进程ID
    fmt.Println(os.Getpid());
  
    //获取父进程ID
    fmt.Println(os.Getppid());
  
    //获取环境变量的值
    fmt.Println(os.Getenv("GOPATH"));
  
    //设置环境变量的值
    os.Setenv("TEST", "test");
  
    //改变当前工作目录
    os.Chdir("C:/");
    fmt.Println(os.Getwd());
  
    //创建文件
    f1, _ := os.Create("./1.txt");
    defer f1.Close();
  
    //修改文件权限
    if err := os.Chmod("./1.txt", 0777); err != nil {
        fmt.Println(err);
    }
  
    //修改文件所有者
    if err := os.Chown("./1.txt", 0, 0); err != nil {
        fmt.Println(err);
    }
  
    //修改文件的访问时间和修改时间
    os.Chtimes("./1.txt", time.Now().Add(time.Hour), time.Now().Add(time.Hour));
  
    //获取所有环境变量
    fmt.Println(strings.Join(os.Environ(), "\r\n"));
  
    //把字符串中带NULL或$var替换成指定指符串
    fmt.Println(os.Expand("NULL NULL NULL", func(k string) string {
        mapp := map[string]string{
            "1": "111",
            "2": "222",
            "3": "333",
        };
        return mapp[k];
    }));
  
    //创建目录
    os.Mkdir("abc", os.ModePerm);
  
    //创建多级目录
    os.MkdirAll("abc/d/e/f", os.ModePerm);
  
    //删除文件或目录
    os.Remove("abc/d/e/f");
  
    //删除指定目录下所有文件
    os.RemoveAll("abc");
  
    //重命名文件
    os.Rename("./2.txt", "./2_new.txt");
  
    //判断是否为同一文件
    //unix下通过底层结构的设备和索引节点是否相同来判断
    //其他系统可能是通过文件绝对路径来判断
    fs1, _ := f1.Stat();
    f2, _ := os.Open("./1.txt");
    fs2, _ := f2.Stat();
    fmt.Println(os.SameFile(fs1, fs2));
  
    //返回临时目录
    fmt.Println(os.TempDir());
}
```

### 11. 文件常用函数
```
import (
    "os"
    "fmt"
    "strconv"
)

//os包中关于文件的操作函数
  
func main() {
    //创建文件，返回一个文件指针
    f3, _ := os.Create("./3.txt");
    defer f3.Close();
  
    //以读写方式打开文件，如果不存在则创建文件，等同于上面os.Create
    f4, _ := os.OpenFile("./4.txt", os.O_RDWR|os.O_CREATE|os.O_TRUNC, 0666);
    defer f4.Close();
  
    //打开文件，返回文件指针
    f1, _ := os.Open("./1.txt");
    defer f1.Close();
  
    //修改文件权限，类似os.chmod
    f1.Chmod(0777);
  
    //修改文件所有者，类似os.chown
    f1.Chown(0, 0);
  
    //返回文件的句柄，通过NewFile创建文件需要文件句柄
    fmt.Println(f1.Fd());
  
    //从文件中读取数据
    buf := make([]byte, 128);
    //read每次读取数据到buf中
    for n, _ := f1.Read(buf); n != 0; n, _ = f1.Read(buf) {
        fmt.Println(string(buf[:n]));
    }
  
    //向文件中写入数据
    for i := 0; i < 5; i++ {
        f3.Write([]byte("写入数据" + strconv.Itoa(i) + "\r\n"));
    }
  
    //返回一对关联的文件对象
    //从r中可以读取到从w写入的数据
    r, w, _ := os.Pipe();
    //向w中写入字符串
    w.WriteString("写入w");
    buf2 := make([]byte, 128);
    //从r中读取数据
    n, _ := r.Read(buf);
    fmt.Println(string(buf2[:n]));
  
    //改变工作目录
    os.Mkdir("a", os.ModePerm);
    dir, _ := os.Open("a");
    //改变工作目录到dir，dir必须为一个目录
    dir.Chdir();
    fmt.Println(os.Getwd());
  
    //读取目录的内容，返回一个FileInfo的slice
    //参数大于0，最多返回n个FileInfo
    //参数小于等于0，返回所有FileInfo
    fi, _ := dir.Readdir(-1);
    for _, v := range fi {
        fmt.Println(v.Name());
    }
  
    //读取目录中文件对象的名字
    names, _ := dir.Readdirnames(-1);
    fmt.Println(names);
  
    //获取文件的详细信息，返回FileInfo结构
    fi3, _ := f3.Stat();
    //文件名
    fmt.Println(fi3.Name());
    //文件大小
    fmt.Println(fi3.Size());
    //文件权限
    fmt.Println(fi3.Mode());
    //文件修改时间
    fmt.Println(fi3.ModTime());
    //是否是目录
    fmt.Println(fi3.IsDir());
}
```

### 12. os中关于进程的操作
```
import (
    "os"
    "fmt"
    "time"
)
  
//os包中关于进程的操作函数
  
func main() {
    //设置新进程的属性
    attr := &os.ProcAttr{
        //files指定新进程继承的活动文件对象
        //前三个分别为，标准输入、标准输出、标准错误输出
        Files: []*os.File{os.Stdin, os.Stdout, os.Stderr},
        //新进程的环境变量
        Env: os.Environ(),
    }
  
    //win下通过记事本打开1.txt
    //开始一个新进程
    p, err := os.StartProcess("C:\\Windows\\System32\\notepad.exe", []string{"C:\\Windows\\System32\\notepad.exe", "D:\\1.txt"}, attr);
    if err != nil {
        fmt.Println(err);
    }
    fmt.Println(p);
    fmt.Println("进程ID：", p.Pid);
  
    //通过进程ID查找进程
    p2, _ := os.FindProcess(p.Pid);
    fmt.Println(p2);
  
    //等待10秒，执行函数
    time.AfterFunc(time.Second*10, func() {
        //向p进程发送退出信号
        p.Signal(os.Kill);
    });
  
    //等待进程p的退出，返回进程状态
    ps, _ := p.Wait();
    fmt.Println(ps.String());
}
```
