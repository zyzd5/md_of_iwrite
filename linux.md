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
```bash
#获取可用的硬盘分区
sudo fdisk -l       #recommend
lsblk               #or

sudo mkdir /mnt/data   #创建挂载点,可以是home目录下的文件夹
sudo mount -t ntfs-3g /dev/mounting_disk /dir1/dir2 #临时挂载

#开机自动挂载
sudo vim /etc/fstab
#添加如下文字，根据条件更改
/dev/sdXn   /mnt/data   ntfs   defaults   0   0
```

```bash
#取消挂载
sudo umount /mnt/data   #/mnt/data为挂载点
```
```bash
#-a： 挂载 /etc/fstab 文件中列出的所有文件系统。
mount -a
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
