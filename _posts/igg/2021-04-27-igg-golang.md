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

```