# V平台服务端规则/函数插件开发

## 简介

2次开发插件主要目的是扩展V平台的功能不足，更好的实现业务定制化。

规则和函数的开发过程基本一样的，有2点不同：实现接口不同，获取参数不同。

## 特点

开发过程完全按照java标准API开发，不需要关心V平台的API，只要实现入口接口即可。

可以自由使用IntelliJ IDEA 或者 Eclipse ，打包使用标准maven。

```java
/**函数接口*/
public interface IFunction {
	/** 
	 * 函数入口
	 * @param context 上下文对象
	 * @return 返回单值
	 */
	public Object evaluate(IFuncContext context) ;
}
```

```java
/** 二次开发规则接口*/
public interface IRule {
	/**
	 * 规则入口
	 * @param context 上下文对象
	 * @return 返回多值请返回Map,单值请返回Object
	 */
	public Object evaluate(IRuleContext context) ;
}

```

## maven配置

_maven不是必须的，但是没有它工作效率会比较低。_

#### 1.maven 的 settings.xml配置

如使用命令行，就要_**配置maven**_的conf目录的settings

或者使用是_**Eclipse 的maven的配置**_，那么就配置指定的settings文件。

配置目的是从第3方的maven库下载V平台的2次开发接口，就是前面提到的 函数接口 IFunction ,规则接口 IRule

打开settings.xml，找到profiles节点，复制下面的配置到profiles内。（没有 profiles 节点就创建节点）

```markup
<!-- 嵌入到maven的settings.xml 这部分是必须的 -->
<profile>
    <id>codingProxy</id>
    <activation>
        <activeByDefault>true</activeByDefault>
    </activation>
    <repositories>
        <repository>
            <id>yindangu-v-devsuite-sdk-maven</id>
            <name>maven</name>
            <url>https://yindangu-maven.pkg.coding.net/repository/v-devsuite-sdk/maven/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>
</profile>
<!-- 嵌入到maven的settings.xml 这部分是必须的 -->
```

## 开始

### 创建标准maven项目

![](../.gitbook/assets/tu-pian-%20%282%29.png)

![](../.gitbook/assets/tu-pian-%20%281%29.png)

一直往下就成功创建标准的mavn项目了。如果有不清楚可以百度一下。

### 配置 pom.xml

#### V3入口依赖

#### 配置 paas-extension构件\(必须\)

```markup
<dependency>
    <groupId>com.toone.v3.platform</groupId>
    <artifactId>paas-extension</artifactId>
    <version>3.3.0</version>
</dependency>
```

#### 配置maven-jar-plugin插件\(必须）

如果没有配置jar-plugin，打包时可能会报"ipojo类增强出错"

```markup
<plugin><!-- 必须的插件 3.0.2 以上-->
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-jar-plugin</artifactId>
    <version>3.0.2</version>
</plugin>
```

#### 导出依赖包（非必须）

把依赖的包导出来，方便发布构件时选择。在 build --&gt; plugins 节点下加入

```markup
<plugin><!-- 把依赖的包导出来，方便发布构件时选择 -->  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-dependency-plugin</artifactId>  
    <executions>  
        <execution>
            <id>copy</id>  
            <phase>package</phase>  
            <goals>  
                <goal>copy-dependencies</goal>  
            </goals>  
            <configuration>  
                <outputDirectory>${project.build.directory}/lib</outputDirectory>  
            </configuration>  
        </execution>  
    </executions>  
</plugin>
```

#### 去除多余节点（非必须）

标准maven包含了一些多余的节点，可以去掉，例如：pluginManagement 节点

```markup
<pluginManagement>
    <plugins>
      ...
    </plugins>
  </pluginManagement>
```

#### 下面是实例的完整pom.xml,开发时可以参考下

```markup
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.yindangu</groupId>
	<artifactId>demo-rule</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<name>demo</name>
	<!-- FIXME change it to the project's website -->
	<url>http://www.example.com</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<maven.compiler.source>1.6</maven.compiler.source>
		<maven.compiler.target>1.6</maven.compiler.target>
	</properties>

	<dependencies>
		<dependency>
			<groupId>com.toone.v3.platform</groupId>
			<artifactId>paas-extension</artifactId>
			<version>3.3.0</version>
		</dependency>
		<!-- 第三方的包 -->
		<!--dependency>
			<groupId>com.yindangu.demo</groupId>
			<artifactId>util</artifactId>
			<version>0.0.1-SNAPSHOT</version>
			<scope>system</scope>
			<systemPath>${project.basedir}/lib/util-0.0.1-SNAPSHOT.jar</systemPath>
		</dependency-->
		<!-- ////////////////日志开始/////////////////// -->
		<dependency>
			<groupId>org.apache.logging.log4j</groupId>
			<artifactId>log4j-api</artifactId>
			<version>2.0</version>
		</dependency>
		<dependency>
			<groupId>org.apache.logging.log4j</groupId>
			<artifactId>log4j-core</artifactId>
			<version>2.0</version>
		</dependency>
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-simple</artifactId>
			<version>1.7.0</version>
		</dependency>
		<!-- ///////////////日志结束//////////////////// -->
	</dependencies>

	<build>
		<plugins>
			<plugin><!-- 必须的插件 3.0.2 以上-->
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-jar-plugin</artifactId>
				<version>3.0.2</version>
			</plugin>
			<plugin><!-- 把依赖的包导出来，方便发布构件时选择 -->
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-dependency-plugin</artifactId>
				<executions>
					<execution>
						<id>copy</id>
						<phase>package</phase>
						<goals>
							<goal>copy-dependencies</goal>
						</goals>
						<configuration>
							<outputDirectory>${project.build.directory}/lib</outputDirectory>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
</project>
```

