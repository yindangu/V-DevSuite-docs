---
description: 现平台提供了很多规则、函数，项目中有些特殊场景需要对现有的规则、函数替换或者复制改造。【注意】"扩展"比"替换"更加可控。
---

# 替换和扩展

## 1.名词说明

**【替换】**就是对现有的规则、函数的实现逻辑改掉，其他的东西不变，只改造实现代理。

替换的应用场景：项目已经大规模使用了规则、函数，重新配置所有的规则会耗费巨大的人力、物力的情况下使用。【**注意**】替换平台的规则、函数并不是二次开发插件的设计目的，二次开发插件的设计的目的是**扩展**平台的规则、函数，**替换**只是妥协的手段。根据我们估计95%的场景都可以使用扩展模式完成。

**【扩展】**复制平台的规则、函数，重新定义规则名称、修改实现代码。

相当于创建新的规则，只是参考了平台现有的规则实现代码。

## 2.替换规范

替换操作过程：

1、复制平台的规则、函数构件源码。（元信息定义只能修改desc属性）

2、修改实现逻辑。（修改实现代码）

3、提交构件。（提交云空间）

约定：平台建议只修改“Desc”属性，元信息定义比较复杂为了控制参数的一致性，修改了其他属性可能导致编译不通过。

平台关键元信息不能修改：机构id\(groupId\)、构件编码\(component.code\)、插件编码\(plugin.code\)不能修改。

```java
	@Override
	public IComponentProfileVo getComponentProfile() {
		return RegVds.getPlugin().getComponentProfile()
				.setGroupId("com.yindangu.plugin")//机构id(groupId)不能修改
				.setCode("mydemo")//构件编码不能修改
				.build();
	}
	private IPluginProfileVo getFileStorageService() {
		IFileStorageServiceBuilder fss = RegVds.getPlugin().getFileStorageServicePlugin();
		IFileStorageServiceProfileVo vo = fss.setName("我的文件存储")
				.setCode(MyFileStorageService.FileStorage_Code) //插件编码不能修改
				.setDesc("我的文件存储服务") //只能修改描述的信息
				.setConfigPath("./config.xml")
				.setAuthor("徐刚")
				.setEntry(MyFileStorageService.class)
				.build();
		return vo;
	}
```

```javascript
{
  "groupId": "com.yindangu.plugin",//机构id(groupId)不能修改
  "code": "mydemo",//构件编码不能修改
  "plugins": [
    {
      "type": "function",
      "scope": "client",
      "code": "NumToChineseFunc",//插件编码不能修改
      "name": "数字转大写汉字(前端)",
      "desc": "数字转大写汉字(前端)",//只能修改描述的信息
      "entry": "com.yindangu.func.demo.evaluate",
      "defineUrl": "./client-demo/function/dist/NumToChineseFunc.js",
      "debugUrl": "./client-demo/function/debug/function.js",
      "inputs": [
        {
          "index": "",
          "type": "number",
          "desc": "转换的数字",
          "required": false,
          "default": null
        }
      ],
      "output": {
        "type": "char",
        "desc": "数字转大写汉字",
        "unknowType": false
      }
    }
 }
```

入参、返回值不能修改：参数个数、类型都不允许修改

```java
/** 函数元信息(数字转汉字) */
	private IPluginProfileVo getNumberUpperFunc() {
		IFunctionBuilder bf = RegVds.getPlugin().getFunctiontPlugin();
		IPluginProfileVo p1 = bf.setCode(NumberUpperFunc.D_Code)
				.setName("数字转汉字-name")
				.setDesc("数字转汉字")
				.setAuthor("徐刚")
				.addInputParam(bf.newInput().setType(VariableType.Integer).setDesc("数字").build())  //参数不能修改
				.setEntry(NumberUpperFunc.class)
				.setOutput(bf.newOutput().setType(VariableType.Char).setDesc("汉字大写").build()) //参数不能修改
				.setExample("使用示例说明，\r\n换号,这是示例说明")//只能修改描述的信息
				.build();
		return p1;
	}
```

作者信息：作者信息在发布云空间是自动获取登录人。

## 3.扩展

相当于创建新的规则，操作过程就跟着demo的过程。



## **4.强烈建议**

**能够扩展就尽量扩展，少用替换模式。**

**替换**平台的规则、函数的主要引发下面问题：

1、改变了平台的行为，出错了难发现问题。

2、无法跟随平台升级。

3、版本控制变得很复杂（平台版本优先级控制、项目版本优先级控制、项目与项目之间的优先级）

4、前期看似节省了时间，这只是表象，替换模式在后期会产生很多维护成本。

**扩展**模式就没有以上问题，唯一的缺点就是前期投入时间多一些。

{% embed url="https://5.版本控制策略" %}

版本

\*\*\*\*

