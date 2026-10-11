# mysql replace 


mysql replace 可以将字段的字符串内容替换，语法：
```
Update `table_name` SET `field_name` = replace (`field_name`,’from_str’,'to_str’) Where `field_name` LIKE ‘%from_str%’
```
使用样例：
```
# 将 blog 表的字段 coentent 里的 "https://haokiu.com" 替换为 "http://haokiu.com"
update blog set content = replace(content, "https://haokiu.com", "http://haokiu.com") where content like '%https://haokiu.com%'
```

