## grub
* 更改启动顺序
```bash
sudo vim /etc/default/grub
# when u modified it
sudo update-grub
```
## disable nouveau driver
```bash
sudo vim /etc/modprobe.d/blacklist.conf
```
* add this
```bash
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```
## time sync
```bash
sudo apt install ntpdate
sudo ntpdate time.windows.com
sudo hwclock --localtime --systohc      
```
## mount
* -t(type): 文件系统类型
* -o 
```bash
# 获取可用的硬盘分区
sudo fdisk -l       
lsblk              

sudo mount -t ntfs /dev/mounting_disk /dir1/dir2 #临时挂载
```

```bash
#取消挂载
sudo umount /mnt/data   #/mnt/data为挂载点
```
### listing the mounts
* -l(list)
* -t(type)
```bash
mount -l
# 列出所有挂载点, 默认操作

mount -l -t ntfs
# 按类型列出挂载点
```
### 手动自动挂载
```bash
sudo vim /etc/fstab
# 添加如下配置
/dev/sdXn   /mnt/data   ntfs   defaults   0   0
```
## proxy
```bash
#启动clash
./clash -d ./       #-d表示directory ./代表使用当前目录下的mmdb文件和配置文件
```

```bash
#绑定systemd实现自启
sudo vim /etc/systemd/system/clash.service
```
```bash
[Unit]
Description=clash service
After=network.target

[Service]
Type=simple
ExecStart=sudo ./home/zyzds/Documents/clash/clash -d /home/zyzds/Documents/clash
User=root
#ExecStart后替换为具体的命令
[Install]
WantedBy=multi-user.target
```
* Type字段是服务运行时的类型，simple表示它是一个后台进程，通常用于只有一个进程的服务。  
* ExecStart字段包含了要运行的命令，多个命令可以用换行符（\n）隔开。  
* User字段指定了以哪个用户的身份运行这个服务，这里选择root用户.

```bash
sudo systemctl start clash      #启动服务
sudo systemctl enable clash     #添加到启动项
```
```bash
sudo systemctl stop clash       #停止
sudo systemctl disable clash    #禁用   
```

* 添加到环境变量中(添加到 ~/.bashrc 和 ~/.zshrc 中)
```bash
export http_proxy=127.0.0.1:7890
export https_proxy=127.0.0.1:7890
```

* manage website
https://clash.razord.top/#/proxies
## zip
```bash
zip pkg.zip file1.txt file2.txt
```
## terminal
```bash
export EDITOR=vim
alias "q"="exit"
alias "n"="nvim"
# 更改vim为默认文本编辑器
```
### 设置 sudo tlp-stat -b
```bash
sudo visudo
```
在 `@includedir /etc/sudoers.d` 后添加
zyzds ALL=(ALL) NOPASSWD: /usr/bin/tlp-stat
> 使用which tlp-stat 来确定路径
## gnome extensions
```bash
sudo apt install gnome-shell-extension-manager
```
* https://extensions.gnome.org/

* https://extensions.gnome.org/extension/261/kimpanel/
>使 fcitx 正常工作

* https://extensions.gnome.org/extension/307/dash-to-dock/
> 安装 dock 面板

* https://extensions.gnome.org/extension/3740/compiz-alike-magic-lamp-effect/
> 仿苹果出现效果

* https://extensions.gnome.org/extension/3210/compiz-windows-effect/
> 拖动窗口效果
## qq音乐
```bash
sudo vim /usr/share/applications/qqmusic.desktop
```
将
```bash
Exec=/opt/qqmusic/qqmusic %U
```
改为
```bash
Exec=/opt/qqmusic/qqmusic --no-sandbox %U
```
## zsh
### oh-my-zsh
* 安装oh-my-zsh
进入oh-my-zsh, 复制命令安装

* 查看已有主题
```bash
ls .oh-my-zsh/themes
```
```bash
ZSH_THEME="robbyrussell"
# in ~/.zshrc
```
* 查看拥有(不一定开启)的插件
```bash
ls ~/.oh-my-zsh/plugins
```
### 插件
* 安装 zsh-autosuggestions  --历史补全
```bash
git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-autosuggestions
```

