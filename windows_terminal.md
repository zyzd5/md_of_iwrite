```sh
Test-Path $PROFILE
# 检查配置文件是否存在

New-Item -Path $PROFILE -ItemType File -Force
# 创建配置文件

nvim $PROFILE
# 打开配置文件

Set-Alias n nvim
Set-Alias cl clear
# 在文件中添加别名

Get-ExecutionPolicy
# 检查当前执行策略
# Restricted: 禁止运行任何脚本。
# RemoteSigned: 允许本地脚本运行，但远程下载的脚本需要有数字签名。
# AllSigned: 允许运行已签名的脚本。
# Unrestricted: 允许所有脚本运行，但会显示警告。

Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
# 更改执行策略
```
