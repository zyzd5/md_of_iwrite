* 在功能中启动 `适用于Linux的Windows子系统`
```bash
wsl --install 
# 安装默认发行版

wsl --set-default-version ${Version}
# Version为1 或 2

wsl --list --online
# 通过在线商店获取可用的 linux 发行版

wsl --install -d ${distribution Name}
# 安装指定发行版

wsl --set-default ${distribution Name}
# 设置默认发行版

wsl --set-version ${distribution name} ${versionNumber}
# versionNumber 为 1 或 2 

wsl --list --verbose
# 列出已安装的 linux 发行版

wsl --status
# 查看状态

wsl --shutdown
# 终止所有正在运行的发行版, 重点是所有

wsl --terminate ${distribution Name}
# 终止指定的发行版运行

wsl --unregister ${distribution Name}
# 注销并卸载指定的发行版
```
## 报错
### 无法解析服务器的名称或地址
>将控制面板中的网络连接中的ipv4协议的dns改为114.114.114.114, 备用地址改为8.8.8.8
### 0x800701bc
>报错如下  
WslRegisterDistribution failed with error: 0x800701bc
Error: 0x800701bc WSL 2 ?????????????????? https://aka.ms/wsl2kernel
```bash
wsl --update # 即可解决
```