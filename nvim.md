## config.lua
```lua
local option = vim.opt
local buffer = vim.b
local global = vim.g

option.showmode = false
-- 是否显示 INSERT VISUAL 等信息

option.backspace = {"indent", "eol", "start"}
-- 控制退格键的行为
-- indent: 允许退格键删除自动缩进的空白字符。
-- start: 允许退格键删除插入模式开始前的字符。  
-- eol(end of line): 允许退格键删除行尾的换行符，从而把当前行和上一行合并。

option.tabstop = 4
-- 将每个制表符显示为4个空格的宽度
option.shiftwidth = 4
-- 控制自动缩进时使用的空格数
option.expandtab = true
-- 将 Tab 键转换为空格
option.softtabstop = 4
-- 按下 Tab 键插入 4 个空格
option.shiftround = true
-- 使用 '>>' 命令时自动对齐

option.autoindent = true
-- 自动继承前一行的缩进
option.smartindent = true
-- 根据情况不会自动继承前一行的缩进, 例如遇到 "}" 时

option.number = true
option.relativenumber = true

option.wildmenu = true
-- 在命令模式下通过菜单来显示所有可选项
option.wildmode = {"longest:full", "full"}
-- 控制 wildmenu 的行为
-- longest:full 先补全到所有的公共项, 再显示菜单
-- full 显示所有可能的选项

option.hlsearch = true
-- 高光显示搜索文字
option.ignorecase = true
-- 搜索忽略大小写
option.smartcase = true
-- 如果搜索模式中没有大写字母，则忽略大小写（即遵循 ignorecase 的设置）。
-- 如果搜索模式中包含一个或多个大写字母，则区分大小写。

option.completeopt = {"menu", "menuone"}
-- 配置补全菜单的行为
-- menu：显示补全菜单，方便选择不同的补全项。
-- menuone：即使只有一个匹配项也显示补全菜单，这样你可以明确看到补全的选项。

option.cursorline = true
-- 高亮光标所在的行

opton.termguicolors = true
-- 真彩色

option.signcolumn = true
-- 显示符号列
-- 用于显示信息, 如断点, 折叠

option.autoread = true
-- 文件变更后自动重新读取

option.title = true
-- 终端标题会根据当前打开的文件变动

option.swapfile = false
option.backup = false
option.updatetime = 50
option.mouse = "a"
option.undofile = true

option.wrap = true
option.splitright = true
------------------------------------
buffer.fileenconding = "utf-8"
------------------------------------
global.mapleader = " " 
```