### 函数程序架构

配置好maven、pom.xml后就可以开发了。如果在eclipse里maven一直update不下来paas-extension的jar文件。可以试试使用maven的命令行，定位到工程的pom.xml的目录执行：（manve的配置需要自己配置）

```markup
mvn package 
```

#### 函数插件需要实现接口：

```markup
com.toone.itop.paas.extension.api.IFunction
```

接下来我们做一个把数字转换成汉字的函数，例如 92287 转换汉字就是 九万二千二百八十七，实例代码：

NumberUpperFunc 参数说明：

```java
入口: com.yindangu.demo.NumberUpperFunc
参数1--需转换数字(数值类型)；
```

```java
package com.yindangu.demo;

import java.util.ArrayList;
import java.util.List;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.toone.itop.paas.extension.api.IFunction;
/**
 * 数字转换成汉字
代码示例:NumberUpperFunc(3,"name",实体)，返回值: 九万二千二百八十七。
入口: com.yindangu.demo.NumberUpperFunc
参数1--需转换数字(数值类型)； 
返回汉字大写。 
 * @author jiqj
 *
 */
public class NumberUpperFunc  implements IFunction {
	private static final Logger log = LoggerFactory.getLogger(NumberUpperFunc.class);
	public NumberUpperFunc(){
		log.info("函数:数字转换成汉字");
	}

	public Object evaluate(IFuncContext context) {
		/////////////////参数检查///////////////////
		Number nb = (Number)context.getParams(0);//参数1--需转换数字(数值类型)
		//String column = (String)context.getParams(1);//参数2--可以接收多参数的例子
		//Date today = (Date)context.getParams(2);//参数3--可以接收多参数的例子
		if(nb == null){
			throw new RuntimeException("参数1--行数不能为空！");
		}
		////////////////业务实现 api 完全与V平台无关////////////////////
		BusinessFunc fb = new BusinessFunc();
		String rs = fb.execute(nb.intValue());
		return rs;
	}
	

	/**
	 * 单机调试代码
	 * @param args
	 */
	public static void main(String[] args){
		final List<Object> pars = new ArrayList<Object>();
		pars.add(92287);
		IFuncContext fc = new IFuncContext() { 
			public int getParamSize() { 
				return pars.size();
			}
			public Object getParams(int idx) { 
				return (idx < pars.size() ? pars.get(idx) : null);
			}
		};
		
		IFunction  func = new NumberUpperFunc(); 
		Object fr = func.evaluate(fc);
		log.info("函数返回:"  + fr);
	}
}
```

NumberUpperFunc 相当于一个接收参数的壳，BusinessFunc 才是真正的业务代码的实现

```java
BusinessFunc fb = new BusinessFunc();
String rs = fb.execute(nb.intValue());
return rs;
```

BusinessFunc 的具体代码，开发时请按实际业务开发：

```java
package com.yindangu.demo;

import com.yindangu.demo.util.Number2UppercaseUtil;
/**具体的业务类(完全与V平台无关了)*/
class BusinessFunc{
	/**业务实现*/
	public String execute(int rowIdx ){
		String ns =Number2UppercaseUtil.toUpperCase(rowIdx);
		return  ns; 
	}
}
```

Number2UppercaseUtil是数字转汉字大写的工具类，是第三方jar。如果插件需要第三方jar包时，发布构件需要提交给服务器打包的。

```java
com.yindangu.demo.util.Number2UppercaseUtil
```

### 规则程序架构

#### 规则插件需要实现接口：

规则返回值必须是Map\(定义为Object是为了以后扩展\),所有返回值都要put到map里面

```java
com.toone.itop.paas.extension.api.IRule
```

规则功能： 把实体某列转换为汉字大写。

```java
规则功能：把实体某列转换为汉字大写
输入参数：列名-需转换的列名，实体
输出参数：转换后的实体
入口: com.yindangu.demo.NumberUpperRule
代码示例:NumberUpperFunc("age",实体)
```

