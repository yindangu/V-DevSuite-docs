# V-DevSuite插件开发参考指南

## **前言**

欢迎阅读这份文档！

V-DevSuite\(银弹谷零代码开发工具套件\)是运用先进的管理理念和设计方法构建的新一代零代码、可视化软件应用开发平台，可以通过拓展插件解决差异化的平台需求。

本文档即适用于V-DevSuite应用开发者，也可供希望理解V-DevSuite插件原理和实现的高级用户参考

## **简介**

### **什么是V-DevSuite插件**

V-DevSuite\(银弹谷零代码软件开发套件\)是通过拖、拉、拽配置和模块化组装，软件企业和个人开发者可快速构建覆盖PC、手机（平板）、智能设备等多终端的软件应用程序。

对于一个企业级应用服务平台，一个庞大、臃肿的软件，并不是我们的设计目标。因此，我们在对V-DevSuite产品目标定位成更轻量、更开放的架构，通过不断扩展的插件来适应不同的需求场景，成为一个支持个性化定制的平台。

V-DevSuite只关注基础功能的提供（如：基础规则、函数、控件、表设计、查询...），基础应用的提供（如：流程、权限、组织、登录、账户、门户、定时任务、事项消息...）以及模块的管理（如：安装、运行、升级、卸载...），其他技术或平台工具则以插件（Plugin）形式开放给开发者。

### **插件与V-DevSuite的关系**

* 所有V-DevSuite插件以构件方式安装到V-DevSuite，可上传至VStore（云仓库）并使用VTeam（软件开发协同工具）进行构件清单的管理。
* V-DevSuite对所有开发者扩展的V-DevSuite插件都是一致对待处理的
* V-DevSuite插件可以随V-DevSuite安装、升级和卸载，不会影响V-DevSuite的运行

### **V-DevSuite支持的插件类型**

