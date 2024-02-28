## 目录结构
```bash
.config/nvim
├── init.lua
├── lua
│   ├── core
│   │   ├── keymaps.lua
│   │   └── options.lua
│   └── plugins
│       └── lualine.lua
```
## init.lua
```lua
-- 存放引用
require("dir.file_name")

require("core.options") 
require("core.keymaps")

-- lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup({

-- 自动加载 ~/.config/nvim/lua/plugins 下每个 lua 文件 
    { import = "plugins" },

-- 使用 nightfly-colors 主题
    { "bluz71/vim-nightfly-colors", name = "nightfly", lazy = false, priority = 1000 },
})
-- lazy.nvim end


```
## ~/.config/nvim/plugins
* 符合 init.lua 中 import 语法, 例
    * 如果 插件的 github 页面支持
```lua
return
{
    "nvim-lualine/lualine.nvim", 
    depandencies = { 'nvim-tree/nvim-web-devicons' },
    config = function()
            require('lualine').setup()
        end, 
}
```
## ~/.config/nvim/core
### 配置文件 keymaps.lua --not finished
```lua
vim.g.mapleader = " "       -- 设置主键

local keymap = vim.keymap   -- 局部变量

```
### 配置文件 options.lua
```lua
local opt = vim.opt         -- 设置局部变量

opt.relativenumber = true   -- 显示相对行号    
opt.number = true           -- 显示当前行号的绝对行号

opt.tabstop = 4             -- 显示缩进符时的缩进数
opt.shiftwidth = 4          -- 按下tab插入的缩进数 
opt.expandtab = true        -- 使用空格代替制表符进行缩进
opt.autoindent = true       -- 自动缩进

opt.cursorline =true        -- 高亮显示光标所在的行

opt.mouse:append("a")       
-- 将 "a" 添加到 mouse 选项中, 允许你在 Normal 模式下使用鼠标来进行光标移动和文本选择

opt.clipboard:append("unnamedplus")
-- 将 "unnamedplus" 添加到 clipboard 选项中, "unnamedplus" 是一个常用的剪贴板提供者，它允许 Neovim 与系统剪贴板之间进行双向的文本复制和粘贴操作。

-- 默认新窗口右和下
opt.splitright = true
opt.splitbelow = true

opt.ignorecase = true
--这个命令用于启用忽略大小写搜索选项。当 ignorecase 设置为 true 时，搜索时会忽略搜索模式中的大小写。例如，如果你搜索 "apple"，那么匹配的结果中不管是 "Apple"、"APPLE" 还是 "aPPle" 都会被匹配到。
opt.smartcase = true
--这个命令用于启用智能大小写搜索选项。当 smartcase 设置为 true 时，如果搜索模式中包含大写字母，则搜索会区分大小写；如果搜索模式全部是小写字母，则搜索会忽略大小写。这使得你可以在需要时进行大小写敏感的搜索，而在不需要时进行大小写不敏感的搜索。

opt.termguicolors = true    -- 使用真彩色
opt.signcolumn = "yes"      -- 显示符号列       
-- `yes`: 始终显示 
-- `auto`: 有错误时显示
-- `no`: 永不显示
```