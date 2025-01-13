## ln
* `symbolic link`: like shortcut in Windows
    * link point to target_file's `path`
    * if target_file was deleted, link will be a invalid link 

* `hard link`: the entry of file
    * each file must have at `least one` hard link
    * a file's all of hard link be deleted, the file will be detele
```sh
ln [option] source_file target_file
# none option will create hard link
# -s: symbolic link
# -v: verbose

ln -s source_file soft_link
```
## disable nvidia driver
```bash
sudo vim /etc/default/grub

# modify it
GRUB_CMDLINE_LINUX_DEFAULT="nouveau.modeset=0"

sudo update-grub

sudo vim /etc/modprobe.d/blacklist-nvidia.conf

sudo vim /etc/modprobe.d/blacklist-nvidia.conf

# add it
blacklist nvidia
blacklist nvidia-drm
blacklist nvidia-modeset
blacklist nvidia-uvm
blacklist nouveau

sudo mkinitcpio -P

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
```/etc/systemd/system/clash.service
[Unit]
Description=clash service
After=network.target

[Service]
Type=simple
ExecStart=sudo ./home/zyzds/C/zyzds/clash/clash -d /home/zyzds/C/zyzds/clash
User=root
[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl start clash      
sudo systemctl enable clash     
```
```bash
sudo systemctl stop clash       
sudo systemctl disable clash    
```

* 添加到环境变量中(添加到 ~/.bashrc 和 ~/.zshrc 中)
```bash
export http_proxy=127.0.0.1:7890
export https_proxy=127.0.0.1:7890
```

* manage website
https://clash.razord.top/#/proxies
## zsh
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
