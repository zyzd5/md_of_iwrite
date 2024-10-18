## Command

## Normal
* `zz`: 屏幕居中
* `zt`: 屏幕第一行
* `zb`: 屏幕最后一行

* `%`: 跳转到配对的配对符(括号等)处
## Insert
* `s`: 删除当前光标的字符, 进入insert
* `S`: 删除当前行, 进入insert
## Register
* 一个字符对应一个寄存器(如`a-z`, `0-9`)
* 特别的寄存器
    * `"`: 默认寄存器, 平时复制, 删除的内容都在里面
    * `%`: 当前文件名
    * `.`: 上一次插入的内容
    * `:`: 上一次执行的命令
* 通过`:reg {register}` 查看对应寄存器的内容
* 在复制/删除/粘贴/等操作前加上`{register}`就可以指定本次操作使用的寄存器
* 只要涉及寄存器操作的都可以这样指定
    * `ayy`: 将这一行复制到`a`寄存器中
    * `bdiw`: 当单词删除, 保存到`b`寄存器中
    * `cp`将`c`寄存器中的内容粘贴出来
## 宏
* 录制一系列键盘操作, 并且允许重放操作
* 操作序列存储在指定的寄存器中
    * `q{register}` 开始录制宏, 存在寄存器 `register` 中
    * 录制过程中按 `q` 退出录制
    * `@{register}`: 重放寄存器`{register}`中的操作
    * `@@`: 重放上一次宏操作
    * `.` 对宏不生效
## config
```vim
let mapleader = ' ' 

set encoding=utf-8
set number
set relativenumber
set clipboard+=unnamedplus
set scrolloff=4
set incsearch
set ignorecase
set smartcase
set expandtab
set shiftwidth=4
set tabstop=4
set whichwrap=b,h,l,<,> 

nnoremap <leader>h <C-w>h
nnoremap <leader>l <C-w>l
nnoremap <leader>j <C-w>j
nnoremap <leader>k <C-w>k

nnoremap ; ^
nnoremap ' $

nnoremap J <Nop>
nnoremap q: <Nop>
nnoremap <C-e> <Nop>

vnoremap J >+1<CR>gv=gv
vnoremap K <-2<CR>gv=gv

nnoremap <leader>va ggVG
```
