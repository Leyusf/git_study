#### SSH协议：

SSH是Secure Shell（安全外壳协议）缩写，是目前较为可靠的，专为远程登录会话和其他网络服务提供安全性的协议。

本地git仓库和远程仓库之间的传输通过SSH加密，则必须要远程仓库服务器认证SSH key，在此之前必须要生成SSH key。

使用SSH协议时，需要为自己创建一对密钥（公钥和私钥），并把公钥放到要访问的服务器上。

#### 配置SSH协议：

##### 未配置SSH：

```
$ git clone git@gitee.com:red_coated_leaves/network-cw2.git
Cloning into 'network-cw2'...
The authenticity of host 'gitee.com (180.97.125.228)' can't be established.
ECDSA key fingerprint is SHA256:FQGC9Kn/eye1W8icdBgrQp+KkGYoFgbVr17bmjey0Wc.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'gitee.com,180.97.125.228' (ECDSA) to the list of known hosts.
git@gitee.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

报错：权限被拒绝。

可以使用GitBash生成公钥和私钥。

1.使用命令 `ssh-keygen-t rsa`生成公钥和私钥，执行完成后出现 C:\Users\用户名\\.ssh。

```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/zly/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/zly/.ssh/id_rsa.
Your public key has been saved in /c/Users/zly/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:1jxpxlelreb8rXppWpK+cKRcSt/k5ojFTTqxEmLcPZY zly@LAPTOP-QOH779PM
The key's randomart image is:
+---[RSA 3072]----+
|                .|
|               + |
|              o .|
|       . = o o . |
|        S % E =  |
|       o * % /   |
|          * @ O. |
|           B B+..|
|          . **o.o|
+----[SHA256]-----+
```

一直回车就可以。

2.复制公钥文件内容至服务器。

（1）码云配置：

​				设置->安全设置->SSH公钥。

```
$ git clone git@gitee.com:red_coated_leaves/network-cw2.git
Cloning into 'network-cw2'...
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 1), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (14/14), 37.59 KiB | 938.00 KiB/s, done.
Resolving deltas: 100% (1/1), done.
```

可以克隆成功。

（2）GitHub配置：

​				setting->SSH and GPG keys->new SSH。