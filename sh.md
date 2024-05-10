## 变量
```sh
echo "helloworld, $val"          
# 打印字符串和变量(也可使用${val}(推荐))

read $variable
# 从命令行读取

readonly variable
# 创建只读变量

unset variable
# 删除变量

string="helloworld" 
string='helloworld'
# 不区分 ' "

array=(1, 2, 3, 4, 5)
# 数组

string="helloworld"
length=${#string}
# 在变量中使用 # 来获取变量长度

string1="helloworld"
echo ${string1:0:5}
# 使用val:0:5来获取0号位开始的后5个字符

```
## shell
```sh
#!/bin/zsh
# 指定默认shell

bluetoothctl << EOF
connect $bluetooth_address 
exit
EOF
# 打开程序后自动输入
```

## for while if 
```sh
    for file in $files; do
        # somethint
    done
# for循环

    if [[ $file_type == *"executable"* ]] && [[ $file_type != *"text"* ]]; then
        echo "Deleting binary executable: ${single_file}"
        rm "${single_file}"
    fi
# if
```
