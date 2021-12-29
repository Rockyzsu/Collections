# ubuntu终端Git中文乱码

csdn_yuan88 2019-04-04 21:42:56  2677  收藏 2
分类专栏： 技术_主机系统软件 文章标签： ubuntu git github 中文乱码
版权
ubuntu终端Git中文乱码：200\273\347\273\223
使用git add添加要提交的文件的时候，显示形如2200\273\347\273\223乱码。 
解决方案：git config --global core.quotepath false