```java
package com.yindangu.demo;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.toone.itop.paas.extension.api.IRule;
/**
规则功能：
把实体某列转换为汉字大写
输入参数2个：列名-字符串需转换的列名，实体
输出参数1个：转换后的实体
入口: com.yindangu.demo.NumberUpperRule
代码示例:NumberUpperFunc("age",实体)

参数:[{code:column,type:string},
	{code:myentity,type:entity,"entityField": [
       {
            "code": [参数列],
            "type": "int" 
        },...
    ]}

返回 {
  myentity:{
     type:entity,"entityField": [
        {
            "code": [参数列],
            "type": "char" 
        }, ...
    ]}
  }
 * @author jiqj 
 */
public class NumberUpperRule implements IRule {
 
	private static final Logger log = LoggerFactory.getLogger(NumberUpperRule.class);
	public NumberUpperRule(){
		log.info("规则:指定数据实体某行某列的值转换为汉字大写");
	}

	/**
	 * 规则入口
	 * @return 返回值必须是Map(定义为Object是为了以后扩展),所有返回值都要put到map里面
	 */
	@SuppressWarnings({ "unchecked", "rawtypes" })
	public Object evaluate(IRuleContext context) {
		/////////////////参数检查///////////////////
		String column = (String)context.getParams("column");//需转换的列名
		//Date today = (Date)context.getParams("today");//日期参数--可以接收多参数的例子
		List<Map> entity = (List<Map>)context.getParams("myentity");//实体
		if(column == null){
			throw new RuntimeException("参数column--列名不能为空！");
		}
		if(entity == null){
			throw new RuntimeException("转换参数myentity--实体不能为空！");
		}		
		////////////////业务实现 api 完全与V平台无关////////////////////
		BusinessRule br = new BusinessRule();
		List<Map> entity2 = br.convertEntity(column, entity);
		
		//输出的key: myentity 具体可以构件定义
		Map<String,Object> map = new HashMap<String, Object>();
		map.put("myentity", entity2);
		return map;
	}
	
	/**自测代码*/
	@SuppressWarnings({ "unchecked", "rawtypes" })
	public static void main(String[] args){ 
		List<Map> entity = mockEntity();
		final HashMap<String,Object> pars = new HashMap<String,Object>();
		pars.put("column", "age");//需转换的列名
		pars.put("myentity", entity);//实体
		
		IRuleContext context = new IRuleContext() {
			public int getParamSize() { 
				return pars.size();
			}
			public Object getParams(String key) { 
				return pars.get(key);
			}
		}; 
		
		
		IRule  rule = new NumberUpperRule();
		Map<String,Object>  result =(Map<String,Object>) rule.evaluate(context);
		List<Map> entity2 =(List<Map>) result.get("myentity");
		for(Map m : entity2){
			log.info(m.get("myname") + ") 年龄: "  + m.get("age"));
		}
	}
	/**自测代码*/
	@SuppressWarnings({ "rawtypes", "unchecked" })
	private static List<Map> mockEntity(){
		List<Map> entity =new ArrayList();
		Map<String,Object> m =  new HashMap();
		m.put("myname","李四");
		m.put("age",40);
		entity.add(m);
		
		Map<String,Object> s =  new HashMap();
		s.put("myname","张三");
		s.put("age",39);
		entity.add(s);
		return entity;
	}
}
```

NumberUpperRule 接收参数转换后执行BusinessRule 业务代码的实现

BusinessRule的代码实现：

```java
package com.yindangu.demo;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import com.yindangu.demo.util.Number2UppercaseUtil;

/**具体的业务类(完全与V平台无关了)*/
class BusinessRule{   
	/**
	 * 业务实现 : 把指定列转换为汉字大写
	 * @param column
	 * @param sourceEntity
	 * @return
	 */
	@SuppressWarnings({ "rawtypes", "unchecked" })
	public List<Map> convertEntity(String column,List<Map> sourceEntity){
		List<Map> rds = new ArrayList<Map>();
		if(sourceEntity == null || sourceEntity.isEmpty()){
			Map<String,Object> map = new HashMap<String, Object>();
			map.put(column, "没有记录");
			rds.add(map);
		}
		else{
			for(Map src: sourceEntity){
				Map<String,Object> map = new HashMap<String, Object>(src);
				Integer age = (Integer)map.get(column); 
				String myage = "无";
				if(age!=null){
					myage = Number2UppercaseUtil.toUpperCase(age.longValue());
				}
				map.put(column, myage); 
				rds.add(map);
			}
		}
		return rds;
	} 
}
```

## 输出制品

输出制品可以直接用maven命令，生成jar文件，及第3方jar。

```java
mvn package
```

_**注意：**_如果使用了第3的jar包，打包插件时也要上传

## 附录一：样例工程源码

{% file src="../.gitbook/assets/demo-func \(1\).zip" caption="函数maven项目示例" %}

{% file src="../.gitbook/assets/demo-rule \(1\).zip" caption="规则maven项目示例" %}

