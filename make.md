## 示例
```make
.PHONY: clean # 伪目标

# 自定义环境变量
CC = gcc # 指定编译器

CFLAGS = -I include # 指定头文件目录
CFILES = $(shell find src -name "*.c") # 搜索所有的源文件
OBJS = $(CFILES:.c=.o) # 所有的目标文件
TARGET = main # 最终生成目标
DATA = src/data/*.txt # 搜索所有的数据文件

RM = -rm -f # 删除方式

all: $(TARGET)
	git commit -a -m "> make"

# 项目构建方式
$(TARGET): $(OBJS)
	$(CC) -o $(TARGET) $(OBJS)

%o : %c
	$(CC) -c $(CFLAGS) $< -o $@

clean:
	$(RM) $(TARGET) $(OBJS) $(DATA)
	git commit -a -m "> make clean"
```
## gcc
```bash
gcc -c hello.c			#编译程序, 会生成hello.c
gcc -o main hello.o		#链接hello.o生成./main可执行文件
```
## 伪目标
```make
.PHONY: clean		
# 声明clean为伪目标
```
如果不声明clean为伪目标就会生成名称为`clean`的文件, 再次执行会比对是否最新, 是最新则不会执行`clean`对应的命令
## 关键词
```make
.DEFAULT_GOAL=hello.o
# 执行make时默认生成hello.o文件

.SECONDEXPANSION
# 一种模式, 分开展开
"$"的模式
```

## 变量
```make
obj = main
$(obj): hello.cc
	g++ -o $(obj) .cc
```

## 自动推断生成规则
```make
hello: 
# 留空也可以, 会自动推断
```

## sub makefile
```make
include ./dir/makefile.build
#可以读取到里层makefile.build的变量
# makefile.build的名字可以任意
```

## 双冒号::
```make
hello::
	gcc hello.c -o hello
clean:
	rm hello
# 不管目标hello是不是最新的都将无条件执行hello
```

## 多个目标相同, 执行最后一个目标
```make
.PHONY: print
print: 
	echo "helloworld"

print:
	echo "goodbye"
# 输出goodbye
```

## $$在命令中转义为$
```make
.PHONY print

print:
	$$(hello)
# 输出$$(hello)
```

## order-only 依赖
有两种依赖, 一种是普通依赖, 另一种是order-only依赖
```make
target: normal_dep1 normal_dep2 | order-only_dep1
```
* 管道符号左边为普通依赖, 右边为order-only依赖

* 普通依赖比目标新, 则目标会被更新, 但是order-only不管是否比目标新, 都不会更新目标

## Wildcard 展开 (通配符展开)
```make
object = *.o
```

> object = *.o 这种变量定义, 如果在命令行中使用可能会被认为是shell中的值, 为避免这种麻烦, 可以写成这种形式 
```make
objects := $(wildcard *.o )
```
# 到VPATH这一节了