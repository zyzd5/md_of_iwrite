## font
复制字体文件到/usr/share/fonts/或者~/.local/share/fonts/中，执行fc-cache -fv（f参数：force，v参数：view



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
ExecStart=sudo /home/zyzds/clash/clash -d /home/zyzds/clash/
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

* 添加到环境变量中
```bash
export http_proxy=127.0.0.1:7890
export https_proxy=127.0.0.1:7890
```

* manage website
https://clash.razord.top/#/proxies

## gnome extension
https://extensions.gnome.org/

* https://extensions.gnome.org/extension/261/kimpanel/
>使 fcitx 正常工作

* https://extensions.gnome.org/extension/307/dash-to-dock/
> 安装 dock 面板

* https://extensions.gnome.org/extension/3740/compiz-alike-magic-lamp-effect/
> 仿苹果出现效果

* https://extensions.gnome.org/extension/3210/compiz-windows-effect/
> 拖动窗口效果
## fcitx
* 出现问题运行
```bash
fcitx-diagnose
```

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

* 添加这三行到~/.zshrc
```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

## 安装chrome
* 安装前置依赖
```bash
sudo pacman -S ttf-liberation
```
* 安装chrome
```bash
pamac build google-chrome
```
