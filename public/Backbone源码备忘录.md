# Backbone 源码备忘录

## 概览

### 闭包结构

带两个参数的自执行函数

```
(function(root, factory) {
	// 兼容环境	
}(this, function(root, Backbone, _, $) {
	// Backbone 各模块实现
}))
```

* 参数一为全局变量
* 参数二为Backbone函数体，形参包含全局变量、Backbone顶级变量、underscore、$(DOM选择器)

函数体判断当前执行环境

1. 兼容AMD规范，并依赖于underscore, jqquery, exports
2. 兼容CommonJS规范，并依赖于underscore
3. 作为浏览器全局变量

### factory结构

顶层定义了基本变量

* `previousBackbone`
* 基本array方法`push`,`slice`,`splice`
* 版本号
* `Backbone.noConflict` method
* `Backbone.emulateHTTP`用来兼容比较旧的HTTP服务器(不支持patch, put, delete)
* `Backbone.emulateJSON`用来兼容不支持`applicatin/json`的请求

中间是各模块的实现以及工具函数

* Events
* Model
* Collection
* View
* sync
* ajax
* Router
* History
* extend
* *error

## 模块详解

### Backbone.Events

#### Type

`Object`

#### Methods

| 方法名        | 参数列表         | 返回值 |
| :-------------:|:-------------:| :-----:|
| on           | name, callback, context | this |
| once   | name, callback, context     |   this|
| off | name, callback, context      |    this |
| trigger | name|    this |
| stopListening | obj, name, callback  |    this |

#### Functions

| 函数名        | 参数列表         | 返回值 |
| :-------------:|:-------------:| :-----:|
| eventsApis | obj, action, name, rest | boolean |
| triggerEvents| events, args     | - |
