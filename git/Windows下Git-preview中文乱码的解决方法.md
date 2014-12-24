
##Windows下Git-preview中文乱码的解决方法


在Windows下安装Git-preview-1.7.4后，使用中发现许多的乱码问题，感觉甚是不便。这是因为Git是在linux下开发的管理软件，而linux的编码方式是基于UTF-8的，所以移植到Windows之后难免会存在编码方式不同的情况，所以极易产生乱码。即便如此，也是有解决方案的，方法如下：（以下假设Git-preview的安装路径为D:\Git）

###1. 在Git Bash提示符下，使用git add添加含有中文的新文件时乱码（乱码类似：\316\304\261\276\316\304\265\265.txt）。

解决方案： 编辑D:\Git\etc\inputrc文件中对应的行： 查找以下2行，并修改其值：

原先：

`set output-meta off`

`set convert-meta on`

改为：

`set output-meta on`

`set convert-meta off`

###2. 在Git Bash提示符下，使用git log查看含有中文的log信息时乱码（乱码类似：<E4><BF><AE><E6><94><B9><E6><96><87><E6><9C><AC><E6><96><87><E6><A1><A3>）。

解决方案： 在Bash提示符下输入：

`git config --global i18n.commitencoding utf-8`

`git config --global i18n.logoutputencoding gbk`

注：设置commit提交时使用utf-8编码，可避免Linux服务器上乱码；同时设置在执行git log时将utf-8编码转换成gbk编码，以解决乱码问题。

编辑D:\Git\etc\profile文件，添加如下一行：

`export LESSCHARSET=utf-8`

注：以使git log可以正常显示中文（需要配合：i18n.logoutputencoding gbk）。

3.在Git Bash提示符下，使用ls命令查看含有中文的文件名乱码（乱码类似：????.txt）。

解决方案： 使用ls --show-control-chars命令来强制使用控制台字符编码显示文件名，即可查看中文文件名。

为了方便使用，可以编辑D:\Git\etc\git-completion.bash文件，添加如下一行： alias ls="ls --show-control-chars"

###4. 在Git Gui中查看UTF-8编码的文本文件时乱码（乱码类似：锘夸腑鏂囨枃妗￡）。

解决方案： 在Bash提示符下输入：

`git config --global gui.encoding utf-8`

注：通过上述设置，UTF-8编码的文本文件可以正常查看，但是GBK编码的文件将会乱码，所以还是没有从根本上解决问题。

可行的方法之一为：将所有文本文件的编码统一为UTF-8或GBK，然后设置相应的gui.encoding参数为utf-8或gbk。