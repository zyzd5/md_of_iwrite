* 在功能中启动 `适用于Linux的Windows子系统`
## 重新挂载盘符
```bash
sudo vim /etc/wsl.conf
```
```ini
[automount]
enabled = true
root = /mnt/
options = "metadata,umask=22,fmask=11"
```
* `enable = true`: 启用自动挂载

* `root = /home/zyzds`: 自动挂载到 /home/zyzds 下

* `options = "metadata, umask=22, fmask=11"`: 
    * `metadata`: 启用对文件的元数据支持, 允许 wsl 存储和读取文件的额外属性 

    * `umask`: 决定文件和目录的默认权限
        * 22 表示 权限默认为755, 计算方式为 777 - 022

    * `fmask`: 决定文件的默认权限, 会覆盖 `umask` 的配置
        * 计算原理同 `umask`
## command
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
