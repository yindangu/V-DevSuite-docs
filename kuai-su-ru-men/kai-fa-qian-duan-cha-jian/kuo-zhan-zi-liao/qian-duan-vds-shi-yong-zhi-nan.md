---
description: 平台提供一系列接口供二次开发人员调用，方便开发人员使用平台现有接口，提升开发效率。
---

# 前端vds使用指南

## 使用规范

在使用vds提供的接口前，需要先将vds接口引入，引入规范如下：

```text
//引入vds命名空间下所有接口
vds.import("vds.ds.*");
//引入多个vds命名空间
vds.import("vds.ds.*","vds.mock.*");
```

## 验证准备

二次开发使用vds提供的接口后，验证时需要先初始化vds，如下：

```text
<script src="http://localhost:8080/module-operation!executeOperation?operation=vds-sdk-js"></script>
<script>
	vds.config({
		debug: true,
		import: ["vds.mock.*", "vds.ds.*","vds.test.*"]//额外引入vds命名空间
	}).ready(function () {
		//这里编辑验证逻辑
	});
</script>
```

其中http://localhost:8080为平台执行系统服务地址。

## ds（数据源）

ds命名空间为datasource的缩写,提供一些列数据源的操作,如获取数据源实例,加载数据,保存数据等。

### **lookup（获取数据源实例）**

查找数据源实例，如果数据源实例存在则返回数据源实例，否则返回null。

#### **入参**

接口入参定义如下：

| 参数 | 值类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| datasourceName | String | 是 |  | 数据源名称 |

#### **返回值**

