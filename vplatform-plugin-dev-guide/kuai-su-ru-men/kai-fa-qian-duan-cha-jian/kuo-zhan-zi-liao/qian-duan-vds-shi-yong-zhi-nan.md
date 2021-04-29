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
	"id":“”“”,
	"name":"张三",
	"sex":"male",
	"age":35
},{
	"id":2,
	"name":"李四",
	"sex":"female",
	"age":26
}]);
vds.ds.register("persion",datasource);
```

