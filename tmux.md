## 命令
```bash
tmux ls     

tmux attach -t ${session_id}
```

## 默认键位
* `prefix`: ctrl+b

* `${prefix}` + `d`: detach 
### window
* `${prefix}` + `c`: 创建新窗口 

* `${prefix}` + `数字`: 窗口之间切换

* `${prefix}` + `b/n`: 前后切换窗口

* `${prefix}` + `&`: 关闭当前窗口
### Pane
* `${prefix}` + `%`: 向右分裂窗格

* `${prefix}` + `"`: 向下分裂窗格

* `${prefix}` + `上下左右`: 窗格之间移动

* `${prefix}` + `q`: 手动选择窗格

* `${prefix}` + `z`: 窗格最大化/还原

* `${prefix}` + `x`: 关闭当前窗格


