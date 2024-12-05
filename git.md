## git rm
```sh
git rm $file
# 删除指定的文件, 标记为已删除

git rm --cached $file
# 将文件标记为已删除, 但是不会删除文件
```
## git branch?

# command
```bash
git switch [branch_name]

git merge [branch_name]

git rebase [branch_name]

git remote
git remote -v
# verbose
git remote add [remote_name] [remote_url]
git remote set-url [remote_name] [url]
```
## git config
```sh
git config --global -e
git config --global http.sslverify false
git config --global sslCAInofo /path/to/crt
```
# 配置 ssh 密钥
* 在用户根目录下创建 .ssh目录

* 在目录中输入 
```bash
ssh-keygen
```
```bash
ssh -T -p 443 git@github.com
# for windows
# or
ssh -T  git@github.com
# are you sure you want to continue connecting (yes/no/[fingerprint])? 
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
在`~/.ssh/config`中添加
```bash
Host github.com
IdentityFile ~/.ssh/${somefile}
Hostname ssh.github.com
Port 443
User git
```
