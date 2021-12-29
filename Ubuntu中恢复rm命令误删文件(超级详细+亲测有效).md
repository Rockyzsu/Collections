# Ubuntu中恢复rm命令误删文件(超级详细+亲测有效)

置顶 2019年05月27日 11:13:12 [rain_Man2018](https://me.csdn.net/weixin_44038165) 阅读数 40

 

在实验室做项目时使用的是ubuntu16.04

某次开发时打字太快从而误删除别的文件，而且还是很重要的文件，ubuntu没有像windows一样的回收站，因此删完就没了，只能通过其他办法恢复。

### 第一步：进入误删除文件的目录内，查看被删文件的挂载分区

如 cd /home/conference 进入到conference目录，原来的误删除的文件处于此目录内

使用df -h命令查看此目录的挂载分区，如/dev/sda1是误删文件所在的分区

### 第二步： 安装恢复工具extundelete

使用命令： sudo apt-get install extundelete

### 第三步：恢复文件

使用命令： sudo extundelete /dev/sda1 --restore-all

通过以上三步骤后，会在当前目录中生成一个名为RECOVERED_FILES目录，并且将恢复的文件放到这个目录中，然后自己去一个一个找需要用到的文件。

