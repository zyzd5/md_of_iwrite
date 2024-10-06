## 通用
* 在每一项绘制出的项目均有 `Ordering` 选项, 调整 `Z Index` 可以设置绘制顺序

* 强制类型转换
```gd
str($varible)
# 强制转换 varible 为 String
```

* 背景音乐
    * 如果尝试在游戏场景中加载背景音乐为一个 `Node`, 在重新加载场景时则会重新开始播放音乐, 这很突兀
    * 在 `项目设置` -> `全局` -> `自动加载` 中设置可以解决

## Node
* `AnimatedSprite2D`: 可以导入素材来播放动画
```gd
$AnimatedSprite2D.play("$action_by_u")
```
* `CollisionShape2D`: 定义碰撞范围
* `Timer`: 在设定好的时间后触发事件
```gd
$Timer.start()
# 开始计时, 计时结束事件 timeout() 需要手动拖拽到脚本编辑器中绑定
```
* `Area2D`: 定义区域, 可以通过信号来绑定区域进入事件
* `CharactorBody2D`: 创建脚本时拥有默认的移动脚本, 拥有碰撞判定
* `RayCast2D`: 2D 空间中的射线, 可以通过方法 `$".".is_colliding() 来判断物体是否碰撞, 与 if 结合使用来定义事件`
* `Lable`: 添加文字, 可以拖拽
```gd
$Lable.text = "String" + varible + "String"
```
## function
```gd
queue_free()
# 也可以写作 $Object.queue_free()
# 延迟删除, 等待当前帧结束后才会删除对象

free()
# $Object.free()
# 立即删除对象, 如果脚本还想继续访问对象, 就会发生错误

var tree = get_tree()
# 访问场景树

get_tree().change_scene("res://$new_scene.tscn")
# 切换场景

get_tree().paused = true/false
# 暂停/ 恢复

var root = get_tree.root
# 获取根节点

get_tree().call_group("my_group", "func_name") 
# 向某个节点组中的所有节点发送信号或调用函数

get_tree.quit()
# 退出

Input.get_axis("$negetive_action", "positive_action")
# input 是类, 指定两个方向的输入, 一个为正, 一个为负
# 当玩家不动时返回 0, 正负方向移动时返回 -1/1
```
