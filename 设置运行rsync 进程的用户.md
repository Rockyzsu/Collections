安装及配置
安装运行：

yum -y install rsync  
#启动rsync服务
systemctl start rsyncd.service
systemctl enable rsyncd.service

#检查是否已经成功启动
netstat -lnp|grep 873
1
2
3
4
5
6
7

好了，好了。安装成功。

配置：
首先，配置文件在：
/etc/rsyncd.conf

vim /etc/rsyncd.conf
1
看到：



好了，先修改成：

 uid = root                              
 # //设置运行rsync 进程的用户
 gid = root
 use chroot = no
 max connections = 4
# pid file = /var/run/rsyncd.pid        
#//CentOS7中yum安装不需指定pid file 否则报错
 lock file=/var/run/rsyncd.lock
 log file = /var/log/rsyncd.log     
 # //此文件定义完成后系统会自动创建
 exclude = lost+found/
 transfer logging = yes
 timeout = 900
 ignore nonreadable = yes         
 # //同步时跳过没有权限的目录
 dont compress   = *.gz *.tgz *.zip *.z *.Z *.rpm *.deb *.bz2          
 #  //传输时不压缩的文件
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17


重启：

systemctl restart rsyncd.service
1
两个服务器间传输文件
好了，上面配置完rsync了，那么接下来，假设有两台服务器，开发服务器dev及线上测试环境test，现在需要从dev将可运行代码更新到test上面去。

注意：每一次传输文件客户端将告诉服务端需要调用哪个传输规则进行传输，而传输规则如下：

[simba]          //此名字即客户端使用rsync来同步的路径
path=/usr/local/simba    //实际需要同步的路径
comment=simba    //和中括号里名字一样就行
ignore errors
read only=no   //表示可以pull 
write only=no      //表示可以push
list=no
auth users=rsyncuser    //客户端获取文件的身份此用户并不是本机中确实存在的用户
secrets file=/etc/rsyncd.passwd     //用来认证客户端的秘钥文件 格式 USERNAME:PASSWD 此文件权       
                                                        //限一定需要改为600，且属主必须与运行rsync的用户一致。
hosts allow=*    //允许所有主机访问
1
2
3
4
5
6
7
8
9
10
11
好了，我们自己做一个规则，假定test上面接收的目录是： /data/www/helloRsync


#创建目录
mkdir  /data/www/helloRsync
1
2
3
4
而dev上面也是。。。
请自行创建。
那么在test上面的/etc/rsyncd.conf添加规则：

#规则名称，作为测试用规则，直接用这个算了。
[helloRsync]          
#同步的路径
path=/data/www/helloRsync    
#规则描述
comment=测试规则
ignore errors
#是否可以pull
read only=no    
#是否可以push
write only=no      
list=no
#下面配置同步时候的身份，注意该身份是在rsync里面定义的，并非是本机实际用户。等下说说如何在rsync里面定义身份。
#客户端获取文件的身份此用户并不是本机中确实存在的用户
auth users=rsyncuser    
#//用来认证客户端的秘钥文件 格式 USERNAME:PASSWD 此文件权     
#//限一定需要改为600，且属主必须与运行rsync的用户一致。  
secrets file=/etc/rsyncd.passwd                                                             
#允许所有主机访问
hosts allow=*    
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20


给rsync定义身份，如下：

echo 'rsyncuser:123456'>/etc/rsyncd.passwd   //文件用户名和路径为上面定义，别写错，密码自己定
chmod 600 /etc/rsyncd.passwd        //修改权限
1
2
重启服务。

systemctl restart rsyncd.service
1
客户端的配置

1。创建密码。

echo '123456' >>/etc/rsyncd-test.passwd     //注意这里只需要服务器rsyncd.passwd 中的密码
chmod 600 /etc/rsyncd-test.passwd
1
2
为了测试顺利，我们添加一些文件进行同步，譬如：

echo 'test,hello'>> /data/www/helloRsync/readme.txt
1
2
好了，同步：

rsync -auv --password-file=/etc/rsyncd-test.passwd rsyncuser@120.x.x.x::helloRsync /data/www/helloRsync/   
1


看看服务器上面对应目录



检查原因



test上面看日志：

vim  /var/log/rsyncd.log 
1
2


好了，



auth user 是错的，要用 auth users，也是醉了，都没发现吗？

改过以后重启rsync服务，在尝试

得到：



name or service not kunown

据查这不是问题，怀疑，是rsync命令问题，应该是将test的文件下载下来了，于是将目录调换一下顺序，得到：

rsync -auv --password-file=/etc/rsyncd-test.passwd  /data/www/helloRsync/ rsyncuser@120.x.x.x::helloRsync 
1
报错：


好了，是没有放开权限：




放开以后重启终于成功了。泪流满面。坑爹丫。

一份真实环境用的更新脚本demo

src="/usr/local/webroot/java-web-bld"
rsync -rauvvt --progress \
--password-file=/etc/rsyncd-test.passwd \
--exclude="console/data" \
--exclude=".svn" \
--exclude="WEB-INF/logs" \
--exclude="res/upload" \
--exclude="WEB-INF/upload" \
--exclude="WEB-INF/temp" \
--exclude="env.properties" \
/usr/local/webroot/java-web-bld/ rsyncuser@xxx.xx.xx.xxx::backend
————————————————
版权声明：本文为CSDN博主「码农下的天桥」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/cdnight/article/details/78861543