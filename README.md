Github RSA Key Generating Demo
==============================

生成公私钥
--------

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

它会生成好相应的公私钥。

但需要注意的是，它给出的保存路径(`~/.ssh/id_rsa`)很可能文件已经存在，请千万注意不要覆盖已有的，否则如果没有备份好的话，就找不回来了。

可以给它输入一个不同的路径，在这个例子中，让它直接生成在当前目录下：`./id_rsa`

```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/freewind/.ssh/id_rsa): ./.ssh/id_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ./id_rsa.
Your public key has been saved in ./id_rsa.pub.
The key fingerprint is:
SHA256:E/12mXrZhy5nDLpcOe29TERoMyruc2tqPnKPM4Rb758 your_email@example.com
The key's randomart image is:
+---[RSA 4096]----+
|                 |
|         .    .  |
|        . .  = . |
|         . .o +o |
|        S. .o +. |
|       ..+...=.+ |
|        +...=o=.o|
|       o.Oo=.=B..|
|        ==&=oEooo|
+----[SHA256]-----+
```

把公钥copy到github设置中
-----------------

然后把生成的公钥`id_rsa.pub`的内容copy到github中:

![github-add-key1](./images/github-add-key1.jpg)

![github-add-key2](./images/github-add-key2.jpg)

把私钥放在本地
------------

同时把生成的私钥`id_rsa`放到本机的`~/.ssh`下，可以使用原名，也可以换个名字方便记忆。

修改私钥权限，否则无法使用：

```
chmod 400 ~/.ssh/id_rsa
```

注意该私钥需要绝对保密，不应该泄露给任何人。

~/.ssh/config
-------------

为了可以使用key来与github交互，还需要在`~/.ssh`下创建一个`config`文件，内容如下：

```
Host github.com
    User git
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa
```

