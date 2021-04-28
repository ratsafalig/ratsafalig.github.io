---
title: Go net/http
tags:
- IGG
---

# quickstart

## 发送请求

```go
import "net/http"

resp, err := http.Get("...")
...
resp, err := http.Post("...", "image/jpeg", &buf)
...
resp, err := http.PostForm("...", url.Values{"key" : {"..."}, "id" : {"..."}})
...
```

## IO流关闭

```go
resp, err := http.Get("...")
if err != nil {
    // handle err
}
defer resp.Body.Close()
body, err := io.ReadAll(resp.Body)
```

## 改变 Header

```go
client := &http.Client{
	CheckRedirect: redirectPolicyFunc,
}
resp, err := client.Get("http://example.com")
// ...
req, err := http.NewRequest("GET", "http://example.com", nil)
// ...
req.Header.Add("If-None-Match", `W/"wyzzy"`)
resp, err := client.Do(req)
// ...
```

## 更改传输层配置

```go
tr := &http.Transport{
	MaxIdleConns:       10,
	IdleConnTimeout:    30 * time.Second,
	DisableCompression: true,
}
client := &http.Client{Transport: tr}
resp, err := client.Get("https://example.com")
```

## Controller

```go
/**
Handle 和 HandleFunc 的区别在于, 
fooHandler 必须自己实现接口
而 HandlerFunc 的参数只要一个同样签名的函数即可
*/
http.Handle("/foo", fooHandler)
http.HandleFunc("/bar", func(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, %q", html.EscapeString(r.URL.Path))
})

log.Fatal(http.ListenAndServe(":8080", nil))
```