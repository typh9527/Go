# 基础类型

## 变量

* 基础用法

```go
var x int
```

* 命名多变量

```go
var (
    x, y int
    a, s = 100, "abc"
)
```

* 赋值

简短模式，存在缺点，定义变量必须初始化，不能指定数据类型，只能在函数内部使用，定义必须使用。

```go
z := 100
z, m := 200, 300
//先计算右边
res1, res2 := z+1, m+50
```

* 规范

推荐驼峰式，首字母大写为导出成员，首字母小写只能在包内使用（private）

## 常量

* 用法示例

```go
const (
    i int = 1
    t                            //默认和上一个命名相同类型和相同赋值

    b = false
    strSize = len("hello world") //可以进行计算赋值
    num1 = iota
    num2
    num3
)
func main(){
    const m = 123 //未使用不会引起错误
    {
        const m = "abc"    //在不同作用域定义同名常量
        println(m)
    }
    println(m)
    println(t)
    print(num1,num2,num3)
}
```

* iota

常量计算器，只能在常量的表达式中使用

```go
fmt.Println(iota)     //错误用法
```

每次出现const时都会将iota初始化为0

```go
const a = iota //0
const (
    b = iota //0
    c        //1
)
```

跳过某些值

```go
type AudioOutput int
const (
    OutMute AudioOutput = iota //0
    OutMono                 //1
    OutStereo               //2
    _
    _
    OutSurround             //5
)
```

中间插队

```go
const (
    i = iota //0
    j = 3.14 
    k = iota //2
    l        //3
)
```

掩码表达式

```go
type Allergen int

const (
    IgEgg Allergen = 1<<iota //1<<0 00000001
    IgChocolate             //1<<1 0000010
    IgNuts
    IgStrawberries
    IgShellfish
)
```

隐性重复最后一个非空的表达式列表

* 作用域

```go
var cwd string

func init() {
    cwd, err := os.Getwd()
    if err != nul {
        log.Fatalf("os.Getwd:%v".err)
    }
}
```

这段程序中，目的是给cwd全局变量赋值，而由于cwd和err在init的词法块中都没有声明过，所以:=会将它们声明为本地变量。虽然err因为未被调用而报错，但是如果在其他情况中调用了err，则无法发现这个错误。为了避免这种风险，尽量不要使用:=.

正确的程序

```go
var cmd string

func init() {
    var err error
    cwd, err = os.Getwd()
    if err != nil {
        log.Fatalf("os.Getwd failed: %v",err)
    }
}
```

## 基本类型

数值，浮点，字符串，布尔，数组及错误类型

传递副本

## 引用类型

切片，字典，接口，函数类型，通道

传递标头值，底层结果并没有被复制，所以高效。

```go
package main

import (

)

func main() {
    a := make([]int, 3)
    a[1] = 10
    
    b := new([]list)
    b[1] //报错
```

new为引用类型分配零值内存并返回指针

make为其分配内存初始化结构并返回对象

```go
package main

import (

)

func mkslice() []int {
	s := make([]int,0,10)
	s = append(s,100)
	return s
}

func mkmap() map[string]int {
	m := make(map[string]int)
	m["a"] = 1
	return m
}

func main() {
	m := mkmap()
	println(m["a"])

	s := mkslice()
	println(s[0])
}
```



