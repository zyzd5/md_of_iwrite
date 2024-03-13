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

# -t： 指定文件系统的类型。
mount -t ext4 /dev/sdXn /mnt/data

# -o： 允许你提供挂载选项，比如读写权限、用户权限等。
mount -o rw /dev/sdXn /mnt/data
# 这里的 rw 表示读写权限，你可以根据需要设置不同的选项。
# -r： 以只读模式挂载。


mount -r /dev/sdXn /mnt/data
# -L： 通过卷标挂载文件系统。

mount -L mylabel /mnt/data
# -U： 通过 UUID 挂载文件系统。

mount -U 12345678-1234-5678-1234-567812345678 /mnt/data
# 可以通过 lsblk -o NAME,UUID 查看文件系统的 UUID。


# --bind： 将一个目录挂载到另一个目录，实现目录的重定向。
mount --bind /source/directory /destination/directory

# -o loop： 用于挂载一个文件作为块设备，通常用于挂载 ISO 文件。
mount -o loop filename.iso /mnt/iso

# -n： 阻止 /etc/fstab 中列出的文件系统自动挂载。
mount -n /mnt/data
```
```
在 /etc/fstab 文件中，挂载选项用于定义文件系统的挂载行为。以下是一些常见的挂载选项：

auto： 自动挂载。系统启动时会自动挂载。

noauto： 不自动挂载。系统启动时不会自动挂载，需要手动挂载。

exec： 允许执行程序。这个选项允许在文件系统上执行二进制文件。

noexec： 禁止执行程序。这个选项会阻止在文件系统上执行二进制文件。

ro： 以只读模式挂载。文件系统是只读的，不能进行写操作。

rw： 以读写模式挂载。文件系统是可读写的。

user： 允许普通用户挂载。这个选项允许普通用户挂载文件系统，而不仅仅是超级用户。

users： 允许多个用户挂载。与 user 类似，但允许多个用户同时挂载。

owner： 只有所有者可以挂载。这个选项限制只有挂载点的所有者才能挂载文件系统。

group： 只有组成员可以挂载。只有挂载点的组成员才能挂载文件系统。

umask： 设置默认权限掩码。影响文件和目录的权限，默认为 022。

defaults： 使用默认挂载选项。通常包括 rw、suid、dev、exec、auto、nouser 等。

async： 异步挂载。写操作不会等待写入磁盘，而是立即返回。

sync： 同步挂载。写操作会等待写入磁盘后才返回。

atime： 更新访问时间。默认情况下，文件系统会更新文件的访问时间。使用 noatime 选项可以禁用这个行为。

noatime： 禁止更新访问时间。

nodiratime： 禁止更新目录的访问时间。
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
ExecStart=sudo ./home/zyzds/clash/clash -d ./
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
* 默认 shell 为 zsh 时 fcitx 不会自动启动且启动后无法在chrome中输入
尝试添加这些到/etc/environment中
```bash
export XIM_PROGRAM=fcitx
export XIM=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=“@im=fcitx”
export LANG=“zh_CN.UTF-8”
```

* 出现问题运行
```bash
fcitx-diagnose
```

### manjaro
* 先换源
```bash
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syy
```

* 安装fcitx要用的组件
```bash
sudo pacman -S fcitx5 \
sudo pacman -S fcitx5-configtool  \
sudo pacman -S fcitx5-qt\
sudo pacman -S fcitx5-gtk\
sudo pacman -S fcitx5-chinese-addons\
sudo pacman -S fcitx5-material-color\
sudo pacman -S kcm-fcitx5\
sudo pacman -S fcitx5-lua
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
执行
```bash
fc-cache -fv
# 刷新缓存, f参数：force，v参数：view
```
```bash
fc-list 
# 显示所有支持的字体, 推荐搭配grep使用
fc-list : family style
# 显示所有字体系列
```
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