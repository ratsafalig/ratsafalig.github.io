---
title: HttpRouter
tags:
- IGG
---

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

func handler2(w http.ReponseWriter, r * http.Request){
    
}
```