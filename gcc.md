```sh
gcc -o output_file hello.c
# -o means output

```

* -o output: 指定生成程序名称
```sh
gcc -o output hello1.c hello2.c
gcc -o output hello1.o hello2.o
# 可以使用 .o 中间文件或者 .c 源文件来生成可执行程序
```
* -c create: 创建中间 `.o` 文件
