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
		const m = "abc"	//在不同作用域定义同名常量
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

* 作用域



