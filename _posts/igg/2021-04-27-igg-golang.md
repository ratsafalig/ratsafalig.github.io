---
title: GoLang
tags:
- IGG
---

# quickstart

- `go get github.com/gin-gonic/gin`
- 创建一个文件夹, 运行 `go mod init`
- 在 `go.mod` 添加 `require github.com/gin-gonic/gin v1.7.1`
- 在代码里添加 `import 'github.com/gin-gonic/gin'`

# 控制流

```go
if a < 20{
    ...
}
else if a < 25{
    ...
}
else{
    ...
}

/*********************/

for i := 1; i < 3; i++{
    ...
    continue
    ...
    break
}

/*********************/

switch a{
    case 1: 
    ...
    case 2: 
    ...
    fallthrough
    case 3: 
    ...
    default:
    ...
}
```

# 调用

## 函数

```go
func function(param1 int, param2 string) int{
    return 123
}
```

## 方法

```go
type receiver struct{
    ...
}

/*******************/

func (receiver type) method(param1 int, param2 string)int{
    return 123
}

/**
GO 语言参数传递全部为值传递
下面对 receiver 的修改可以改变实际值, 因为参数以地址实参的形式传进来
*/
func (receiver * type)method(param1 int)int{
    
    return 123
}
```

## 多返回值

```go
func function(param1 int)(return1 int, return2 int){
    return 1,2
}
/*******************/
a, b := function(123)
```

## 闭包

```go
func function() func()int{
    return func(){
        return 123
    }
}
```

# 指针

```go
var i = 123
var * j = &i

```

## 数组

```go
var arr[4]int {1,2,3,4}

/**
 不确定数组的长度
*/
var arr[...]int{1,2,3,4,5}

var i int = arr[0]
```

# 变量

```go
type asd struct{
    i int
    j string
}

var a asd = asd{1,"123"}

a.i
a.j
```

# 切片 & 范围 & 集合

```go
/**
 数组和索引的区别, 必须使用 make 函数创建一个索引

 len 为 length
 cap 为 capacity

 使用 append 函数扩充切片时, 总长度必须小于 cap
*/
slice1 := make([]type, len, cap)

var i := slice1[1:3]

append(slice1, 1, 2, 3)

slice2 := make([]type, len, cap * 2)

copy(slice1, slice2)
```

## 范围

```go
var i = ... //切片, 数组, 通道, 集合

for idx, data := range i{
    ...
}
```

## 集合

```go
var m map[key_type]val_type
m = make(map[key_type]val_type)

m["123"]="123"

/* 删除元素 */

delete(m, key)
```

# 接口

```go
type name interface{
    method1() return1
    method2(param1 int)string
}
```

# 错误处理

```go
type error interface{
    Error() string
}

/****************************/

func f()int, error{
    if ...{
        return 0, errors.New("...")
    }
}   
```

# 并发

## 线程

```go
go funcname(param1)return1{
    ...
}
```

## 通道

```go
// 使用 make(chan int) 创建一个通道
ch := make(chan int)
// 使用 <- 从通道中传递数据
// 把 v 传递到通道中
ch <- v
// 把通道中的数据传递到 v 中
v := <-ch

// !! 默认情况下,通道是同步的 !!
// !! 带缓冲区的通道是异步的 !!
ch := make(chan int, 100)

// 通道使用 close 关闭
ch := make(chan int, 100)
close(ch)
```

# defer

[defer](https://draveness.me/golang/docs/part2-foundation/ch05-keyword/golang-defer/)

```go
// 使用 defer 调用函数可以暂时将函数缓存起来继续执行,等到手头结束之后再执行 defer 函数
func main() {
	for i := 0; i < 5; i++ {
		defer fmt.Println(i)
	}
}
// 输出如下
$ go run main.go
4
3
2
1
0
```