[数据源实例](https://docs.qq.com/doc/DRGtsZWRZQ25PaXRr)

#### **使用样例**

```text
vds.ds.lookup("ds1");
```

### **register（注册数据源实例）**

注册现有的数据源实例；注册时，当前上下文中如果不存在该名称的数据源，则返回true，否则返回false。

#### **入参**

接口入参定义如下：

| 参数 | 值类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| datasourceName | String | 是 |  | 数据源名称 |
| datasource | [Datasource](https://docs.qq.com/doc/DRGtsZWRZQ25PaXRr) | 是 |  | 数据源实例 |

#### **返回值**

Boolean

#### **使用样例**

```text
vds.ds.register("ds1",datasource);//true:注册成功,false:注册失败
```

### **unRegister（注销数据源实例）**

销毁现有的数据源实例；如果当前上下文中不存在该数据源实例，则返回false，否则返回true

#### **入参**

接口入参定义如下：

| 参数 | 值类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| datasourceName | String | 是 |  | 数据源名称 |

#### **返回值**

Boolean

#### **使用样例**

```text
vds.ds.unRegister("ds1");//true:销毁成功,false:销毁失败
```

### **exists（数据源实例是否存在）**

判断当前上下文中是否存在指定的数据源，存在返回true，否则返回false。

#### **入参**

接口入参定义如下：

| 参数 | 值类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| datasourceName | String | 是 |  | 数据源名称 |

#### **返回值**

Boolean

#### **使用样例**

```text
vds.ds.exists("ds1");//true:存在,false:不存在
```

### **mock（mock数据源）**

提供mock数据源接口，方便开发人员进行测试验证；接口内部逻辑会将根据第一条数据源数据窗体数据源元信息，根据数据中属性值类型确定字段类型；其中数据源数据中必须包含id字段，且保证id字段值唯一（即id字段为主键）。

#### **入参**

接口入参定义如下：

| 参数 | 值类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| datasource | List | 是 |  | 数据源数据 |

#### **返回值**

[数据源实例](https://docs.qq.com/doc/DRGtsZWRZQ25PaXRr)

#### **使用样例**

```text
var datasource = vds.ds.mock([{
	"id":"1",
	"name":"张三",
	"sex":"male",
	"age":35
},{
	"id":"1",
	"name":"李四",
	"sex":"female",
	"age":26
}]);
vds.ds.register("persion",datasource);
```

## object（object工具方法）

提供一系列的Object工具方法供开发人员使用，提升开发效率。

### keys

获取对象中所有属性名称

#### 返回值

Array

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.keys(obj);
//rs => ["one", "two", "three"]
```

### values

获取所有属性值

#### 返回值

Array

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.keys(obj);
//rs => [1, 2, 3]
```

### pairs

将对象转换成二维数组

#### 返回值

Array

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.pairs(obj);
//rs => [["one", 1], ["two", 2], ["three", 3]]
```

### invert

将对象中属性和属性值对调

#### 返回值

Object

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.invert(obj);
//rs => {1: "one", 2: "two", 3: "three"}
```

### functions

获取对象中所有方法名称

#### 返回值

Array

#### 使用样例

```text
var obj = {one: function(){return 1;}, two: 2, three: 3};
var rs = vds.object.functions(obj);
//rs => ["one"]
```

### extend

对象属性合并，如果目标对象存在该属性值，则被覆盖。支持多个对象。

#### 返回值

Object

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var obj1 = {four: 4, five: 5};
var rs = vds.object.extend(obj,obj1);
//rs => {one: 1, two: 2, three: 3, four: 4, five: 5}
//obj === rs => true
```

### pick

从对象中挑选属性并返回新对象

#### 返回值

Object

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.pick(obj,"one","two");
//rs => {one: 1, two: 2}
```

### omit

从对象中忽略指定属性并返回新对象

#### 返回值

Object

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.omit(obj,"one","two");
//rs => {three: 3}
var rs = vds.object.pick(obj,function(val,key,obj){
    return key.charAt(0) == "o";
});
//rs => {two: 2, three: 3}
```

### defaults

对象属性合并，如果目标对象存在该属性值，则被忽略。支持多个对象。

#### 返回值

Object

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var obj1 = {four: 4, five: 5};
var obj2 = {one: 4,six: 6};
var rs = vds.object.defaults(obj,obj1,obj2);
//rs => {one: 1, two: 2, three: 3, four: 4, five: 5,six: 6}
//obj === rs => true
```

### clone

创建一个浅拷贝的克隆对象。任何嵌套的对象或数组都通过引用拷贝，不会复制。

#### 返回值

Object

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.clone(obj);
//rs => {one: 1, two: 2, three: 3}
//obj === rs => false
```

### has

对象是否包含给定的属性。

#### 返回值

Boolean

#### 使用样例

```text
var obj = {one: 1, two: 2, three: 3};
var rs = vds.object.has(obj,"one")
//rs => true
```

### isEqual

对两个对象进行深度比较，确定是否相等。

#### 返回值

Boolean

#### 使用样例

```text
var obj = {name: '张三', luckyNumbers: [13, 16, 59]}; 
var obj1  = {name: '张三', luckyNumbers: [13, 16, 59]};
var rs = vds.object.isEqual(obj,obj1);
//rs =》 true
```

### isEmpty

判断对象是否为空。

### 返回值

Boolean

#### 使用样例

```text
var obj = {};
var rs = vds.object.isEmpty(obj)
//rs => true
```

### isElement

判断指定的对象是否为DOM元素。

#### 返回值

Boolean

#### 使用样例

```text
var obj = {};
var rs = vds.object.isElement(document.body)
//rs => true
```

### isArray

判断给定的对象是否为数组。

#### 返回值

Boolean

#### 使用样例

```text
var arr = [1,2,3];
var rs = vds.object.isArray(arr);
//rs => true
```

### isObject

判断是否为对象

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isObject({});//true
vds.object.isObject(1);//false
```

### isArguments

判断是否为参数对象。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isArguments({});//false
(function(){return vds.object.isArguments(arguments);})();//true
```

### isFunction

判断是否为函数。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isFunction(window.alert);//true
```

### isString

判断是否为字符串。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isString("abc");//true
vds.object.isString(123);//false
```

### isNumber

判断是否为数值。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isNumber("abc");//false
vds.object.isNumber(123);//true
```

### isBoolean

判断是否为布尔值。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isBoolean(true);//true
vds.object.isBoolean("abc");//false
```

### isDate

判断是否为Date.

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isDate("abc");//false
vds.object.isDate(new Date());//true
```

### isRegExp

判断是否为正则表达式。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isRegExp(/abc/);//true
vds.object.isRegExp("abc");//false
```

### isNull

判断给定的值是否为null。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isNull("");//false
vds.object.isNull(null);//true
```

### isUndefined

判断给定的值是否为undefined。

#### 返回值

Boolean

#### 使用样例

```text
vds.object.isUndefined(undefined);//true
vds.object.isUndefined(111);//false
```

## collection（collection工具方法）

### each

遍历集合中所有元素，按顺序用元素作为参数执行回调函数。

#### 返回值

无

#### 使用样例

```text
vds.collection.each([1,2,3],function(item,index){
    console.log("item:"+item+",index:"+index);    
});
//item:1,index:0
//item:2,index:1
//item:3,index:2
vds.collection.each({one: 1,two: 2,three: 3},function(val,key){
    console.log("key:"+key+",value:"+val);
});
//key:one,value:1
//key:two,value:2
//key:threee,value:3
```

### map

遍历集合中所有元素，执行回调函数，并生成与之相对应的数组。

#### 返回值

Array

#### 使用样例

```text
var rs = vds.collection.map([1,2,3],function(item,index){
    return item * 2;
});
//rs => [2,4,6]
var rs = vds.collection.map({one: 1, two: 2, three: 3},function(value,key){
    return value * 2;
});
// rs => [2,4,6]
```

### find

在集合中逐项查找，执行回调函数，如果回调返回值为true，则立即返回，中断遍历；如果遍历完成回调函数都没有返回true，则返回值为undefined。

#### 返回值

Any

#### 使用样例

```text
var rs = vds.collection.find([1,2,3],function(item,index){
    return item%2 == 0;
});
//rs => 2
var rs = vds.collection.find([1,2,3],function(item,index){
    return item == 4;
});
//rs => undefined
```

### where

根据指定的条件过滤数组。

#### 返回值

Array

#### 使用样例

```text
var players = [{name:"张三",sex:"男",age:25},{name:"李四",sex:"女",age:18}];
var rs = vds.collection.where(players,{sex:"男"});
/*
rs => [{
    name:"张三",
    sex:"男",
    age:25
}]
*/
```

### contains

判断集合中是否有指定的元素。

#### 返回值

Boolean

#### 使用样例

```text
var rs = vds.collection.contains([1,2,3],3);
//rs => true
```

### max

返回集合中最大值。

#### 返回值

Any

#### 使用样例

```text
var persons = [{name: '张三', age: 40}, {name: '李四', age: 50}, {name: '王五', age: 60}];
var rs = vds.collection.max(persons, function(person){ 
    return person.age; 
});
//rs => {name: '王五', age: 60};
```

### min

返回集合中最小值。

#### 返回值

Any

#### 使用样例

```text
var persons = [{name: '张三', age: 40}, {name: '李四', age: 50}, {name: '王五', age: 60}];
var rs = vds.collection.min(persons, function(person){ 
    return person.age; 
});
//rs => {name: '张三', age: 40};
```

### sortBy

根据指定函数排序。

#### 返回值

Array

#### 使用样例

```text
var rs = vds.collection.sortBy([1, 2, 3, 4, 5, 6], function(num){
    return Math.sin(num); 
}); 
//rs => [5, 4, 6, 3, 1, 2]  
var persons = [{name: '王五', age: 60},{name: '张三', age: 40}, {name: '李四', age: 50}, ];
var rs = vds.collection.sortBy(persons, 'age'); 
//rs => [{name: '张三', age: 40}, {name: '李四', age: 50}, {name: '王五', age: 60}]
```

