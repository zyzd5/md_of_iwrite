## .alacritty.yml
```yml
# 注意缩进
font:
    normal:
        family: UbuntuMono Nerd Font Mono
        style: Regular
    bold: 
        family: UbuntuMono Nerd Font Mono
        style: Bold
    italic: 
        family: UbuntuMono Nerd Font Mono
        style: italic 
    bold_italic:          
        family: UbuntuMono Nerd Font Mono
        style: BoldItalic
    size: 14
```
## WARN
```bash
[0.001890179s] [WARN ] [alacritty] YAML config "/home/zyzds/.alacritty.yml" is deprecated, please migrate to TOML using `alacritty migrate`
# Alacritty 在版本更新后改用了 TOML 格式的配置文件，而不再支持 YAML 格式。因此，你需要将你的配置文件从 YAML 格式迁移到 TOML 格式。

# 在终端中输入
alacritty migrate
# 将会将 yaml 格式转换为 toml 格式的配置文件
```