* 安装 zsh-syntax-highlighting  --语法正确高亮
```bash
git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
* 配置.zshrc文件开启
```bash
plugins=(
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```
## fxitx
```bash
sudo apt install fcitx5
sudo apt install fcitx5-chinese-addons
sudo apt install fcitx5-mozc
```
* 添加到.zshrc中
```bash
export XIM_PROGRAM=fcitx
export XIM=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
export LANG="zh_CN.UTF-8"
```

* 出现问题运行
```bash
fcitx-diagnose
```
## bluetooth
### windows
```cmd
cd .\Download\PSTools\
./PsExec.exe -s -i regedit
定位到
```cmd
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys
```
### ubuntu
蓝牙的linkkey存放在
```bash
cd /var/lib/bluetooth/&主机蓝牙地址/设备蓝牙地址
sudo vim info
```
将两个linkkey修改为一致即可
## font
### 安装font
复制字体文件到/usr/share/fonts/或者~/.local/share/fonts/中，
## find 
```bash
find ./code -name test.cc
# 在 ./code 目录下搜索 test.cc文件
```
* 选项
    * -name: 按文件名搜索
    * -iname: 不区分大小写, 按文件名搜索 
        * i 表示 `ignore`
    * -inum 和 ls -i 配对使用, 以后再了解
## tar
* -c --create 创建新的tar文件
* -x --extract，--get 解开tar文件
* -t --list 列出tar文件中包含的文件的信息
* -v --verbose 列出每一步处理涉及的文件的信息，只用一个“v”时，仅列出文件名，使用两个“v”时，列出权限、所有者、大小、时间、文件名等信息
* -z --gzip，--gunzip，--ungzip 调用gzip执行压缩或解压缩
## 配置盒盖后不休眠
```bash
sudo nvim /etc/systemd/logind.conf
```
* 在[Login]部分
    * HandleLidSwitch - 盖子关闭时触发，下面的两种情况除外。
    * HandleLidSwitchExternalPower - 如果系统连接到外部电源，则在盖子关闭时触发。
    * HandleLidSwitchDocked - 如果系统插入扩展坞，或者连接了多个显示器，则在盖子关闭时触发。
    * 参数说明
        * ignore(无操作)
        * poweroff(关闭系统并切断电源)
        * reboot(重新启动)
        * halt(关闭系统但不切断电源)
        * kexec(调用内核"kexec"函数)
        * suspend(休眠到内存)
        * hibernate(休眠到硬盘)
        * hybrid-sleep(同时休眠到内存与硬盘)
        * suspend-then-hibernate(先休眠到内存超时后再休眠到硬盘)
        * lock(锁屏)
## ssh
```bash
sudo apt install openssh-server
```
### 密码连接
```bash
sudo systemctl status sshd
# 查看 sshd 状态
```
* 确定在同一局域网下, 使用ifconfig查看内网地址后使用
```bash
ssh User@192.168.x.x
```
### 密钥连接
* 在客机生成密钥
```bash
cd ~/.ssh
ssh-keygen
# 输入保存的文件名和指纹后回车
```
```bash
ssh-copy-id -i ~/.ssh/remote_ssh_key.pub zyzds@192.168.80.98
# 将指定的公钥传输给服务器
```
```bash
ssh -i ~/.ssh/remote_ssh_key zyzds@192.168.80.98
# 使用私钥登陆
```
### 禁用密码登陆
```bash
sudo vim /etc/ssh/sshd_config
```
```
PasswordAuthentication no
PubkeyAuthentication yes
```
### 配置自动连接
```bash
touch ~/.ssh/config
```
```bash
Host Y9000X
    Hostname 192.168.80.98
    IdentityFile ~/.ssh/remote_ssh_key
    User zyzds

# Host 为别名, 可以自己指定
# 剩下的自己看情况填
```
