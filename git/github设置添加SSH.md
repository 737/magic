#github设置添加SSH

很多朋友在用github管理项目的时候，都是直接使用https url克隆到本地，当然也有有些人使用 SSH url 克隆到本地。然而，为什么绝大多数人会使用https url克隆呢？

这是因为，使用https url克隆对初学者来说会比较方便，复制https url 然后到 git Bash 里面直接用clone命令克隆到本地就好了。而使用 SSH url 克隆却需要在克隆之前先配置和添加好 SSH key 。

因此，如果你想要使用 SSH url 克隆的话，你必须是这个项目的拥有者。否则你是无法添加 SSH key 的。

##https 和 SSH 的区别：

* 前者可以随意克隆github上的项目，而不管是谁的；而后者则是你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。
* https url 在push的时候是需要验证用户名和密码的；而 SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。

##在 github 上添加 SSH key 的步骤：

1. 首先需要检查你电脑是否已经有 SSH key 运行 git Bash 客户端，输入如下代码：
	+ `$ cd ~/.ssh`
	+ `$ ls`
	+ 这两个命令就是检查是否已经存在 id_rsa.pub 或 id_dsa.pub 文件，如果文件已经存在，那么你可以跳过步骤2，直接进入步骤3。


2. 创建一个 SSH key
	+ `$ ssh-keygen -t rsa -C "your_email@example.com"`
	+ 代码参数含义：-t 指定密钥类型，默认是 rsa ，可以省略。-C 设置注释文字，比如邮箱。-f 指定密钥文件存储文件名。
	+ 以上代码省略了 -f 参数，因此，运行上面那条命令后会让你输入一个文件名，用于保存刚才生成的 SSH key 代码，如：


`Generating public/private rsa key pair.`
'# Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter]`

当然，你也可以不输入文件名，使用默认文件名（推荐），那么就会生成 id_rsa 和 id_rsa.pub 两个秘钥文件。



接着又会提示你输入两次密码（该密码是你push文件的时候要输入的密码，而不是github管理者的密码），

当然，你也可以不输入密码，直接按回车。那么push的时候就不需要输入密码，直接提交到github上了，如：


`Enter passphrase (empty for no passphrase): 
# Enter same passphrase again:`

接下来，就会显示如下代码提示，如：


`Your identification has been saved in /c/Users/you/.ssh/id_rsa.
# Your public key has been saved in /c/Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com`

当你看到上面这段代码的收，那就说明，你的 SSH key 已经创建成功，你只需要添加到github的SSH key上就可以了。

3、添加你的 SSH key 到 github上面去
a、首先你需要拷贝 id_rsa.pub 文件的内容，你可以用编辑器打开文件复制，也可以用git命令复制该文件的内容，如：


`$ clip &lt; ~/.ssh/id_rsa.pub`

b、登录你的github账号，从又上角的设置（Account Settings）进入，然后点击菜单栏的 SSH key 进入页面添加 SSH key。

c、点击 Add SSH key 按钮添加一个 SSH key 。把你复制的 SSH key 代码粘贴到 key 所对应的输入框中，记得 SSH key 代码的前后不要留有空格或者回车。当然，上面的 Title 所对应的输入框你也可以输入一个该 SSH key 显示在 github 上的一个别名。默认的会使用你的邮件名称。

4、测试一下该SSH key

在git Bash 中输入以下代码


`$ ssh -T git@github.com`

当你输入以上代码时，会有一段警告代码，如：


`The authenticity of host 'github.com (207.97.227.239)' can't be established.
# RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
# Are you sure you want to continue connecting (yes/no)?`

这是正常的，你输入 yes 回车既可。如果你创建 SSH key 的时候设置了密码，接下来就会提示你输入密码，如：


`Enter passphrase for key '/c/Users/Administrator/.ssh/id_rsa':`

当然如果你密码输错了，会再要求你输入，直到对了为止。

注意：输入密码时如果输错一个字就会不正确，使用删除键是无法更正的。

密码正确后你会看到下面这段话，如：


`Hi username! You've successfully authenticated, but GitHub does not
# provide shell access.`

如果用户名是正确的,你已经成功设置SSH密钥。如果你看到 “access denied” ，者表示拒绝访问，那么你就需要使用 https 去访问，而不是 SSH 。



如果你有什么疑问，请留言。



产考文档：https://help.github.com/articles/generating-ssh-keys

