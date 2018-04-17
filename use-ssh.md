# 同时配置多个ssh，windows操作如下：
## 1.生成一个公司用的SSH-Key
> $ ssh-keygen -t rsa -C "first-email@company.com” -f ~/.ssh/id-rsa

## 2.生成一个github用的SSH-Key
> $ ssh-keygen -t rsa -C "second-email@github.com” -f ~/.ssh/github-rsa

## 3.添加私钥
> $ ssh-add ~/.ssh/id-rsa
>
> $ ssh-add ~/.ssh/github-rsa

如果执行ssh-add时提示”Could not open a connection to your authentication agent”，可以先执行命令:
> $ ssh-agent bash

然后再运行ssh-add命令。
可以通过 ssh-add -l 来确私钥列表
> $ ssh-add -l

可以通过 ssh-add -D 来清空私钥列表
> $ ssh-add -D

## 4.修改配置文件
若.ssh目录下无config文件，那么创建
> touch ~/.ssh/config 

### 添加以下内容
<blockquote>
# gitlab  

Host gitlab.com  
    HostName gitlab.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id-rsa
</blockquote>

<blockquote>
# github  

Host github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/github-rsa  
</blockquote>

## 5.测试
> $ ssh -T git@gitlab.com

配置无误，应该输出类似信息：
> Welcome to GitLab, your name!

# 关于配置config
>Host	别名  
>   HostName		主机名  
>   Port			端口(端口没修改可以不填写该行)  
>   User			用户名  
>   IdentityFile	密钥文件的路径  