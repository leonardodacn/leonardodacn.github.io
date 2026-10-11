# beego 的日志级别


看 beego 的源码，beego 的日志分为7个级别：

```
const (
	LevelEmergency = iota
	LevelAlert
	LevelCritical
	LevelError
	LevelWarning
	LevelNotice
	LevelInformational
	LevelDebug
)
```

转换为

```
	LevelEmergency = 0
	LevelAlert = 1
	LevelCritical = 2
	LevelError = 3
	LevelWarning = 4
	LevelNotice = 5
	LevelInformational = 6
	LevelDebug = 7
```
