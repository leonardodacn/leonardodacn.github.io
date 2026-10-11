# linux 复制文件，并创建不存在的目录


linux复制文件和目录用cp命令，`--parents` 参数可以确保不存在目录的创建，比如文件 `cp --parents java/doc/readme.md ../doc` ，如果目录 doc不存在目录：java/doc则会创建。

高级操作：
```
#查找当前目录下所有.md文件，并将它们复制到DataxDoc目录，如果目录不存在则双肩
find . -name "*.md" | xargs -I {} cp --parents {} ../DataxDoc
```
