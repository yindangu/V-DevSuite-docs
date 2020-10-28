---
description: >-
  The official V-DevSuite SDK for JavaScript, available for browsers and mobile
  devices
---

# V-DevSuite JS SDK



{% hint style="info" %}
####  V-DevSuite JS SDK是[银弹谷](http://www.yindangu.net/module-operation!executeOperation?componentCode=yindangu_officialwebsite&windowCode=Form_Product_VDevSuite&&token=%7B%22data%22%3A%7B%22inputParam%22%3A%7B%22variable%22%3A%7B%22formulaOpenMode%22%3A%22locationHref%22%7D%7D%7D%7D)零代码开发平台面向web端开发者提供的扩展开发工具包。

#### 本SDK目前尚处于内测阶段，预计11-1正式发布。
{% endhint %}

## **JS SDK使用步骤** <a id="JSSDK&#x4F7F;&#x7528;&#x6B65;&#x9AA4;"></a>

**步骤一：引入JS文件**

在需要调用JS SDK接口的页面引入如下JS链接，"module-operation!executeOperation?operation=vds-sdk-js"（本链接会自动请求当前V-AppServer服务的sdk版本）

```markup
<script src="module-operation!executeOperation?operation=vds-sdk-js"></script>
```

**步骤二：通过config接口初始化sdk配置**

```javascript
vds.config({
  debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
  extensions: [] // 可选，需要预加载的扩展服务命名空间，平台业务构件的构件编码会默认作为扩展服务的命名空间。
});
```

**步骤三：通过ready接口处理sdk的调用**

```javascript
vds.ready(function(){
  // config信息初始化成功后会执行ready方法，所有接口调用都必须在config接口获得结果之后，config是一个客户端的异步操作，所以如果需要在页面加载时就调用相关接口，则须把相关接口放在ready函数中调用来确保正确执行。
});
```

**步骤四：通过error接口处理config初始化失败**

```javascript
vds.error(function(res){
  // config信息初始化失败会执行error函数，具体错误信息可以打开config的debug模式查看，也可以在返回的res参数中查看。
});
```

#### **接口调用说明** <a id="&#x63A5;&#x53E3;&#x8C03;&#x7528;&#x8BF4;&#x660E;"></a>

所有接口通过vds对象来调用，参数是一个对象，除了每个接口本身需要传的参数之外，还有以下通用参数：

1. success：接口调用成功时执行的回调函数。
2. fail：接口调用失败时执行的回调函数。
3. complete：接口调用完成时执行的回调函数，无论成功或失败都会执行。

以上几个函数都带有一个参数，类型为对象，其中每个接口本身返回的数据放到data属性之外，还有一个通用属性errMsg，其值格式如下：

1. 调用成功时："xxx:ok" ，其中xxx为调用的接口名。
2. 调用失败时：其值为具体错误信息。

## **接口列表** <a id="&#x57FA;&#x7840;&#x63A5;&#x53E3;"></a>

### 调用V平台业务构件API方法

通过本接口可以直接调用V平台业务构件配置的构件级客户端/服务端API方法。

**注意**：相关业务构件需保证已经安装并正常运行在指定的V-AppServer服务中。

```javascript
//初始化依赖配置，预加载指定业务构件的API
vds.config({
	debug:false,// 关闭调试模式
	extensions:["loginComponent"] // 选填，loginComponent为构件编号 
});
vds.ready(function(){
  //在vds的biz内置命名空间下使用本接口
	vds.biz.callFunction ({
		name:"loginComponent.login"//构件编号.api编号
		data:{
			account:"user1",//api输入account
			pwd:"pwd1",//api输入pwd
		},
		success:function(res){
      var data = res.data;
			//do something
		},
		fail : function(err){
      var errMsg = err.errMsg;
			// do something
		}
	});
});
```

上述例子中需要调用业务构件**loginComponent**的API方法**login**，API入参传递方法如上所示，如果api入参为实体类型，则传递数组，数组中每个元素都是Object，Object中key为字段编号，value为字段值。

**success回调**只有一个参数，类型为Object；Object中有两个属性：data和errMsg；data值为api输出，类型为Object，其中key为api输出变量编号，value为输出变量值。如api无输出 ，则为null。 

**fail回调**同样只有一个参数，类型为Object；Object中有一个属性：errMsg，存放错误信息。

## **附录1-所有JS SDK接口列表** <a id="&#x9644;&#x5F55;2-&#x6240;&#x6709;JS&#x63A5;&#x53E3;&#x5217;&#x8868;"></a>

#### 基础接口

vds.config  
vds.ready  
vds.error

#### 业务接口

vds.biz.callFunction

## **附录2-常见错误及解决方法** <a id="&#x9644;&#x5F55;5-&#x5E38;&#x89C1;&#x9519;&#x8BEF;&#x53CA;&#x89E3;&#x51B3;&#x65B9;&#x6CD5;"></a>

## **附录3-DEMO页面和示例代码** <a id="&#x9644;&#x5F55;6-DEMO&#x9875;&#x9762;&#x548C;&#x793A;&#x4F8B;&#x4EE3;&#x7801;"></a>

## **附录4-问题反馈** <a id="&#x9644;&#x5F55;7-&#x95EE;&#x9898;&#x53CD;&#x9988;"></a>

