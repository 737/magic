
如何修改git push时的密码
===========================

###如下:
* 打开git bash
* 输入 `$ cd ~/.ssh`
* `$ ls` 确定有 *id_rsa* 和 *id_rsa.pub*文件
* `$ ssh-keygen -p -f id_rsa`
* 第一次输入旧密码
* 新密码
* 确认新密码

###说明
对于上面的 `ssh-keygen -p -f id_rsa`这命令是为什么？ 可以参考下面的连接

[SSK-KEYGEN](http://www.manpager.com/linux/man1/ssh-keygen.1.html)
