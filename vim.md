## 键盘的语法
>`hjkl`四个键对应上下左右，`hj`左右,`jk`上下  
--  
`i`表示`insert`，`I`表示从`行首`插入  
`a`表示`append`，`A`表示从`行尾`插入    
`o`表示`open new line`,新增`下一行`  
`O`表示与`o`相反，新增上一行  
~~我觉得无所谓啦，能进入insert就是好模式~~    
--  
`gg` 再开一把，表示移动到第一行  
`G` 取反义移动到最后一行  
--  
`yy`表示`yank`，复制一行  
`yw`表示`yank a word`  
`p`表示`paste`  
`3p`表示`粘贴3次`  
--    
`.`表示重复上次操作  
--  
`u`表示`undo`，撤回上次操作  
`ctrl+r`，撤回上次的撤回  
--  
`dw`,表示`delete a word`
`cw`,表示`change a word`  
--  
`w`,表示`word`，下个单词首部  
`e`,表示`end`，下个单词尾部  
`b`，表示`back`，上个单词首部  
--  
`ci`表示`change in`，删除{}的内容物  
`/searching_word`，使用/来匹配单词
---
>`ctrl+v`表示`visual block`，选中一块  
`shift+v`，选中一行  
选中后可以使用`y`(yank), `d`(delete), `p`(paste)等等  



```bash
        #加入到.vimrc中
set number          #显示数字行号
set relativenumber  #显示相对数字行号
示行号
```
