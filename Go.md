1. %v    只输出所有的值

2. %+v 先输出字段类型，再输出该字段的值

3. %#v 先输出结构体名字值，再输出结构体（字段类型+字段的值）

輸出結果分析
作为函数参数是值拷贝，在函数中slice的修改是通过slice中保存的地址对底层数组进行修改。但是删除操作，需要传递地址。
作为函数参数，当在函数中使用append增加切片元素的时候，就相当于创建一个新的变量。

## new
创建的是一个指针！

GO是一个前类型语言，不同类型之间不能进行赋值

不同类型的指针不能互相赋值，unsafe指针除外

写代码的书，最好不要在写完代码后，额外在代码其他地方写注释，最后在代码下面就写注释
----
struct 里面小写的字段，包外面是无法正常访问的。

指针的运算需要使用uintptr进行转换后才能相加，减
uintptr移动的单位是字节，8bit

---
＊＆ 成对出现就是抵消了。等于无

go继承C的结构体，而没有类的概念
面象现象特性： 封装

同一个包内的 小写 私有变量可以访问，包外就不可以了


GO 没有继承
用的是组合 has－a

继承是 is-a

空接口 断言
i.(T) i为空接口类型的变量，T为所需要的断言的类型

断言推荐 使用 
```
if value,ok:=i.(T);ok{
    
    }
```
这样，即使断言出错，也不会panic


# VS 类型判断
i.(type) type 是关键字
```
package main

import (
	"fmt"
)

type data interface{}
type Car struct {
	Color string
	Brand string
}

func main() {
	slice := make([]data, 3)
	slice[0] = 1                 // an int
	slice[1] = "Hello"           // a string
	slice[2] = Car{"Red", "BMW"} //a struct

	for i, v := range slice {
		//v.(type)不能在switch外的任何逻辑里面使用
		switch value := v.(type) {
		case int:
			{
				fmt.Printf("slice[%d] type is int[%d]\n", i, value)
			}
		case string:
			{
				fmt.Printf("slice[%d] type is string [%s]\n", i, value)
			}
		case Car:
			{
				fmt.Printf("slice[%d] type is Car [%s]\n", i, value)
			}
		default:
			{

			}
		}
	}
}

```
函数签名：不包含函数名，类型，返回值

方法签名： QA: 似乎签名里面 参数没有名称，返回也没有名称 ?
```
type IDrive interface{
    Drive() // 方法签名
    }
```

main函数本质是一个独立的主协程，如果主协程退出，则其他的协程即使还没有执行完，也将终止执行

反射的性能相对较低

切片的传参方式， 
func myfunc(args ...interface{}){
    
    Exec(args...) // 把他传进args

    }
    


性能测试工具
ipmort _ "net/khttp/pprof"

web: 127.0.0.1:8080/debug/pprof

生成的exe临时文集那
/tmp/go-build893595111/b001/exe/

压缩文件记得close，不然无法解压

