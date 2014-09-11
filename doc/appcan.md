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


`db.transaction(sqlFun,callback)`:用返回的数据库对象，进行事务操作，`sqlFun`要执行用的sql语句序列函数，
`callback`是事务返回的结果回调，同样的`callback(err,data,dataType,optId)`第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id     


###appcan.database.select(name,sql,callback)
在指定的数据库上执行查询操作   
`name`:要查询的数据库名    
`sql`:要执行sql查询语句    
`callback(err,data,dataType,optId)`:第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id    

###appcan.database.exec(name,sql,callback)
在指定的数据库上执行更新操作   
`name`:要更新的数据库名    
`sql`:要执行sql更新语句    
`callback(err,data,dataType,optId)`:第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id    

###appcan.database.transaction(name,sqlFun,callback)
在指定的数据库上执行事务操作   
`name`:要执行事务的数据库名    
`sqlFun`:要执行sql序列函数    
`callback(err,data,dataType,optId)`:第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id    

###appcan.database.destory(name,[optId],callback)
销毁已经创建的数据库    
`name`:要销毁的数据库名称    
`optId`:可选，销户数据库的操作id   
`callback(err,data,dataType,optId)`:第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id    


##appcan detect模块
该模块包含了一下浏览器基础能力的监测    

###appcan.detect.browser
浏览器相关信息    
`appcan.detect.browser.version`:浏览器版本号   
`appcan.detect.browser.name`:当前浏览器名称   
`appcan.detect.browser.ie`:是否是ie   
`appcan.detect.browser.chrome`:是否是chrome   
`appcan.detect.browser.android`:是否是android   
`appcan.detect.browser.iphone`:是否是iphone   
`appcan.detect.browser.ios`:是否是ios   
`appcan.detect.browser.ipad`:是否是ipad   
`appcan.detect.browser.ipod`:是否是ipod   
`appcan.detect.browser.wp`:是否是wp   
`appcan.detect.browser.webos`:是否是webos   
`appcan.detect.browser.touchpad`:是否是touchpad   
`appcan.detect.browser.blackberry`:是否是blackberry   
`appcan.detect.browser.bb10`:是否是bb10   
`appcan.detect.browser.rimtabletos`:是否是rimtabletos   
`appcan.detect.browser.playbook`:是否是playbook   
`appcan.detect.browser.kindle`:是否是kindle   
`appcan.detect.browser.silk`:是否是silk   
`appcan.detect.browser.firefox`:是否是firefox   
`appcan.detect.browser.safari`:是否是safari   
`appcan.detect.browser.webview`:是否是webview   


###appcan.detect.os
操作系统相关信息    

`appcan.detect.os.name`:操作系统名称   
`appcan.detect.os.version`:操作系统版本号  
`appcan.detect.os.phone`:是否是手机    
`appcan.detect.os.tablet`:是否是平板    

###appcan.detect.events
关于事件的支持情况

`appcan.detect.events.supportTouch`:是否支持touch事件
   
###appcan.detect.css
关于css的支持情况    

`appcan.detect.css.support3d`:是否支持3d  

###appcan.detect.ua
当前浏览器的ua信息   


##appcan device
appcan设备相关模块

###appcan.device.vibrate(millisecond)
使设备震动    
`millisecond`:设备震动的时常 单位毫秒   

###appcan.device.cancelVibrate()
停止设备震动    

