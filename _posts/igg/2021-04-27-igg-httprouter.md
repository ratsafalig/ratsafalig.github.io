---
title: HttpRouter
tags:
- IGG
---

# quickstart

```go
func handler(w http.ResponseWriter, r * http.Request, p httprouter.Params){
    ...
}
router := httprouter.New()

router.GET("/", handler)

/**
 Pattern: /user/:user
 /user/gordon              match
 /user/you                 match
 /user/gordon/profile      no match
 /user/                    no match
 */
router.GET("/:name", handler)

/**
 Pattern: /src/*filepath
 /src/                     match
 /src/somefile.go          match
 /src/subdir/somefile.go   match
 */
router.GET("/*name", handler)
```

# http.Handler

```go
import "net/http"

func handler(w http.ResponseWriter, r * http.Request){
    // 方式1
    param1 := httprouter.ParamsFromContext(r.Context())
    // 方式2
    param2 := r.Context().Value(httprouter.ParamsKey)
    
    // 自动 OPTIONS 
    router.GlobalOPTIONS = http.HandlerFunc(func (w http.ReponseWriter, r * http.Request){
        if r.Header.Get("Access-Control-Request-Method") != "" {
            // Set CORS headers
            header := w.Header()
            header.Set("Access-Control-Allow-Methods", header.Get("Allow"))
            header.Set("Access-Control-Allow-Origin", "*")
        }

        // Adjust status code to 204
        w.WriteHeader(http.StatusNoContent)
        })
    ...
}
```
