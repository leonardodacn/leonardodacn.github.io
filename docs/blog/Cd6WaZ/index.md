# golang 判断目录或文件是否存在


golang 判断目录或文件是否存在：

```
func Exist(path string) bool {
	_, err := os.Stat(path)
	return err == nil || os.IsExist(err)
}
```
