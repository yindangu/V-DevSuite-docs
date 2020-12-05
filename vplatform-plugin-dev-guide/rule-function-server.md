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

在maven的conf目录，或者是Eclipse 的maven的配置

配置目的是从第3方的maven库下载V平台的2次开发接口，就是前面提到的 函数接口 IFunction ,规则接口 IRule

打开maven/settings.xml，找到profiles节点，复制下面的配置到profiles内。

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

配置 paas-extension构件

```markup
<dependency>
    <groupId>com.toone.v3.platform</groupId>
    <artifactId>paas-extension</artifactId>
    <version>3.3.0</version>
</dependency>
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

### 下面是实例的完整pom.xml,开发时可以参考下

```markup
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<!-- parent> <groupId>com.toone.v3.platform</groupId> <artifactId>platform-parent</artifactId> 
		<version>3.4.0-SNAPSHOT</version> </parent -->
	<groupId>com.yindangu.demo</groupId>
	<modelVersion>4.0.0</modelVersion>
	<artifactId>v3func</artifactId>
	<version>1.1.0</version>
	<packaging>jar</packaging>

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
		<!-- dependency>
		    <groupId>com.yindangu.demo</groupId>
			<artifactId>util</artifactId>
			<version>0.0.1-SNAPSHOT</version>
		</dependency -->
		
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

实例代码：

```java
package com.yindangu.demo;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Date;
import java.util.List;
import java.util.Map;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.toone.itop.paas.extension.api.IFunction;
/**
 * 指定数据实体某行某列的值转换为汉字大写
代码示例:NumberUpperFunc(3,"name",实体)，返回值: 九万二千二百八十七。
入口: com.yindangu.demo.NumberUpperFunc
参数1--行数(数值类型)；
参数2--列名(字符) 
参数3--日期时间
返回指定行列值的汉字大写。 
 * @author jiqj
 *
 */
public class NumberUpperFunc  implements IFunction {
	private static final Logger log = LoggerFactory.getLogger(NumberUpperFunc.class);
	public NumberUpperFunc(){
		log.info("函数:指定数据实体某行某列的值转换为汉字大写");
	}

	public Object evaluate(IFuncContext context) {
		/////////////////参数检查///////////////////
		Number rowIdx = (Number)context.getParams(0);//参数1--行数(数值类型)
		String column = (String)context.getParams(1);//参数2--列名(字符) 
		Date today = (Date)context.getParams(2);//参数3--日期时间
		//List<Map> entity = (List<Map>)context.getParams(3);//参数4--实体
		if(rowIdx == null){
			throw new RuntimeException("参数1--行数不能为空！");
		}
		if(column == null){
			throw new RuntimeException("参数2--列名不能为空！");
		}
		if(today == null){
			;//throw new RuntimeException("参数3--实体不能为空！");
		}
				
		
		////////////////业务实现 api 完全与V平台无关////////////////////
		BusinessFunc fb = new BusinessFunc();
		String rs = fb.execute(rowIdx.intValue(),column,today);
		return rs;
	}
	

	/**
	 * 单机调试代码
	 * @param args
	 */
	public static void main(String[] args){
		String s = "92287";
		if(args!=null && args.length>0){
			s = args[0];
		}
		List<Map> en = new ArrayList<Map>();
		en.add(Collections.EMPTY_MAP);
		final List<Object> pars = new ArrayList<Object>();
		pars.add(Integer.valueOf(s));
		pars.add("列名x");
		pars.add(en);
		
		IFuncContext fc = new IFuncContext() { 
			public int getParamSize() { 
				return pars.size();
			}
			
			public Object getParams(int idx) { 
				return (idx < pars.size() ? pars.get(idx) : null);
			}
		};
		
		IFunction  u = new NumberUpperFunc(); 
		Object n = u.evaluate(fc);
		System.out.println("函数返回:"  + n);
	}
}
```

NumberUpperFunc 参数说明：

```java
入口: com.yindangu.demo.NumberUpperFunc
参数1--行数(数值类型)；
参数2--列名(字符) 
参数3--日期时间
```

NumberUpperFunc 相当于一个接收参数的壳，BusinessFunc 才是真正的业务处理的实现

```java
BusinessFunc fb = new BusinessFunc();
String rs = fb.execute(rowIdx.intValue(),column,today);
return rs;
```

BusinessFunc 的具体代码，开发时请按实际业务开发：

```java
package com.yindangu.demo;

import java.util.Calendar;
import java.util.Date;

import com.yindangu.demo.util.Number2UppercaseUtil;

/**具体的业务类(完全与V平台无关了)*/
class BusinessFunc{
	/**业务实现*/
	public String execute(int rowIdx, String column,Date today){
		String ns =Number2UppercaseUtil.toUpperCase(rowIdx);
		String dates = "可选参数3日期";
		if(today!=null){
			Calendar c = Calendar.getInstance();
			c.setTime(today);
			dates = c.get(Calendar.YEAR) + "-" + (c.get(Calendar.MONTH)+1)
					+ "-" + c.get(Calendar.DATE)
					+ " " + c.get(Calendar.HOUR_OF_DAY)
					+ ":" + c.get(Calendar.MINUTE)
					+ ":" + c.get(Calendar.SECOND);
		}
		return "函数正确运行,入参(" + rowIdx +  "," + column + ",日期参数:" + dates + "),返回:" + ns; 
	}
}
```

Number2UppercaseUtil是数字转汉字大写的工具类，是第三方jar。如果插件需要第三方jar包时，发布构件需要提交给服务器打包的。

```java
com.yindangu.demo.util.Number2UppercaseUtil
```

### 规则程序架构

#### 规则插件需要实现接口：

```java
com.toone.itop.paas.extension.api.IRule
```

