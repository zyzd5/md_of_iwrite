# 命令
```bash
git config --global user.name "zyzds"
# 设置提交人为 "zyzds"

git config --global user.email 1325471284@qq.com
# 设置提交人邮箱为 1325471284@qq.com

git config --global credential.helper store
# 储存当前--还是没懂，等我看懂了再补全

git config --global --list
# 查看全局的配置信息, global 可以替换为--local, 查看当前仓库的配置信息
```

```bash
git init
# 创建仓库

git status
# 查看状态

git log
git log --oneline       #简洁日志
# 查看提交日志 

git add [file_name]
# 文件添加到暂存区

git add .
# 将所有修改过的文件和所有未被跟踪的文件添加到暂存区中

git rm [file_name]
# 同时从工作区和暂存区删除文件

git rm --cached [file_name]
# 从暂存区删除文件

git ls-files
# 列出所有被跟踪的文件

git commit [file_name]
# 提交到仓库
# 默认会拉起默认文本编辑器来输入提交信息
git commit [file_name] -m ["message"]
# 添加-m参数来直接输入提交信息
git commit [filename] -am ["message"]
# 同时完成提交到暂存区和仓库

git reset
# 删除所有暂存区的文件

git reset --soft 
# 保存工作区的和暂存区的文件, 回退版本 

git reset --mixed 
# 工作区和暂存区都不保存, 回退版本 

git reset --mixed       # reset的默认参数
# 保存工作区, 删除暂存区, 回退版本 

git reflog 
# 查看所有操作的历史记录
# 可以在使用hard选项误删除后, 找到误删除对应的版本号, 在使用reset回退

git diff
# 默认比较的是工作区和暂存区的差别

git push
# 推送到仓库

git pull
# 拉取到仓库

git branch [branch_name]
# 创建新分支
git branch -d [branch_name]
# 删除已经合并的分支
git branch -D [branch_name]
# 强制删除分支

git switch [branch_name]
# 切换到其他分支

git merge [branch_name]
# 将其他分支合并到当前分支

git rebase [branch_name]
# 将其他分支变基到当前分支

```
# gitignore
* 创建一个仓库主目录下存在的.gitignore文件, 每一行对应的是添加是需要忽略的文件, 支持通配符

* 只有在文件被追踪前才可以被忽略

```bash
*.a
# 忽略所有 .a 文件

!lib.a
# 在上一条的基础上, 虽然忽略了所有的 .a 文件, 但是排除 lib.a 文件

/DIR
# 忽略主目录下的 /DIR 目录, 不忽略 subdir/DIR 目录

build/
# 忽略所有的 build 目录
```

# 配置 ssh 密钥
* 在用户根目录下创建 .ssh目录

* 在目录中输入 
```bash
ssh-keygen -t rsa -b 4096
# -t指定协议 rsa, -b指定块大小4096
```

* 根据提示生成后 `id_rsa` 为私钥, `id_rsa.pub` 为公钥

* 复制公钥文件到github页面设置中粘贴进 SSH Keys 中
# 小报错
```bash
warning: in the working copy of 'ansi.md', LF will be replaced by CRLF the next time Git touches it
# 检测到换行符不是windows风格而是unix风格, 这个警告仅仅是提醒, 一般都能继续正常工作
```