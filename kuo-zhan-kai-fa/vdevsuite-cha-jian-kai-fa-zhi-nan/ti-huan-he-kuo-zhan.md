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

#### 约定

a、平台建议只修改“Desc”属性，元信息定义比较复杂为了控制参数的一致性，修改了其他属性可能导致编译不通过。

b、每个构件包含的插件数量要相同。

目前平台的构件和插件都是一对一的（一个构件只包含一个插件），但以后可能会一个构件包含多个插件。如果a构件包含了b、c、d三个插件，如果a1替换了a构件，但是a1构件只包含了b、c两个插件，这样系统就会丢失了d插件。

#### **其他信息说明**

**关键元信息**不能修改：机构id\(groupId\)、构件编码\(component.code\)、插件编码\(plugin.code\)不能修改。

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

**入参、返回值**不能修改：参数个数、类型都不允许修改

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

**作者信息：**作者信息在发布云空间是自动获取登录人。

## 3.扩展

相当于创建新的规则、函数，操作过程就跟着demo的过程。

### 函数

直接复制平台的代码和元信息描述后，需要修改机构id\(groupId\)、构件编码\(component.code\)、插件编码\(plugin.code\)为自定义的内容。

扩展的函数与平台的函数已经没有必然的关系，参数信息、返回值等都可以按需改造。

### 函数示例

函数比较简单，取得平台原码后，需要修改的地方：

a\)修改pom.xml文件: groupId，artifactId，version等都要修改。

b\)修改插件注册器: groupId,component.code,plugin.code。

d\)增加扩展参数：扩展方式与demo的一样。

具体请参考demo

### 规则

扩展平台规则可以使用现有的配置界面，还可以增加额外参数。平台现有的规则没有入参、返回值的，扩展的额外参数只能通过入参、返回值实现。

扩展配置取得原码后，需要修改的地方：

a\)修改pom.xml文件: groupId，artifactId，version等都要修改。

b\)修改插件注册器groupId,component.code,plugin.code。

c\)配置扩展平台规则属性：manifest.json（references属性）**【重要】**

references：说明扩展平台的具体规则

前端配置json\(前后其实都一样，只是表现方式不同而已\)

```java
reference:{
  groupId:"组织id，平台规则基本就是：com.toone.v3.platform"
  scope:"client",//可选，默认值为client，枚举值：client、server
  componentCode:"Webrule_AbortRule",//必填，构件编号
  pluginCode:"AbortRule"//必填，插件编号
},
```

完整的结构：

```java
[{
    type:"rule",//插件类型
    code:"",//规则编号
    name:"",//规则名称
    deprecated:false,//是否已弃用
    desc:"",//规则描述
    author:"",//开发者
    entry:"",//规则主入口
    scope:"",//规则应用范围
    catalog:"",//规则所属目录
    transactionType:"",//事务类型
    defineUrl:"",//规则定义脚本文件url
    debugUrl:""//规则测试脚本文件url
    reference:{//可选，基于已有规则扩展，目前只支持平台规则
        groupId:"com.toone.v3.platform",//必填，组织id
        scope:"client",//可选，默认值为client，枚举值：client、server
        componentCode:"Webrule_AbortRule",//必填，构件编号
        pluginCode:"AbortRule"//必填，插件编号
    },
    inputs:[{//使用数组，方便属性排序,可选
		code:"",//属性编号，
		name:""//属性名称，
        type:"",//属性类型
		desc:""//属性描述，
		default:null//默认值,
		editor:{//编辑器信息，可选
			type:"",//编辑器类型
		}
	}],
    outputs:[{
        code:""//规则输出编号,
        type:""//规则输出类型,
        name:"",//规则输出名称,
        desc:"",//规则输出描述,
        fields:[{//输出类型为entity时,此属性生效
            code:""//列编号,
            type:""//列类型,
            name:"",//列名称,
            desc:""//列描述
        }...]
    }]
}]
```



d\)增加扩展参数：扩展方式与demo的一样。

### 规则示例

例如清除实体记录\(ClearEntityData\)的规则需要增加写操作日志标志参数，如果参数为1，就要记录数据被谁清除的记录。

1\)修改pom.xml\(只截取了需要修改的部分\)

```markup
<groupId>com.mydemo</groupId>
<artifactId>demo_ClearEntityData</artifactId>
<version>3.4.0</version>
<description>后台规则-清除实体数据，并且记录清除人</description>
```

2\)修改插件注册器ClearEntityRegister.java\(增加入参和返回值，已经修改groupid等参数\)，注意要设置扩展的规则信息

设置扩展的规则信息\(前后端其实都一样，只是表现方式不同而已\)：

```java
IRuleReferenceBuilder refBuilder = ruleBuilder.newReference()
	.setGroupId("com.toone.v3.platform")
	.setComponentCode("Serverrule_ClearEntityData")
	.setPluginCode("ClearEntityData");
```

