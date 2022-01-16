# IDE安装教程

## 安装教程

### 1.官网下载专业版

打开官网:

```markdown
https://www.jetbrains.com/pycharm/download/#section=windows
```

选择你的平台,如果你是Windows,选择Windows,Mac选择Mac.

如图所示,点击专业版下载:

![image-20211205143554475](https://billy.taoxiaoxin.club//img/202112051435582.png)

### 2.安装

找到下载好的安装包,右键以管理员身份运行.

![image-20211205144235843](https://billy.taoxiaoxin.club//img/202112051442908.png)

选择是

![image-20211205144606399](https://billy.taoxiaoxin.club//img/202112051446473.png)

点击NEXT

![image-20211205144724158](https://billy.taoxiaoxin.club//img/202112051447226.png)

选择安装路径,点击NEXT.

![image-20211205144823445](https://billy.taoxiaoxin.club//img/202112051448505.png)

勾选桌面快捷方式,点击NEXT.

![image-20211205144947424](https://billy.taoxiaoxin.club//img/202112051449499.png)

直接点击安装即可

![图片](https://billy.taoxiaoxin.club//img/202112051451065.webp)

等待安装完成之后,勾选启动Pycharm.

![image-20211205145704003](https://billy.taoxiaoxin.club//img/202112051457070.png)

## 激活IDE

**重要提示:**如果之前激活IDEA时，修改过Host文件，请删除Host中的相关配置

### 1.下载插件

下载激活插件:

```markdown
https://txx.lanzouw.com/iH3Ugx9t07i
```

下载的文件包含：

- reset_script （如果你已经过了30天试用期，可以使用这个重置）
- 激活码
- 补丁Jar文件

### 2.打开Pycharm

然后在桌面双击pycharm运行。第一次运行的话就无需导入，直接点击ok。

![图片](https://billy.taoxiaoxin.club//img/202112051506573.webp)

### 3.注册账号登录

以前的pycharm30天是不需要登录的,但是现在出现了注册登录

首先没有账号的小伙伴还是要先**注册/登录**一下，先免费试用30天

注册登录账号几分钟就搞定了

![image-20211205151311024](https://billy.taoxiaoxin.club//img/202112051513115.png)

当然,它是支持第三方登录注册的,如果有GitHub账号的用户直接可以使用GitHub账号登录注册.

![image-20211205151712886](https://billy.taoxiaoxin.club//img/202112051517989.png)

这里我使用的我GitHub账号登录

![image-20211205151907855](https://billy.taoxiaoxin.club//img/202112051519002.png)

#### 温馨提示:

如果你之前登录过并且试用期30天已经过了，**请解压 reset_script.zip 文件**

> **解压之后会看到下面两个文件，根据自己的操作系统执行对应文件即可**

windows点击运行文件：`reset_jetbrains_eval_windows.vbs`

Mac / Linux  执行：`reset_jetbrains_eval_mac_linux.sh`

### 4.免费试用

登录成功之后，点击 **Start Trial** **,开始免费试用**

![image-20211205152122912](https://billy.taoxiaoxin.club//img/202112051521002.png)

### 5.创建项目

首先随便创建一个项目,点击`New Project`

![image-20211205152755650](https://billy.taoxiaoxin.club//img/202112051527743.png)

选择你的项目创建路径和本地Python解释器.

![image-20211205152941187](https://billy.taoxiaoxin.club//img/202112051529268.png)

![image-20211205153132772](https://billy.taoxiaoxin.club//img/202112051531851.png)

最后点击`create`

![image-20211205153228019](https://billy.taoxiaoxin.club//img/202112051532122.png)

### 6.开始激活

复制激活插件**FineAgent.jar**到你安装pycharm的路径下.

![image-20211205154217567](https://billy.taoxiaoxin.club//img/202112051542628.png)

新建一个idea的文件夹

![image-20211205154404752](https://billy.taoxiaoxin.club//img/202112051544812.png)

粘贴激活插件文件`FineAgent.jar`到`idea`文件夹下.

![image-20211205154545412](https://billy.taoxiaoxin.club//img/202112051545475.png)

#### 温馨提示

如果你忘记了你的pycharm安装路径在哪里,可以点击pycharm快捷方式--->右键---->点击打开文件所在位置.

![image-20211205154951219](https://billy.taoxiaoxin.club//img/202112051549307.png)

返回到目录`PyCharm 2021.3`下

![image-20211205155129199](https://billy.taoxiaoxin.club//img/202112051551273.png)

进入到IDEA项目开发界面（`默认情况下，需要创建一个项目或者打开一个项目，才能进入到这个页面`）

点击如图所示的菜单：`Help - > Edit Custom VM Options...`。修改`idea64.exe.vmoptions`文件。

![image-20211205153707749](https://billy.taoxiaoxin.club//img/202112051537034.png)

点击按钮，会打开`idea64.exe.vmoptions`文件。

![image-20211205153842636](https://billy.taoxiaoxin.club//img/202112051538789.png)

然后到刚刚的`idea`文件夹并复制文件夹路径.

![image-20211205160022532](https://billy.taoxiaoxin.club//img/202112051600631.png)

在`idea64.exe.vmoptions`文件中添加，这样一段话

`-javaagent:文件路径\FindAgent.jar`

示例:

```markdown
# FindAgent.jar 的文件路径
-javaagent:F:\Program Files\JetBrains\PyCharm 2021.3\idea\FineAgent.jar
```

![image-20211205160341723](https://billy.taoxiaoxin.club//img/202112051603792.png)

然后保存，重启Pycharm.

重启之后，又会重新进入到激活页面，这个时候，我们选择`Activate IntelliJ IDEA`

![image-20211205162746965](https://billy.taoxiaoxin.club//img/202112051627050.png)

找到激活文件里面的激活码

![image-20211205162906996](https://billy.taoxiaoxin.club//img/202112051629139.png)

![image-20211205162921802](https://billy.taoxiaoxin.club//img/202112051629895.png)

打开文件,全选复制

![image-20211205163003785](https://billy.taoxiaoxin.club//img/202112051630887.png)

回到Pycharm激活页面,粘贴激活码,点击激活按钮.

![image-20211205163217727](https://billy.taoxiaoxin.club//img/202112051632829.png)

恭喜你！成功激活到 2099 年！！！

![image-20211205163541824](https://billy.taoxiaoxin.club//img/202112051635929.png)