（持续更新中...）

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x89C4;&#x5219;</td>
      <td style="text-align:left">
        <p>V-DevSuite&#x4E2D;&#x7684;&#x57FA;&#x672C;&#x4E1A;&#x52A1;&#x903B;&#x8F91;&#x5355;&#x5143;&#xFF0C;&#x591A;&#x4E2A;&#x89C4;&#x5219;&#x53EF;&#x901A;&#x8FC7;if&#x3001;else&#x3001;for
          each&#x7EC4;&#x6210;&#x4E00;&#x4E2A;&#x89C4;&#x5219;&#x94FE;&#xFF0C;&#x5F62;&#x6210;&#x4E1A;&#x52A1;&#x903B;&#x8F91;&#x7247;&#x6BB5;&#xFF0C;&#x4F9B;&#x754C;&#x9762;&#x6216;&#x540E;&#x7AEF;&#x7684;&#x4E8B;&#x4EF6;&#xFF08;&#x5982;&#xFF1A;&#x8868;&#x5355;&#x52A0;&#x8F7D;&#x4E8B;&#x4EF6;&#x3001;&#x6309;&#x94AE;&#x6309;&#x4E0B;&#x4E8B;&#x4EF6;&#x3001;&#x6D41;&#x7A0B;&#x542F;&#x52A8;&#x4E8B;&#x4EF6;&#x3001;&#x4EFB;&#x52A1;&#x63D0;&#x4EA4;&#x4E8B;&#x4EF6;...&#xFF09;&#x89E6;&#x53D1;&#x6267;&#x884C;&#x3002;</p>
        <p>&#x89C4;&#x5219;&#x6709;&#x5BA2;&#x6237;&#x7AEF;&#x4E0E;&#x670D;&#x52A1;&#x7AEF;&#x4E4B;&#x5206;&#xFF0C;&#x5BA2;&#x6237;&#x7AEF;&#x89C4;&#x5219;&#x6267;&#x884C;&#x7EAF;js&#x4EE3;&#x7801;&#x903B;&#x8F91;&#xFF0C;&#x5728;&#x6D4F;&#x89C8;&#x5668;&#x8FD0;&#x884C;&#xFF0C;&#x670D;&#x52A1;&#x7AEF;&#x89C4;&#x5219;&#x6267;&#x884C;&#x7EAF;java&#x4EE3;&#x7801;&#x903B;&#x8F91;&#xFF0C;&#x5728;jvm&#x8FD0;&#x884C;&#x3002;</p>
        <p>V-DevSuite&#x63D0;&#x4F9B;&#x4E86;&#x4E30;&#x5BCC;&#x7684;&#x901A;&#x7528;&#x89C4;&#x5219;&#x5E93;&#xFF0C;&#x80FD;&#x591F;&#x8986;&#x76D6;&#x5927;&#x591A;&#x6570;&#x4E1A;&#x52A1;&#x573A;&#x666F;&#x7684;&#x5B9E;&#x73B0;&#xFF0C;&#x5BF9;&#x4E8E;&#x5B9A;&#x5236;&#x5316;&#x7684;&#x573A;&#x666F;&#xFF0C;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;V-DevSuite&#x63D2;&#x4EF6;&#x4E8C;&#x6B21;&#x5F00;&#x53D1;&#x89C4;&#x5219;&#x6765;&#x6EE1;&#x8DB3;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x51FD;&#x6570;</td>
      <td style="text-align:left">
        <p>V-DevSuite&#x4E2D;&#x7684;&#x57FA;&#x672C;&#x4E1A;&#x52A1;&#x903B;&#x8F91;&#x5355;&#x5143;&#xFF0C;&#x51FD;&#x6570;&#x5728;&#x8868;&#x8FBE;&#x5F0F;&#x4E2D;&#x6267;&#x884C;&#xFF0C;&#x8868;&#x8FBE;&#x5F0F;&#x652F;&#x6301;&#x591A;&#x4E2A;&#x51FD;&#x6570;&#x7684;&#x5D4C;&#x5957;&#x6267;&#x884C;&#x3002;&#x8868;&#x8FBE;&#x5F0F;&#x901A;&#x5E38;&#x5728;&#x6267;&#x884C;&#x8868;&#x8FBE;&#x5F0F;&#x89C4;&#x5219;&#x6216;&#x89C4;&#x5219;&#x94FE;&#x4E2D;&#x7684;if&#x5224;&#x65AD;&#x8868;&#x8FBE;&#x5F0F;&#x4E2D;&#x6267;&#x884C;&#x3002;</p>
        <p>&#x51FD;&#x6570;&#x6709;&#x5BA2;&#x6237;&#x7AEF;&#x4E0E;&#x670D;&#x52A1;&#x7AEF;&#x4E4B;&#x5206;&#xFF0C;&#x5BA2;&#x6237;&#x7AEF;&#x51FD;&#x6570;&#x6267;&#x884C;&#x7EAF;js&#x4EE3;&#x7801;&#x903B;&#x8F91;&#xFF0C;&#x5728;&#x6D4F;&#x89C8;&#x5668;&#x8FD0;&#x884C;&#xFF0C;&#x670D;&#x52A1;&#x7AEF;&#x51FD;&#x6570;&#x6267;&#x884C;&#x7EAF;java&#x4EE3;&#x7801;&#x903B;&#x8F91;&#xFF0C;&#x5728;jvm&#x8FD0;&#x884C;&#x3002;</p>
        <p>V-DevSuite&#x63D0;&#x4F9B;&#x4E86;&#x4E30;&#x5BCC;&#x7684;&#x901A;&#x7528;&#x51FD;&#x6570;&#x5E93;&#xFF0C;&#x80FD;&#x591F;&#x8986;&#x76D6;&#x5927;&#x591A;&#x6570;&#x4E1A;&#x52A1;&#x573A;&#x666F;&#x7684;&#x5B9E;&#x73B0;&#xFF0C;&#x5BF9;&#x4E8E;&#x5B9A;&#x5236;&#x5316;&#x7684;&#x573A;&#x666F;&#xFF0C;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;V-DevSuite&#x63D2;&#x4EF6;&#x4E8C;&#x6B21;&#x5F00;&#x53D1;&#x51FD;&#x6570;&#x6765;&#x6EE1;&#x8DB3;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x63A7;&#x4EF6;</td>
      <td style="text-align:left">
        <p>V-DevSuite&#x4E2D;&#x7684;&#x9875;&#x9762;&#x5143;&#x7D20;&#x5355;&#x5143;&#xFF08;&#x5982;&#xFF1A;&#x7A97;&#x4F53;&#x3001;&#x6309;&#x94AE;&#x63A7;&#x4EF6;&#x3001;&#x8868;&#x683C;&#x63A7;&#x4EF6;&#x3001;&#x6587;&#x672C;&#x63A7;&#x4EF6;...&#xFF09;&#xFF0C;&#x901A;&#x8FC7;&#x62D6;&#x3001;&#x62C9;&#x3001;&#x62FD;&#x914D;&#x7F6E;&#x7A97;&#x4F53;&#x4E2D;&#x7684;&#x63A7;&#x4EF6;&#xFF0C;&#x63A7;&#x4EF6;&#x4E2D;&#x7684;&#x4E8B;&#x4EF6;&#x914D;&#x7F6E;&#xFF08;&#x5982;&#xFF1A;&#x7A97;&#x4F53;&#x52A0;&#x8F7D;&#x540E;&#x4E8B;&#x4EF6;&#xFF0C;&#x6309;&#x94AE;&#x70B9;&#x51FB;&#x540E;&#x4E8B;&#x4EF6;&#xFF0C;&#x8868;&#x683C;&#x884C;&#x5207;&#x6362;&#x4E8B;&#x4EF6;...&#xFF09;&#x3002;</p>
        <p>&#x63A7;&#x4EF6;&#x6709;&#x79FB;&#x52A8;&#x7AEF;&#x3001;PC&#x7AEF;&#x4E4B;&#x5206;&#xFF0C;&#x6267;&#x884C;&#x7EAF;js&#x4EE3;&#x7801;&#x903B;&#x8F91;&#xFF0C;&#x5728;&#x6D4F;&#x89C8;&#x5668;&#x8FD0;&#x884C;&#x3002;</p>
        <p>V-DevSuite&#x63D0;&#x4F9B;&#x4E86;&#x4E30;&#x5BCC;&#x7684;&#x63A7;&#x4EF6;&#x5E93;&#xFF0C;&#x80FD;&#x591F;&#x8986;&#x76D6;&#x5927;&#x591A;&#x6570;&#x4E1A;&#x52A1;&#x573A;&#x666F;&#x7684;&#x5B9E;&#x73B0;&#xFF0C;&#x5BF9;&#x4E8E;&#x5B9A;&#x5236;&#x5316;&#x7684;&#x573A;&#x666F;&#xFF0C;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;V-DevSuite&#x63D2;&#x4EF6;&#x4E8C;&#x6B21;&#x5F00;&#x53D1;&#x63A7;&#x4EF6;&#x6765;&#x6EE1;&#x8DB3;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Command</td>
      <td style="text-align:left">
        <p>&#x7528;&#x4E8E;&#x5904;&#x7406;HTTP&#x7684;&#x8BF7;&#x6C42;&#x4E0E;&#x54CD;&#x5E94;&#xFF08;&#x7C7B;&#x4F3C;&#xFF1A;Servlet&#xFF09;</p>
        <p>Command&#x6267;&#x884C;&#x7EAF;java&#x4EE3;&#x7801;&#xFF0C;&#x5728;jvm&#x4E2D;&#x8FD0;&#x884C;&#x3002;</p>
        <p>&#x53EF;&#x4EE5;&#x901A;&#x8FC7;Command&#x63D2;&#x4EF6;&#x4E8C;&#x6B21;&#x5F00;&#x53D1;&#x6765;&#x5B8C;&#x6210;HTTP&#x8BF7;&#x6C42;&#x7684;&#x7684;&#x5904;&#x7406;&#x53CA;&#x54CD;&#x5E94;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

### **为什么要用V-DevSuite插件**

V-DevSuite插件开发与基于其他开源平台与商业软件的开发，具备以下优势：

* 接口简单，易于开发
* 不侵入框架代码，让开发人员专注于业务逻辑的实现
* 插件以构件（模块）方式进行统一的部署，管理，分发

## **插件的内容**

### **后端插件**

后端插件包（jar包）包括：

1. 插件注册器实现：用于收集各个后端插件的元信息
2. 插件接口实现实现：各个后端插件的接口（interface）实现
3. 第三方依赖jar包：插件需要使用到的第三方依赖jar，需统一放到jar包的lib目录下

后面章节会详细讲解后端插件包的构成及开发过程

### **前端插件**

前端插件包（zip包）包括：

1. manifest.json文件：用于描述前端插件元信息
2. 目标文件：即前端插件的源码js文件
3. 其他文件：如debug相关的资源文件，第三方依赖的资源文件

后面章节会详细讲解前端插件包的构成及开发过程