```java
import java.util.Collections;
import java.util.List;

import com.yindangu.v3.plugin.vds.reg.api.IRegisterPlugin;
import com.yindangu.v3.plugin.vds.reg.api.builder.IRuleBuilder;
import com.yindangu.v3.plugin.vds.reg.api.builder.IRuleBuilder.IRuleReferenceBuilder;
import com.yindangu.v3.plugin.vds.reg.api.model.IComponentProfileVo;
import com.yindangu.v3.plugin.vds.reg.api.model.IPluginProfileVo;
import com.yindangu.v3.plugin.vds.reg.api.model.IRuleProfileVo;
import com.yindangu.v3.plugin.vds.reg.api.model.VariableType;
import com.yindangu.v3.plugin.vds.reg.common.RegVds;

/**
 * @Author xugang
 * @Date 2021/5/27 11:23
 */
public class ClearEntityRegister implements IRegisterPlugin {
	
    @Override
    public IComponentProfileVo getComponentProfile() {
        return RegVds.getPlugin()
                .getComponentProfile()
                .setGroupId("com.mydemo") //这3个元素按需要修改
                .setCode("demo")
                .setVersion("1.0.0")
                .build();
    }

    @Override
    public List<IPluginProfileVo> getPluginProfile() {
    	IPluginProfileVo pro = getRuleProfile();
        return Collections.singletonList(pro);
    }

 
    private IRuleProfileVo getRuleProfile() {
    	IRuleBuilder ruleBuilder = RegVds.getPlugin().getRulePlugin();
    	IRuleBuilder.IRuleInputBuilder rulePlog = ruleBuilder.newInput()
    			.setCode(ClearEntityData.D_PARAM_WRITELOG)
				.setName("需要写日志标志").setType(VariableType.Boolean);
    	IRuleBuilder.IRuleOutputBuilder ruleOut = ruleBuilder.newOutput()
    			.setCode(ClearEntityData.D_PARAM_ClearCount)
    			.setName("返回清除记录数")
    			.setType(VariableType.Integer);
    	
    	IRuleReferenceBuilder refBuilder = ruleBuilder.newReference()
    			.setGroupId("com.toone.v3.platform")
    			.setComponentCode("Serverrule_ClearEntityData")
    			.setPluginCode("ClearEntityData");
    	
    	ruleBuilder.setAuthor("jiqj")
                .setCode(ClearEntityData.D_RULE_CODE)//这3个元素按需要修改
                .setDesc(ClearEntityData.D_RULE_DESC)
                .setName(ClearEntityData.D_RULE_NAME)
                .setEntry(ClearEntityData.class)
                .addInput(rulePlog.build())//增加入参
                .addOutput(ruleOut.build()) //增加返回值
                .setReference(refBuilder.build()) //设置扩展的规则信息
                ;
    	
        return ruleBuilder.build();
    }
}

```

编译安装到开发系统会显示【原始配置】、【扩展配置】

![&#x6269;&#x5C55;&#x914D;&#x7F6E;](../../.gitbook/assets/image%20%2834%29.png)

逻辑实现代码获取参数与demo一样，通过上下文获取：

后端：

```java
//获取扩展参数
Boolean writeLog = (Boolean)context.getInput(D_PARAM_WRITELOG);
if(writeLog!=null && writeLog) {
	clearCount = + 10000; 
}
//输出返回值
return context.newOutputVo()
		.put("clearCount", Integer.valueOf(clearCount))
		.put(Boolean.TRUE);
```

前端:

```javascript
var output = ruleContext.newOutputVo();
var clearCount =100;//获取扩展参数
var writelog = ruleContext.getInput("writelog");
if(writelog){
	clearCount = 999;
}//输出返回值
output.set("clearCount",clearCount);
```

## **4.强烈建议**

**能够扩展就尽量扩展，少用替换模式。**

**替换**平台的规则、函数的主要引发下面问题：

1、改变了平台的行为，出错了难发现问题。

2、无法跟随平台升级。

3、版本控制变得很复杂（平台版本优先级控制、项目版本优先级控制、项目与项目之间的优先级）

4、前期看似节省了时间，这只是表象，替换模式在后期会产生很多维护成本。

**扩展**模式就没有以上问题，唯一的缺点就是前期投入时间多一些。

## 5.版本控制策略

版本控制策略适合所有的构件。先说明一下日常工作会涉及的版本：

a\)maven中的pom.xml的版本：这个版本号在二次开发插件的规范中并没有使用，因为考虑二次开发是开发式的，有些开发团队可能不是用maven管理，因此maven版本号是没有作用的。

b\)构件元信息版本：二次开发插件是使用这个版本为准，如果没有填写默认是"1.0.0"。前端是写在manifest.json文件，后端是在IRegisterPlugin.getComponentProfile\(\)方法配置。

c\)构件编译时间戳：本地编译jar时间，云编译时间。二次开发规范是以云编译时间为准。如果两个构件的版本号一样，就以最新云编译时间的构件为最高版本。

d\)清单引用项分支优先级: 当清单存在多个项目或分支的引用项，需要配置优先级排序策略。

这4个版本项的优先级由高到低：

优先使用引用项分支优先级：如果a清单和b清单同时存在abs构件，a清单优先高于b清单，不管b清单abs构件版本号、时间戳是否高于a清单，都不会使用b清单的abs构件。

构件元信息版本号第二优先级，构件编译时间戳第三优先级。









\*\*\*\*

