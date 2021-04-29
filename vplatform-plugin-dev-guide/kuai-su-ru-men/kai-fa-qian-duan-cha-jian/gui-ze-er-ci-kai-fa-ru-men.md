---
description: >-
  本文档将详细介绍前端规则如何进行二次开发，并辅以样例进行说明；适合无任何V平台前端规则二次开发经验的开发人员进行阅读。本文以将金额转换成中文为例（453.564转换为：肆佰伍拾叁元伍角陆分肆毫），详细阐述整个开发过程。
---

# 规则二次开发入门

## 开发流程

        在进行前端规则二次开发之前，首先需要了解前端规则二次开发的开发流程，以便于在整体轮廓上理解二次开发流程。如下图

![&#x89C4;&#x5219;&#x5F00;&#x53D1;&#x6D41;&#x7A0B;](../../../.gitbook/assets/image%20%287%29.png)

## 元数据定义

        在二次开发规则前，首先需要明确当前规则需求，确定当前规则名称、配置及返回值等信息。当以上信息固化下来后，规则元信息已经完成，以下为元数据详细描述，其内容格式：

```text
{
    groupId:"com.yindangu.client.rule",//组织id
    code:"moneyToChinese",//插件编号
    plugins:[{
			"type":"rule",//插件类型，规则为rule
			"code":"NumToChineseRule",//规则编号
			"catalog":"other",//规则分类
			"name":"数字转大写汉字(前端规则)",//规则名称
			"desc":"数字转大写汉字(前端规则)",//规则描述
			"transactionType":"none",//是否有事务
			"entry":"com.yindangu.client.rule.moneyToChineseRule",//规则主入口
			"defineUrl":"./moneyToChineseRule.js",//规则定义脚本url
			"debugUrl":"./debug.js",//调试脚本url
			"inputs":[{//规则输入信息
				"code":"money",//输入编号
				"name":"单价",//输入名称
				"type":"number",//输入类型
				"desc":"转换前的单价数值",//输入描述
				"default":null,//默认值
				"editor":{//输入编辑器
					"type":"expression"//编辑器类型
				}
			}],
			"outputs":[{
				"code":"out",
				"type":"char",
				"name":"转换结果",
				"desc":"转换后结果"
			}]
	}]
}
```

元数据文件名称固定为manifest.json，其中各部分定义如下：

### plugins属性

定义控件基本信息，详情如下：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7F16;&#x7801;</th>
      <th style="text-align:left">&#x503C;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">Enum</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63D2;&#x4EF6;&#x7C7B;&#x578B;&#xFF0C;&#x89C4;&#x5219;&#x4E3A;rule</td>
    </tr>
    <tr>
      <td style="text-align:left">code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x7F16;&#x7801;&#xFF0C;&#x5E94;&#x5168;&#x5C40;&#x4FDD;&#x6301;&#x552F;&#x4E00;</td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x540D;&#x79F0;&#xFF0C;&#x5E94;&#x7B80;&#x8981;&#x660E;&#x786E;&#x8BF4;&#x660E;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">entry</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x4E3B;&#x5165;&#x53E3;</td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x89C4;&#x5219;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">author</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5F00;&#x53D1;&#x8005;</td>
    </tr>
    <tr>
      <td style="text-align:left">scope</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">client</td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5E94;&#x7528;&#x8303;&#x56F4;&#xFF0C;&#x679A;&#x4E3E;&#x503C;&#xFF1A;client&#xFF08;&#x5BA2;&#x6237;&#x7AEF;&#xFF09;&#x3001;server&#xFF08;&#x670D;&#x52A1;&#x7AEF;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">catalog</td>
      <td style="text-align:left">Enum</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">other</td>
      <td style="text-align:left">
        <p>&#x89C4;&#x5219;&#x6240;&#x5C5E;&#x76EE;&#x5F55;&#xFF0C;&#x679A;&#x4E3E;&#x503C;&#xFF1A;</p>
        <p>count&#xFF08;&#x8BA1;&#x7B97;&#x3001;&#x8D4B;&#x503C;&#xFF09;&#x3001;</p>
        <p>check&#xFF08;&#x68C0;&#x67E5;&#x3001;&#x63D0;&#x793A;&#xFF09;&#x3001;</p>
        <p>control&#xFF08;&#x63A7;&#x4EF6;&#x64CD;&#x4F5C;&#xFF09;&#x3001;</p>
        <p>entity&#xFF08;&#x5B9E;&#x4F53;&#x64CD;&#x4F5C;&#xFF09;&#x3001;</p>
        <p>query&#xFF08;&#x7B5B;&#x9009;&#x3001;&#x67E5;&#x8BE2;&#x3001;&#x641C;&#x7D22;&#xFF09;&#x3001;</p>
        <p>import&#xFF08;&#x6570;&#x636E;&#x5BFC;&#x5165;&#x3001;&#x5BFC;&#x51FA;&#xFF09;&#x3001;</p>
        <p>database&#xFF08;&#x6570;&#x636E;&#x5E93;&#x64CD;&#x4F5C;&#xFF09;&#x3001;</p>
        <p>other&#xFF08;&#x5176;&#x4ED6;&#x64CD;&#x4F5C;&#xFF09;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">transactionType</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">none</td>
      <td style="text-align:left">
        <p>&#x4E8B;&#x52A1;&#x7C7B;&#x578B;,&#x679A;&#x4E3E;&#x503C;:</p>
        <p>transaction(&#x6709;&#x4E8B;&#x52A1;),</p>
        <p>none(&#x65E0;&#x4E8B;&#x52A1;),</p>
        <p>unknown(&#x672A;&#x77E5;)&#xFF0C;</p>
        <p>&#x8BE6;&#x60C5;&#x53C2;&#x8003;&#xFF1A;<a href="https://docs.qq.com/doc/DREhCWEZpQ3NKYmVn">&#x89C4;&#x5219;&#x4E8B;&#x52A1;&#x7C7B;&#x578B;</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">defineUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">./define.js</td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5B9A;&#x4E49;&#x811A;&#x672C;&#x6587;&#x4EF6;url</td>
    </tr>
    <tr>
      <td style="text-align:left">debugUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x6D4B;&#x8BD5;&#x811A;&#x672C;&#x6587;&#x4EF6;url</td>
    </tr>
  </tbody>
</table>

### inputs属性

inputs属性值为数据组，方便属性在编辑器中显示时，进行排序，但此顺序不是最高优先级，最高优先级为属性采用的属性编辑器，规则配置界面中，优先按照属性编辑器进行分组，按照内定的顺序进行排序，统一组内再按照属性定义中的顺序进行排序，即：先根据属性编辑器进行分组，组内再按照inputs中的顺序进行排序；该属性为可选属性，如未设置，则代表规则无任何属性；inputs属性值中每一个数组元素定义一个控件属性，其中规则属性包括以下信息：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7F16;&#x7801;</th>
      <th style="text-align:left">&#x503C;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5C5E;&#x6027;&#x7F16;&#x7801;&#xFF0C;&#x5728;&#x63A7;&#x4EF6;&#x4E2D;&#x5E94;&#x4FDD;&#x6301;&#x552F;&#x4E00;</td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5C5E;&#x6027;&#x540D;&#x79F0;&#xFF0C;&#x5E94;&#x7B80;&#x8981;&#x660E;&#x786E;&#x8BF4;&#x660E;&#x5C5E;&#x6027;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">Enum</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">text</td>
      <td style="text-align:left">
        <p>&#x5C5E;&#x6027;&#x7C7B;&#x578B;&#xFF1A;</p>
        <p>char-&#x6587;&#x672C;&#xFF0C;</p>
        <p>text-&#x957F;&#x6587;&#x672C;&#xFF0C;</p>
        <p>number-&#x5C0F;&#x6570;&#xFF0C;</p>
        <p>boolean-&#x5E03;&#x5C14;&#xFF0C;</p>
        <p>date-&#x65E5;&#x671F;&#xFF0C;</p>
        <p>longDate-&#x957F;&#x65E5;&#x671F;&#xFF0C;</p>
        <p>integer-&#x6574;&#x578B;,</p>
        <p>entity-&#x5B9E;&#x4F53;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5C5E;&#x6027;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">default</td>
      <td style="text-align:left">Any</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">null</td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5C5E;&#x6027;&#x9ED8;&#x8BA4;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">editor</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">null</td>
      <td style="text-align:left">&#x5C5E;&#x6027;&#x7F16;&#x8F91;&#x5668;&#x4FE1;&#x606F;</td>
    </tr>
  </tbody>
</table>

#### 编辑器定义信息\(editor\)

编辑器信息，描述当前属性使用何种编辑器及编辑器元信息；该属性为可选属性，如未设置，则使用文本编辑器编辑；详细参考[属性编辑器定义](https://docs.qq.com/doc/DREtEV1RRdG9MRm9S)；

### outputs属性

属性值为Array,数组中每个数组项详情定义如下:

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7F16;&#x7801;</th>
      <th style="text-align:left">&#x503C;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x8F93;&#x51FA;&#x7F16;&#x7801;</td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x8F93;&#x51FA;&#x540D;&#x79F0;&#xFF0C;&#x5E94;&#x7B80;&#x8981;&#x660E;&#x786E;&#x8BF4;&#x660E;&#x8F93;&#x51FA;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">null</td>
      <td style="text-align:left">
        <p>&#x8F93;&#x51FA;&#x7C7B;&#x578B;&#xFF1A;</p>
        <p>char-&#x6587;&#x672C;&#xFF0C;</p>
        <p>text-&#x957F;&#x6587;&#x672C;&#xFF0C;</p>
        <p>number-&#x5C0F;&#x6570;&#xFF0C;</p>
        <p>boolean-&#x5E03;&#x5C14;&#xFF0C;</p>
        <p>date-&#x65E5;&#x671F;&#xFF0C;</p>
        <p>longDate-&#x957F;&#x65E5;&#x671F;&#xFF0C;</p>
        <p>integer-&#x6574;&#x578B;,</p>
        <p>entity-&#x5B9E;&#x4F53;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89C4;&#x5219;&#x5C5E;&#x6027;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">fields</td>
      <td style="text-align:left">Array</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x5F53;&#x8F93;&#x51FA;&#x7C7B;&#x578B;&#x4E3A;entity&#x65F6;,&#x4F7F;&#x7528;&#x6B64;&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x5B9E;&#x4F53;&#x5217;&#x4FE1;&#x606F;</td>
    </tr>
  </tbody>
</table>

## 本地开发

## 本地验证

## 规则部署

## 规则安装

## 规则使用

