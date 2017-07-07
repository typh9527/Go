# 概述

## 命令简介

* go get:获取远程包 
* go run:直接运行程序
* go build：测试编译，检测是否有编译错误
* go fmt：格式化源码
* go install 编译包文件并运行
* go test ：运行测试文件
* go doc：查看文档

## 基础知识普及

* 第一行必须是package 必须要有main

```
 package std fmt //别名调用 std == fmt,但二者不能混用
```

* import 导入的报名，多个用（）而不是{}

* const 常量定义
* var 全局变量
* type 一般类型声明
* type gogo struct{} 结构的声明
* type golang interface{} 接口声明
* func main\(\){} 主函数 必须有

## 编程基础

* 函数名首字母**小写，**即为private
* 函数名首字母**大写，**即为public

## 基本语法

### 基本类型

* bool
* int/unint
* int8/unint8
* byte\(unit8\)
* float32/float64
* complex64/complex128\(复数\)
* uintptr\(保存指针\)
* slice、map、chan（高并发）
* interface
* func

\#\#\#变量声明



\`\`\`

var x int32 //默认为0值，不是空值，bool默认false，字符串默认空字符串

var x = "hello world"

\`\`\`

省略var

\`\`\`

x := 100 //注意赋值符号差别

\`\`\`

\#\#\#表达式

仅有三种流控制语句

\* if

\`\`\`

if x

&gt;

0 {

} else if x

&lt;

0 {

} else {

}

\`\`\`

\* switch

\`\`\`

switch {

```
case x 
```

&gt;

0:

```
    cmd




case x 
```

&lt;

0:

```
    cmd

default:

    cmd
```

}

\`\`\`

\* for

\`\`\`

for i := 0;i

&lt;

5; i++ {

```
cmd
```

}

for {            //相当于while（True）

```
cmd




if {




    break




}
```

}

\`\`\`

\#\#\#函数

\#\#\#\#基本的函数使用

\`\`\`

package main

import \(

```
"errors"

"fmt"
```

\)

func div\(a, b int\)  \(int, error\) {    \这里定义了输入的函数类型和输出的函数类型

```
if b == 0 {

    return 0, errors.New\("division by zero"\)

}

return a / b , nil
```

}

\`\`\`

函数可以被作为一个参数或者一个返回值

\`\`\`

func test\(x int\) func\(\) {

```
return func\(\) {    //匿名函数

    println\(x\)        //闭包

}
```

}

func main\(\) {

```
x := 100

f := test\(x\)

f\(\)
```

}

\`\`\`

匿名函数\[^1\]

闭包\[^2\]

\#\#\#\#defer解析

用defer定义延迟调用,无论是否出错都在返回前调用

\`\`\`

package main

func test\(a, b int\) {

```
defer println\("dispose ..."\)




println\(a / b\)
```

}

func main\(\) {

```
test\(10, 0\)
```

}

\`\`\`

首先明确的是defer是在return之前执行。与C语言不同，go是用栈返回的，c是用寄存器。\*return 并不是一条原子指令\*\[^4\]

&gt;

return = 赋值指令 + CALL defer指令 + RET指令

简单范例

原始代码

\`\`\`

```
func f() (r int) {
    defer func(r int) {
          r = r + 5
    }(r)
    return 1
}
```

```

```

等效代码

    \`\`\`

func f\(\) \(r int\) {  
     r = 1  //给返回值赋值  
     func\(r int\) {        //这里改的r是传值传进去的r，不会改变要返回的那个r值  
          r = r + 5  
     }\(r\)  
     return        //空的return  
}

```

```

```
所以结果为1
```

\#\#\#数据

1.切片（slice）

类似动态数组

\`\`\`

x ：= make\(\[\]int,0,5\)     //创建容量为5的切片

for i := 0;i

&lt;

8; i++ {

```
 x = append\(x,i\)         //追加数据，当超出容量限制时，自动分配更大的存储空间
```

}

\`\`\`

2.字典（map）

类型内置，可以直接从运行时层面获得性能优化

\`\`\`

func main\(\) {

```
m := make\(map\[string\]int\)     //创建字典类型




m\["a"\] = 1




x,ok := m\["b"\]    //使用ok-idiom获取值，可知道key/value是否存在

fmt.Println\(x,ok\)




delete\(m,"a"\)    //删除
```

}

\`\`\`

3.结构体（struct）

\`\`\`

type user struct {

```
name string




age byte
```

}

type manager struct {

```
user        //嵌入其他类型




title string
```

}

\`\`\`

\#\#\#方法

1.为\*\*包内的任意类型\*\*定义方法

\`\`\`

package main

type X int

func \(x \*X\) inc\(\) {

```
\*x++
```

}

func main\(\) {

```
var x X




x.inc\(\)




println\(x\)
```

}

\`\`\`

2.直接调用匿名字段，类似继承

\`\`\`

package main

import func\(

```
"fmt"
```

\)

type user struct {

```
name string




age byte
```

}

func \(u user\) ToString\(\) string {

```
return fmt.Sprintf\("%+v",u\)
```

}

type manager struct {

```
user




title string
```

}

\`\`\`

\#\#\#接口

\`\`\`

type user struct {

```
name string




age byte
```

}

func \(u user\) Print\(\) {

```
fmt.Printf\("%+v\n",u\)
```

}

type Printer interface {

```
Print\(\)
```

}

func main\(\) {

```
var u user




u.name = "Tom"




u.age = 29




var p Printer = u




p.Print\(\)
```

}

\`\`\`

\#\#\#并发

1.基础实现

\`\`\`

func task\(id int\) {

```
...
```

}

func main\(\){

```
go task\(1\)                //创建goroutine




go task\(2\)







time.Sleep\(time.Second \* 6\)
```

\`\`\`

2.通道（channel）与goroutine搭配，实现进程间通信

\`\`\`

//消费者

func consumer\(data chan int,done chan bool\) {

```
for x := range data{        //接收数据，直到通道被关闭




    println\("recv:",x\)




}




done 
```

&lt;

* true

}

//生产者

func producer\(data chan int\) {

```
for i := 0; i 
```

&lt;

4;i++ {

```
    data 
```

&lt;

* i        //发送数据

```
}




close\(data\)        //生产结束，关闭通道
```

}

func main\(\) {

```
done := make\(chan bool\)    //用于接收消费者结束信号




data := make\(chan int\)     //数据通道







go comsumer\(data,done\)    //启动消费者




go producer\(data\)    //启动生产者
```

&lt;

-done

}

\`\`\`

\[^1\]:就是没有函数名的函数。

\[^2\]:闭包就是能够读取其他函数内部变量的函数,闭包可以简单理解成“定义在一个函数内部的函数“。在本质上，闭包是将函数内部和函数外部连接起来的桥梁。不要用的太多，会消耗大量内存。

\[^3\]:这个地方还是比较难懂的，附上一个教程辅助了解一下\[链接\]\(

[http://studygolang.com/articles/2593\)](http://studygolang.com/articles/2593%29)

\[^4\]:

所谓原子操作是指不会被线程调度

机

制打断的操作；这种操作一旦开始，就一直运行到结束，中间不会有任何 context switch。

