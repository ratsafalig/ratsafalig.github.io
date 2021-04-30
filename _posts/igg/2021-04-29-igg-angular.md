---
title: Angular
tags:
- IGG
---


所有以 ng-xxx 开头的都是 angular 处理的元素  
所有的 angular 元素必须闭包在 ng-app 内部  
单个页面默认只有一个 ng-app  

```html
<div ng-app="...">
    <p>\{\{ expression \}\}</p>
</div>
```

ng-app 标记的标签可以有 ng-init 标记, 用来标记初始化值:  

```html
<div ng-app="..." ng-init="a=1;b=2;c='...';d={d1:'d1',d2:'d2'};e=[1,2,3]">
    <p>
        \{\{ expression \}\}
        \{\{ a + b \}\}
        \{\{ a * b \}\}
        \{\{ d.d1 \}\}
        \{\{ e[0] \}\}   
    </p>

    // 数据绑定 (IOC)
    <input ng-model="a">
    <input ng-model="b">

    // 重复元素
    <div ng-repeat="x in e">
        \{\{ x \}\}
    </div>

    // 自定义指令
    // app.directive 必须驼峰命名
    // 使用时候必须使用连接号, 例如 my-directive 来使用标签
    <script>
        var app = angular.module("myApp", []);
        app.directive("myDirective", function(){
            return {
                template : "<h1>asdasd</h1>"
            };
        })
    </script>

    // 限制必须为 A 表示只能通过 HTML 属性的方式调用
    // restrict :
    // - A 只能作为属性
    // - C 只能作为类名
    // - E 只能作为元素名
    // - M 只能作为注释
    <script>
        var app = angular.module("myApp", []);
        app.directive("myDirective", function(){
            return {
                restrict : "A",
                template : "<h1>123123</h1>"
            }
        })
    </script>
</div>

// 设置 controller

<div ng-app="myApp" ng-controller="myController">
    <input ng-model="name">
</div>

<script>
    var app = angular.module("myApp", []);
    app.controller("myController", function($scope){
        $scope.name = "123123"
    })
</script>

// 验证邮箱

<form ng-app="" name="myForm">
    // ng-model 名字随意, 但是必须存在, 因为只有 ng-model 绑定后才能被 angular 处理绑定的数据
    <input type="email" name="myAddress" ng-model="myApp">
    // 只有 ng-show 为 true 的时候才会显示
    // 内置的变量有
    // $error
    // - email
    // - 
    // $valid 是否是有效值
    // $dirty 是否被修改过
    // $touched 是否被触屏点击到
    <span ng-show="myForm.myAddress.$error.email">不是一个合法的邮箱地址</span>
</form>
```

过滤器

```html
<p>
    // 全大写 同理 lowercase
    {{ abc | uppercase }}

    // 过滤器有:
    // - currency 转换成货币格式
    // - orderBy: '...' 例如 for x in xs | orderBy:'asd'
    // - filter 过滤输入
</p>
```

