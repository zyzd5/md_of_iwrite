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
git reflog 
# 查看所有操作的历史记录
# 可以在使用hard选项误删除后, 找到误删除对应的版本号, 在使用reset回退

git branch [branch_name]
# 创建新分支
git branch -d [branch_name]
# 删除已经合并的分支
git branch -D [branch_name]
# 强制删除分支
git branch -m [branch_name]
# 当前分支 变更为 branch_name 分支 -m: move
git branch -m [old_name] [new_name] 
# 重命名分支 
git config --global init.defaultBranch main
# 初始化仓库时默认使用 main 作为名称

git switch [branch_name]
# 切换到其他分支

git merge [branch_name]
# 将其他分支合并到当前分支

git rebase [branch_name]
# 将其他分支变基到当前分支

git remote
# 显示当前远程仓库的名称
git remote -v
# 显示远程仓库的详细信息 -v: verbose
git remote add [remote_name] [remote_url]
# 添加 [remote_name] 为 [remote_url] 的名称
git remote set-url [remote_name] [url]
# 切换远程仓库的url

git 
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

```bash
ssh -T -p 443 git@github.com
# for windows
# or
ssh -T  git@github.com
# are you sure you want to continue connecting (yes/no/[fingerprint])? 
# 输入 yes
# 提示成功后就能 git push
```
# 小报错
```bash
warning: in the working copy of 'ansi.md', LF will be replaced by CRLF the next time Git touches it
# 检测到换行符不是windows风格而是unix风格, 这个警告仅仅是提醒, 一般都能继续正常工作
```
```bash
git push 
```
后提示
> git@github.com's password:  
解决方法:  
在确保ssh密钥成功应用后
尝试
```bash
ssh -T -p 443 git@ssh.github.com
```
能通过则在`~/.ssh/config`中添加
```bash
Host github.com
Hostname ssh.github.com
Port 443
User git
```
