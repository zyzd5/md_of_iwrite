## .alacritty.toml
* 在 https://alacritty.org/config-alacritty.html 中查看详细
```toml
[window]
startup_mode = "Windowed"

opacity = 0.93
# 不透明度, 默认为1.0
decorations = "Buttonless"
# Linux 下 只能 Full 或 Buttonless
# 标题栏模式, macOS only, 默认为 "Full"

[font]
size = 14
# font size

[font.bold]
family = "UbuntuMono Nerd Font Mono"
style = "Bold"
# Bold style

[font.bold_italic]
family = "UbuntuMono Nerd Font Mono"
style = "BoldItalic"
# BoldItalic style

[font.italic]
family = "UbuntuMono Nerd Font Mono"
style = "italic"
# italic style

[font.normal]
family = "UbuntuMono Nerd Font Mono"
style = "Regular"
# Regluar style

[font.offset]
x = 0
y = 3
# 字体 x, y 方向偏移值
# 默认 (0, 0)
```
## WARN
```bash
[0.001890179s] [WARN ] [alacritty] YAML config "/home/zyzds/.alacritty.yml" is deprecated, please migrate to TOML using `alacritty migrate`
# Alacritty 在版本更新后改用了 TOML 格式的配置文件，而不再支持 YAML 格式。因此，你需要将你的配置文件从 YAML 格式迁移到 TOML 格式。

# 在终端中输入
alacritty migrate
# 将会将 yaml 格式转换为 toml 格式的配置文件
```
