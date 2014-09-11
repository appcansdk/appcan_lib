#简介

appcanLib 是appcan根据自己的需求封装的一个开发库，对底层的接口进行更高层的封装，能让开发者更快速、
高效的开发更加稳定的项目，该库依赖backbonejs、zeptojs、underscorejs默认打包在基础库中，开发者
不需要进行额外的引用，另外在该库的基础上提供了丰富的插件，能让开发者更高效的开发app。

#框架说明

appcan前端整体框架     
![appcan 前端框架](http://ww4.sinaimg.cn/mw690/8dd3f635jw1ek8e36xm89j20yq0omdih.jpg)

#使用说明

在项目开发中你只需引入`dist/appcan.min.js`文件在你的项目中即可，该文件是系统自动根据源文件构建的包
含了文件的所有依赖，然后按照常用的开发流程，进行后续的开发，具体细节参考后续相关文档说明。

##appcan核心模块

appcan基础模块提供了一套管理整个`appcanlib`的方法

###appcan.define(name,function(){})

创建一个新模块
`appcan.define(name,defineCall)`    
`name`:要创建的模块名   
`defineCall`:创建模块的函数，执行该函数时会传人三个参数，第一个参数是zepto对象，第二个是要导出的模
块的引用的副本，第三个是要导出模块对象，其中的`exports`对象就是要导出到来的引用点。

###appcan.extend(obj,[obj])
扩展对象，如果只有一个参数则会把参数扩展到appcan自己上。例如`appcan.extend({showVersion:function(){return this.version;}})`
会给appcan增加一个`showVersion`方法，可以直接调用`appcan.showVersion()`获取当前appcan库的版本号。    
`obj`：要扩展的对象   
`[obj]`:如果第二个参数不为空，会把第二个参数扩展到第一个参数上，并返回扩展后的值    

###appcan.require(name)

引用一个模块   
`name`:要获取模块的名称,返回对应的模块

###appcan.use(name,funCall)

引用对应的模块进行后续开发    
`name`:模块名   
`funCall`:回调函数，第一个参数默认传入`dom`对象即`zepto`对象，第二个参数是前面要使用的模块名对象，模块名可以是数组，如果参数是数组，回调
中会把数组格式化好按照顺序添加到回调的后续参数中

###appcan.isString(obj)

判断指定的对象是否是`String`类型   
`obj`:要判断类型的对象   

###appcan.isArray(obj)

判断指定的对象是否是`Array`（数组）类型    
`obj`:要判断类型的对象  

###appcan.isFunction(obj)

判断指定的对象是否是函数类型    
`obj`:要判断类型的对象

###appcan.isPlainObject(obj)

判断指定的类型是否是朴素`Object`对象
`obj`:要判断类型的对象   

###appcan.ready(funCall)

在appcan内部插件可用后执行内部的回调函数    
`funCall`:内部插件全部准备好后执行该函数

###appcan.inherit(parent,proto,staticProps)

创建一个新的类继承执行的父类     
`parent`:要继承的父类     
`proto`:子类的新方法如果要添加新的属性则需要实现`initated`方法   
`staticProps`:子类的静态属性通过这个对象实现   

##appcan基础类库
appcan整个框架依赖的基础库

###appcan.dom类库
参考[zetpo.js](http://zeptojs.com/ "zetpojs")类库，用法一致 

###appcan.Backbone类库
参考[Backbone.js](http://backbonejs.org "Backbone.js")类库，用法一致

###appcan._类库
参考[underscore.js](http://underscorejs.org "underscore.js")类库，用法一致

###appcan.underscore类库
参考[underscore.js](http://underscorejs.org "underscore.js")类库，用法一致 

###appcan.logs(msg)
把日志输出到控制台    
`msg`:要打印到控制台的消息

##appcan crypto模块
包含了加密相关的模块，目前提供了`rc4`加密模块

###appcan.crypto.rc4.rc4Init(key)
根据指定的`key`生成扰乱后的`s-box`   
`key`:要加密的字符串`key`   

###appcan.crypto.rc4.rc4Encrypt(content,sbox)

根据给定的内容和sbox进行rc4加解密    
`content`:要加解密的内容   
`sbox`:根据`key`生成的`sbox`   

###appcan.crypto.rc4.rc4EncryptWithKey(key,content)

根据指定的`key`，把指定的`content`进行rc4加解密    
`key`:要进行加解密的`key`   
`content`:要加解密的内容   

##appcan database 模块
该模块包含了appcan对数据库的基础操作   

###appcan.database.create(name,[optId],callback)
创建一个数据库
`name`:要创建的数据库名    
`optId`:创建数据库用的操作id,可为空     
`callback(err,data,db,dataType,optId)`:数据库创建成功后的回调，如果创建过程中有错误
`err`不为空，否则`err`为空，`data`返回的执行结果，`db`是数据库创建成功后的数据库对象，可
以执行相关的操作，`dataType`返回结果的数据类型，`optId`操作Id   

 
`db.select(sql,callback)`:用返回的数据库对象，进行查询操作，`sql`要查询用的sql语句，`callback`查询
返回的结果回调，同样的`callback(err,data,dataType,optId)`第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id     


`db.exec(sql,callback)`:用返回的数据库对象，进行更新操作，`sql`要更新用的sql语句，`callback`是更新
返回的结果回调，同样的`callback(err,data,dataType,optId)`第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id     


`db.transaction(sqlFun,callback)`:用返回的数据库对象，进行更新操作，`sql`要更新用的sql语句，`callback`是更新
返回的结果回调，同样的`callback(err,data,dataType,optId)`第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id     



###appcan.database.select(name,sql,callback)






    







