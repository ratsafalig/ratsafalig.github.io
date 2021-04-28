---
title: HttpRouter
tags:
- IGG
---

# quickstart

```go
func handle(w http.ResponseWriter, r * http.Request, p httprouter.Params){
    ...
}
router := httprouter.New()

router.GET("/", handle)

/**
 Pattern: /user/:user
 /user/gordon              match
 /user/you                 match
 /user/gordon/profile      no match
 /user/                    no match
 */
router.GET("/:name", handle)

/**
 Pattern: /src/*filepath
 /src/                     match
 /src/somefile.go          match
 /src/subdir/somefile.go   match
 */
router.GET("/*name", handle)
```

# 变量

```go
type paramsKey struct{}

var ParamsKey = paramsKey{}
```

# 函数

```go
func CleanPath(p string)string
func ParamsFromContext(ctx context.Context) Params
func New() *Router
```

# 类型

```go
type Handle func(http.ResponseWriter, * http.Request, Params)

type Param struct {
	Key   string
	Value string
}

func (ps Params) ByName(name string) string

type Router struct{
    RedirectTrailingSlash bool
    RedirectFixedPath bool
    HandleMethodNotAllowed bool
    HandleOPTIONS bool
    GlobalOPTIONS http.Handler
    NotFound http.Handler
    MethodNotAllowed http.Handler
    PanicHandler func(http.ResponseWriter, * http.Request, interface{})
}

/**
RESTful
*/
func (*Router) DELETE(path string, handle Handle)
func (*Router) GET(path string, handle Handle)
func (*Router) HEAD(path string, handle Handle)
func (*Router) POST(path string, handle Handle)
...

func (*Router) Handle(method, path string, handle Handle)

/**
查看 httprouter 的 mod 文件,发现没有依赖任何包
但是依然可以使用 http.Handler
原因是 net/http 是核心类库
*/
func (*Router) Handler(method, path string, handler http.Handler)

func (*Router) HandlerFunc(method, path string, handler http.HandlerFunc)
func (*Router) Lookup(method, path string)(Handle, Params, bool)

/**
将一个文件夹映射到一个URL
router.ServeFiles("/src/*filepath", http.Dir("/var/www"))
*/
func (*Router) ServeFiles(path string, root http.FileSsytem)

func (*Router) ServeHTTP(w http.ResponseWriter, req * http.Request)
```