## 树莓派使用USB摄像头和motion实现监控

***\**\*顶\*\**\***

本文同步至个人博客：cyang.tech

# 一、工具

- 1、树莓派3B
- 2、USB摄像头

# 二、操作步骤

- 1、安装motion

```
1sudo apt-get install motion
2
```

- 2、配置motion

(1)

```
1sudo nano /etc/default/motion
2
```

将里面的no修改成yes，让motion可以一直在后台运行：start_motion_daemon=yes

(2)

```
1sudo nano /etc/motion/motion.conf
2
```

修改配置文件，这个文件比较长，请确保一下参数的配置。在nano编辑器下，可以使用^w快速查找到如下配置内容。也可以使用^v向下翻页。

- 3、启动motion

```
1sudo motion
2
```

- 4、查看视频数据

在局域网内的设备，不管是手机还是电脑，均可打开浏览器访问树莓派IP:8081

- 5、退出motion

```
1killall -TERM motion
2
```

或者

```
1service motion stop
2
```

# 三、可能出现的问题

- 1、配置错误

出现Unknown config option "sdl_threadnr"
解决方法：
在配置文件中，直接将这一行内容进行注释。不是下图光标所在处，是光标下面sdl_threadnr 0这一行，注释成# sdl_threadnr 0即可。

- 2、8081页面无法显示

在8081端口，无法显示数据，但是在8080端口可以看到motion的信息。
**解决方法：**
这可能是摄像头没有被识别，可以将摄像头拔下重新插入。