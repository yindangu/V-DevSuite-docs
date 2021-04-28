---
description: 需要实现具体的功能是跟踪V平台开发提供的接口进行扩展
---

# 开发后端插件

**前提要求件**

* **需实现平台提供的扩展接口**

例如：如果要实现函数扩展，那么就要实现IFunction接口。 要实现规则扩展，就要实现IRule接口。 要实现HttpCommand扩展，就要实现IHttpCommand接口。 以后平台逐步开放一些标准接口处理

* **plugin-business-api模块\(必须\)**

基础模块。平台开发的接口都放在这个模块，所以必须引用。引用有2种方式，第一种是通过maven引用；第二种是直接通过官网下载这个jar文件

* **plugin-register模块\(推荐\)**

它的功能作用是：构造接口元素描述服务。我们提供的build工具，轻量级的实现，构建插件描述信息

* **plugin-utils模块\(可选\)**

功能作用是一些标准的工具，例如Json,xml,加密、解密等业界标准工具。方便二次开发的工具

**创建工程**

* 创建标准的maven工程

开发插件时，maven不是必须的，最终的成品是标准jar文件就可以了。

* 引用plugin-business-api，plugin-register两个构件

```markup
<?xml version="1.0" encoding="utf-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.yindangu.plugin</groupId>
	<artifactId>plugin-demo</artifactId>
	<name>${project.groupId}-${project.artifactId}</name>
	<packaging>jar</packaging>
	<description>标准的maven项目</description>
	<version>0.0.1-SNAPSHOT</version>

	<properties>
 
	</properties>

	<dependencies>
		<!-- ////////////////插件依赖开始/////////////////// -->
		<dependency>
			<groupId>com.yindangu.v3.platform</groupId>
			<artifactId>plugin-register</artifactId>
			<version>3.3.0</version>
		</dependency>
		<dependency>
			<groupId>com.yindangu.v3.platform</groupId>
			<artifactId>plugin-utils</artifactId>
			<version>3.3.0</version>
		</dependency>
		<!-- ////////////////插件依赖结束//////////////////// -->
		<!-- 解析序列化Json格式数据的第三方jar包 =BEGIN -->
		<dependency>
			<groupId>com.google.code.gson</groupId>
			<artifactId>gson</artifactId>
			<version>2.8.5</version>
		</dependency>
		<!-- 解析序列化Json格式数据的第三方jar包 ==END -->

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
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>servlet-api</artifactId>
			<version>2.5</version>
			<scope>provided</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<configuration>
					<source>1.6</source>
					<target>1.6</target>
				</configuration>
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

