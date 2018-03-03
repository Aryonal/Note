# Go lang

```go
package main

import "fmt"

func main() {
  fmt.Println("Hello World!")
}
```

[TOC]

## 一. 变量

### 1. 变量声明
一般变量声明格式
```go
var arr []int = [6]int{1,2,3,4,5,6}  //声明并初始化数组
var arr2 = [6]int{1,2,3,4,5,6}   //可以省略变量名后的类型声明，当变量类型可以由赋值语句判断，此处为 []int
var init_val int // 未赋值的变量设零值，init_val == 0
var init_arr [2][2]int //[[0 0] [0 0]]
```
同时可以用 `:=` 代替 `var =`:
```go
arr := [6]int{1,2,3,4,5,6}
num1 := 1 //int
num2 := 1.0 //float64
```

### 2. 类型

#### 显示类型转换

Go 中为显示类型转换，即不存在类似 C 中的 int, float64 等之间的隐式转换：
```go
a := 1
b := 2.0
//c := a*b //error
c := float64(a)*b //2.0
//or
d := a*int(b)     //2
```

#### 基本类型

```go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // uint8 的别名

rune // int32 的别名
     // 表示一个 Unicode 码点

float32 float64

complex64 complex128
```

### 3. 结构体 struct 与指针

定义结构体
```go
//整个表达式作为一个变量类型
struct {
  name1 Type
  name2 Type
  ...
}
```
一般都会跟 `type` 一起使用
```go
type vertex struct {
  x float64
  y float64
}

var v = vertex {1, 2} //{1 2}
var p = &vertex {1, 2} //&{1 2}

//指针重定向
fmt.Println(v.x) //1
fmt.Println((*p).x) //1
fmt.Println(p.x) //1
```
空指针无法重定向，即指针为零值，为 nil 时无法重定向。

与 C 中的指针基本相同，但是面对结构体时加了语法糖(?)重定向，基本逻辑是对于结构体指针 `p`，在访问其成员或方法时与 `(*p)` 等价。
**重定向**场景：
1. 访问成员
2. 访问方法

其余场景下无重定向，如参数传递时。

### 4. 接口 interface

接口概念同 Java 中类似，但是更加灵活，即不用显式 `implements` 一个接口，只要一个类型或结构体实现了接口定义的所有方法，就视作实现了这个接口。
需要注意的一点是，对于如下定义
```go
type I interface {
    f()
}
type S struct() {
    a int
}
func (s S)f() {
    //...
}
```
如下代码都是正确的
```go
var i I
var s = S{1}

i = s
i = &s
```
**但是** 如果方法的定义改成
```go
func (s *S)f() {
    //...
}
```
则接口无法接收结构体作为值传递
```go
var i I
var s = S{1}

//i = s // error
i = &s
```
原因猜测可能是为了保护 `s` 作为结构体而不是结构体指针的数据安全。

**nil接口**
当调用接口的主体为 nil 时，不会报错！并且传入 nil 。此处印证上面的说法，即接口只是 golang 的语法糖。nil 接口只针对对 `*Struct` 实现的方法，因为 `Struct` 无法 `convert to nil`，即不存在值为 nil 的 `Struct`，因为 `Struct` 的零值是所有成员零值的集合。
但是当接口没有指向特定结构体或类型时 nil 接口报错，因为没有明确的接口定义。

**空接口**
`interface{}` 可以保存所有类型的值，相当于 Java 中的 Object 类。


### 5. 数据结构 array, slice, map

#### 数组 array
```go
var arr = [6]byte{'g','o','l','a','n','g'} //[103 111 108 97 110 103]
```
数组间等号表示值传递而不是指针传递
```go
var arr = [5]int{1,2,3,4,5}
var arr2 = arr
arr[0] = 6
fmt.Println(arr)  //[6 2 3 4 5]
fmt.Println(arr2) //[1 2 3 4 5]
```
**切片的等号表示指针传递**

#### 切片 slice
```go
var init_slc []byte //nil
var slc = []byte{'g','o','l','a','n','g'} //[103 111 108 97 110 103]
var zero_slc = make([]byte, len, cap) // [0 0 0 ...]
var slc_of_arr = arr[1:] //[111 108 97 110 103]
```
切片有 len 和 cap 两个属性，即长度和容量。对于切片 s 和底层数组 a，s 的起止索引为 l, h，s 的大小为 N，则
```go
len(s) //h-l
cap(s) //N-l
```
切片的结构(瞎写的)
```go
//泛型T
type []T struct {
  p *T //head element
  len int
  cap int
}
```
为切片增加元素，可以使用内建方法 `append(slice []Type, elems ...Type)`，如果超过容量会自动扩容，生成一个新的底层数组。下文详解。
```go
slc = append(slc, ' ', 'i', 's', ' ', 'g', 'o', 'o', 'd') //[golang is good] in ascii
```
切片的复制可以用 `copy(dst []Type, src []Type)` 实现，开辟新的底层数组
```go
slc_cp := make([]byte, len(slc), cap(slc))
copy(slc_cp, slc)
```

