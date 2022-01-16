ubuntu安装 libxml2

ubuntu下golang下载libxml2 报错信息:

```
$ go get -u github.com/lestrrat-go/libxml2                    
# pkg-config --cflags  -- libxml-2.0
Package libxml-2.0 was not found in the pkg-config search path.
Perhaps you should add the directory containing `libxml-2.0.pc'
to the PKG_CONFIG_PATH environment variable
No package 'libxml-2.0' found
pkg-config: exit status 1


```

因为系统少了个libxml2 开发包:

使用以下命令即可修复:

```
sudo apt install libxml2-dev
```