###appcan.device.getInfo(infoId,callback)
获取设备对应id的信息    
`infoId`:相关信息id   
> 0. `0`: 描述CPU频率的字符串，eg：“1024MHZ”。IOS平台获取不到时，返回“0”     
> 1. `1`: 描述系统版本的字符串，eg：“Android2.3.4”   
> 2. `2`:标书设备制造商的字符串eg:“htc”    
> 3. `3`:代表是否支持键盘的字符串0（不支持）或1（支持）    
> 4. `4`:代表是否支持蓝牙的字符串0（不支持）或1（支持）  
>     当设备有蓝牙功能时，即使蓝牙关闭，返回信息仍然是支持蓝牙，即值为字符串1。    
>     在IOS上的蓝牙功能只支持同一应用间使用，和普遍人们理解的不同，视为不支持。   
> 5. `5`:代表是否支持WIFI的字符串0（不支持）或1（支持）   
当设备有wifi功能时，即使wifi关闭，返回信息仍然是支持wifi，即值为字符串1。   
> 6. `6`:代表是否支持摄像头的字符串0（不支持）或1（支持)    
> 7. `7`:代表是否支持GPS的字符串0（不支持）或1（支持）   
>     当设备有gps功能时，即使gps关闭，返回信息仍然是支持gps，即值为字符串1。    
> 8. `8`:代表当前移动网络数据连接是否可用（不含WIFI）的字符串0（不可用）或1（可用）    
> 9. `9`:代表设备是否支持触屏的字符串0（不支持）或1 （支持）    
> 10. `10`:代表此设备IMEI（国际移动设备唯一标识码）号的15位字符串，eg：“356357046156042”。  
>      在IOS上，获得不到imei时可获得UUID，eg:“dea7f0e2f8c7dfd0c07555b96aff2d342587505b”    
> 11. `11`:推送服务器需要的一个代表此设备的唯一令牌的字符串。   
>      eg：“98d264a3 77689b33 6f1215e6 264ab0c5 55f45b4a ab61e6ff f667883a ef829ccb”,没有时返回空字符串。
>      Android的deviceToken是softToken。   
> 12. `12`:设备类型，用来判断当前的设备是phone	ouch或者pad(IOS专用，类型值参考常量表IOS设备类型)    
> 13. `13`:当前联网的方式(类型值参考常量表网络状态类型)     
> 14. `14`:当前设备剩余的磁盘空间大小的字符串，eg：“12345678”单位：字节	   
>15. `15`:当前移动网络运营商的名称，比如”中国联通”,如果获取不到返回空字符串    
>16. `16`:表示当前设备的WIFI mac地址 ，可作为设备的唯一标识，IMEI可能在某些不具备移动通讯的android平板或MP4上获取不到，但是android系统设备一般都会具有WIFI功能，所以mac地址作为设备唯一标识比IMEI更可靠   
>17. `17`:当前设备的型号名称，如“Galaxy Nexus”   

`callback(err,data,dataType,optId)`:第一个参数是`Error`对象如果为空则表示
没有错误，否则表示操作出错了，`data`表示返回的操作结果,`dataType`操作结果的数据类型，`optId`该操作id    

###appcan.device.getDeviceInfo(callback)
获取所有相关的设备信息   
`callback(deviceInfo,singleInfo,i,len,completeCount)`:`deviceInfo`当前已经获得的设备信息
`singleInfo`正在读取的设备信息 `i`设备信息id `len`设备信息总数 `completeCount`已经获得的设备信息数

##appcan eventEmitter事件模块
关于事件自定义模块，如果想让你的某一个模块具有事件能力请将该对象扩展到你的目标对象上,该对象本身不能单独使用
例如：`appcan.on('error',function(){})`当appcan捕获到错误的时候就会执行该方法。

###appcan.eventEmitter.on(name,callback)
具有自定义事件能力的对象绑定一个函数到指定的名字中   
`name`:要绑定的事件名   
`callback`:当事件被调起时，会执行该回调函数，参数是触发该事件触发者传入的，具体根据情况不同   

###appcan.eventEmitter.off(name,callbakc)
移除已经绑定到对应名称的回调函数    
`name`:要移除的事件名   
`callback`:该事件名对应的函数句柄   

###appcan.eventEmitter.once(name,callback)
执行完绑定的事件后，自动移除对应的事件    
`name`:要移除的事件名   
`callback`:该事件名对应的函数句柄     

###appcan.eventEmitter.addEventListener(name,callback)
`name`:要绑定的事件名   
`callback`:当事件被调起时，会执行该回调函数，参数是触发该事件触发者传入的，具体根据情况不同   

###appcan.eventEmitter.removeEventListener(name,callback)
移除已经绑定到对应名称的回调函数    
`name`:要移除的事件名   
`callback`:该事件名对应的函数句柄  

###appcan.eventEmitter.trigger(name,context,[args,...])
触发绑定的对应的事件    
`name`:对应的事件名称   
`context`:


   











