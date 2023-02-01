---
title: Ubuntu中连接GitHub
date: 2023-01-25 12:50:12
tags: Linux配置
---
在b站听课missing semester的时候，在Ubuntu中尝试使用git报错fatal，于是发现，噢天呐，我在干什么，只有bash连接过github，linux还没有连接过怎么可能不报错呢。遂老老实实配置环境。  
记录下来的目的是让自己以后再安装能快速成功。上次丢了vscode的配置真的哭了......
借鉴大神CSDN
<!-- more -->
## 01.配置
#### Step1 查看Git版本
```bash
root@zhang-PC: git version
git version 2.25.1
```
显示出版本即已安装，若未安装
```bash
root@zhang-PC: sudo apt-get install git
```
#### Step2 配置Git用户信息
```bash
root@zhang-PC: git config --global user.name "username"
# 输入自己的GitHub用户名
root@zhang-PC: git config --global user.email "xxx@xxx.com"
# 输入自己GitHub上用的邮箱
```
没有出现任何提示也没有任何报错是正常的，敲Enter继续就行了。
## 02.创建Secure Shell
#### Step3 安装ssh
需要sudo权限
```bash
root@zhang-PC: sudo apt-get install ssh
```
#### Step4 检查
生成SSH KEY之前，为了防止混淆，可以查看系统里是否已经存在密钥
```bash
# 查看key是否存在
root@zhang-PC: ls -al ~/.ssh

total 20
drwx------  2 root root 4096 Jan  25 10:25 .
drwxr-xr-x  4 root root 4096 Jan  25 10:30 ..
-rw-------  1 root root 2655 Jan  25 10:19 id_rsa
-rw-r--r--  1 root root  572 Jan  25 10:19 id_rsa.pub
-rw-r--r--  1 root root  444 Jan  25 10:31 known_hosts
# 打开key所在位置
root@zhang-PC: cd ~/.ssh
# 防止混淆，删除所有key
root@zhang-PC: rm *

root@zhang-PC: cd ..
```
#### Step5 生成全新的SSH KEY
RSA通常是先生成一对RSA密钥，一个是私钥，由用户保存；另一个为公钥，可对外公开，甚至可在网络服务器中注册。RSA密钥一般推荐使用1024位
```bash
root@zhang-PC: ssh-keygen -t rsa -C "xxx@xxx.com"
# 之前配置相同的邮箱地址

Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): /root/.ssh/id_rsa
# /root/.ssh/id_rsa是默认地址，直接输入就可以
Enter passphrase (empty for no passphrase): 
# 屏幕不会显示任何东西
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa
# 密钥
Your public key has been saved in /root/.ssh/id_rsa.pub
# 公钥
The key fingerprint is:
SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx test@gmail.com
The key's randomart image is:
+---[RSA 1000]----+
| xxxxxxxxxxxxxx  |
|o +..=.* * ..o   |
| B..+ =.X =  .   |
|xxxxxxxxxxxxx    |
|..= a o Axxx     |
| E o o           |
|. o .            |
| \               |
|.                |
+----[SHA256]-----+
```
#### Step6 查看SSH PUBLIC KEY
```bash
#进入key存储目录
root@zhang-PC: cd ~/.ssh
 
#查看当前目录所有的文件
root@zhang-PC: ls -a        
.  ..  id_rsa  id_rsa.pub  known_hosts
 
 
#读取public key公钥
root@zhang-PC: cat id_rsa.pub

```
#### Step7 复制SSH PUBLIC KEY
可能是我的问题，我到现在还不知道在Ubuntu终端界面怎么复制粘贴，Ctrl+Shift+C和Ctrl+Shift+V它不好用啊啊啊...  
于是，来到root/.ssh路径下，使用记事本打开id_rsa.pub，然后复制就舒服多了哈哈哈。
#### Step8 操作GitHub
- 登录GitHub
  GitHub打不开是家常便饭，所以可能需要科学上网~
- 点击右上角头像Setting选项
- 进入Account Setting界面
- 左侧列表点击SSH and GPG keys选项
-  点击SSH keys右边绿色（New SSH key）的按钮
-  跳转到新页面将你复制的内容（id_rsa.pub）粘贴到Key的文本框中，Title可以随便取，建议写清表示这是Ubuntu的连接，windows的bash还会连接一个
-  点击绿色（Add SSH key）按钮
- 页面会跳转回之前的界面，如果成功会显示一串字符（SHA256算法加密的身份验证），可以看到这串字符和之前创建ssh时的fingerprint是完全一致的
到此为止，Linux就可以通过SSH建立本机Git和Github的连接了（下载与传输）
- 补充一步：在git中输入命令：ssh -T git@github.com，然后会跳出一堆话。。输入命令：yes，回车，然后就会提示你成功了~~
## 03.库的下载
#### Step1 在Github上建立一个新的Repository
#### Step2 创建后可以点击选项栏SSH，会出现一个URL地址，把它复制下来
#### Step3 回到Ubuntu，把它拷贝下来
```bash
root@zhang-PC: git clone git@github.com:rObberT93/test.git
```
#### Step4 找到这个文件夹
这个test文件夹会出现在和root同级的目录下。
```bash
# 进入克隆到本地的文件夹
root@zhang-PC: cd test
 
# 命令管理一组跟踪的库，查看关联状态
root@zhang-PC: git remote -v
 
origin  git@github.com:rObberT93/test.git(fetch)
origin  git@github.com:rObberT93/test.git(push)
```
## 04.文件的推送修改与上传
#### Step 1 接下来我们可以尝试创建一个readme.md文件
```bash
#用vim编辑器创建并打开readme.md
root@zhang-PC: vim README.md
```
敲入Hello World，保存退出(Esc :wq)。
可以cat一下看一看。
#### Step 2 将本地内容上传到Github
注：如果你克隆的不是自己仓库，你将没有权限进行任何推送或修改
```bash
#将文件添加到暂存区
root@zhang-PC: git add README.md
 
#提交修改
root@zhang-PC: git commit -m "add readme file"
 
On branch master
Your branch is up to date with 'origin/master'.
 
nothing to commit, working tree clean
                                        
 
#推送到远程仓库
root@zhang-PC: git push origin master
 
Everything up-to-date
```
#### Step 3 回到浏览器，刷新你的Github
进入之前创建的test库，可以看到readme.md文件已经存在了，内容显示 Hello World
# final！成功！