二维切片
```go
import "math/rand"

var mat = make([][]int, dy)
for i := range 2dslc {
  mat[i] = make([]int, dx)
  for j := range 2dslc[i] {
    mat[i][j] = rand.Intn(100)
  }
}
```

#### 映射 map

```go
var init_map map[string]int //nil map
var zero_map = make(map[string]int) // empty map
//init_map["a"] = 1 //error
zero_map["a"] = 1 //map[a:1]

var m = map[string]int{
  "a":1,
  "b":2, //每一行都有逗号
}
```
增删查改
```go
//ADD
m["c"] = 3 //map["a":1 "b":2 "c":3]
//DEL
delete(m, "b") //map["a":1 "c":3]
//CHECK
value,ok := m["a"] //1,true
value,ok  = m["b"] //0,false
//MODIFY
m["a"] = 4 //map["a":4 "c":3]
```
关于增删查改的时间空间复杂度，还不知道。根据打印出的 map 中键的顺序随机排列来看，应该是由 hashmap 实现的。
```c
//TODO
```

### 6. 参数传递
- 基本类型：值传递
- array：值传递
- slice：**值传递**（传的是底层数组的指针）
- map：**指针传递**
- struct：值传递

## 二. 关键词

### 1. defer

```go
defer expr
```
`expr` 会在上层函数 return 之后运行。如果有多条 `expr` 所有 `expr` 压入 defer栈，并遵循后进先出原则执行

### 2. if

```go
if [expr;]expr {
  ...
  expr
  ...
}
```

### 3. for

```go
for [[expr1];]expr2[;[expr3]] {
  ...
  expr
  ...
}
```

### 4. switch

```go
switch [expr] {
  case expr1:
    ...
    expr
    ...
  case expr2:
    ...
    expr
    ...
  ...
}
```
其中 `switch true {}` 等于 `switch {}`

### 5. type

```go
type MyInt int
type vertex struct {
  x float64
  y float64
}
var a MyInt = 1
var b int = 2
// a + b //error, a 与 b 类型不同
c := int(a) + b
/**
 * MyInt 到 int 的类型转换是怎么实现的，以及 MyInt 类型的加法是怎么实现的?
**/
```

### 6. chan

```c
//TODO
```

## 三. 函数

### 1. 函数声明
```go
func fun_name(para1 Type, paras ...Type) ReturnType {
  ...
  expr
  ...
}
//or as Type
func(para1 Type, paras ...Type) ReturnType
```

### 2. 内建函数

```c
//TODO
```

make, len, cap, delete, append, copy

### 3. 方法 method

方法是绑定结构体或某种类型的函数，声明如下
```go
func (t Type)method_name(para1 Type, paras ...Type) ReturnType {
  ...
  expr
  ...
}
```
在调用时候可以
```go
var t Type
t.method_name(para1, ...paras)
```
其与函数等价

作为结构体的方法时，也存在指针重定向
```go
func (s *Struct)method1() {}
func (s Struct)method2() {}

var s = Struct{}
var p = &s
s.method1() //OK
p.method1() //OK
s.method2() //OK
p.method2() //OK
```
两种定义方式都是对 `Struct` 实现的方法。并且无法用相同名称命名对 `Struct` 与 `*Struct` 实现的方法，即 `func (s Struct)method()` 与 `func (s *Struct)method()` 无法同时定义。因为前者是值传递，不改变结构体本身成员属性，但后者可以改变成员属性。可以理解为 OOP 中的 `getter()` 与 `setter()`。

**但是** 在接口定义上，`(s Struct)` 与 `(s *Struct)` 是对两种不同 Type 的方法实现。只实现了 `func (s Struct)method()` 接口可以接受结构体与结构体指针作为值传递，而只实现 `func (s *Struct)method()` 接口只能接受结构体指针。



## 四. 闭包 closure
同函数式中的闭包相同，举一个例子
```go
package main

import "fmt"

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func() int {
	a := 0
	b := 1
	return func() int {
		a,b = b,a+b
		return b-a
	}
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}
```

## 五. 并发
