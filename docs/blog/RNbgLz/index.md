# beego restful path variable


beego的url路径有多个变量的设置和获取方法。

## 在 router.go 注册 url
```
beego.Router("/type/:type/?:page", &controllers.WebController{}, "get:Type")
```

## 获取变量
```
typeID, err := self.GetInt(":type")

func (c *Controller) GetInt(key string, def ...int) (int, error) {
	strv := c.Ctx.Input.Query(key)
	if len(strv) == 0 && len(def) > 0 {
		return def[0], nil
	}
	return strconv.Atoi(strv)
}
```
