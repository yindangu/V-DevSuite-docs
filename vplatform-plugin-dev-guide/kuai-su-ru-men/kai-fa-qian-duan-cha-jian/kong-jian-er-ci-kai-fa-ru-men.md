---
description: >-
  本文档将详细介绍前端控件如何进行二次开发，并辅以样例进行说明；适合无任何V平台前端控件二次开发经验的开发人员进行阅读。本文将以文本框为例，详细阐述整个开发过程。
---

# 控件二次开发入门

## 开发流程

        在进行前端控件二次开发之前，首先需要了解前端控件二次开发的开发流程，以便于在整体轮廓上理解二次开发流程。如下图：

![&#x63A7;&#x4EF6;&#x5F00;&#x53D1;&#x6D41;&#x7A0B;](../../../.gitbook/assets/image%20%2811%29.png)

## 元数据编辑

        在二次开发控件前，首先需要明确当前控件需求，确定当前控件名称、属性及事件等信息。当以上信息固化下来后，控件元信息已经完成，以下为元数据详细描述，其内容格式：

```text
{
    groupId:"com.yindangu.widget",//组织id
    code:"JGDevTextBox",   
    plugins:[{
			"type": "widget",
			"icon": "./JGDevTextBox.png",
			"code": "JGDevTextBox",
			"name": "二次开发文本",
			"desc": "简单的二次开发文本控件",
			"defineUrl": "./JGDevTextBox.js",
			"visible": true,
			"properties": [{
					"code": "Alias",
					"name": "标题",
					"desc": "文本中显示的标题",
					"default": "按钮",
					"type": "char",
					"editor": {
						"type": "char",
						"placeholder": "请输入标题"
					},
					"access": {
						"rule": {
							"readable": true,
							"writable": true
						},
						"webDesigner": {
							"readable": true,
							"writable": true
						}
					}
				}, {
					"code": "Top",
					"name": "上边距",
					"desc": "上边距",
					"type": "integer",
					"default": 0,
					"editor": {
						"type": "top"
					}
				}, {
					"code": "Left",
					"name": "左边距",
					"desc": "左边距",
					"type": "integer",
					"default": 0,
					"editor": {
						"type": "left"
					}
				}, {
					"code": "MultiWidth",
					"name": "宽度",
					"desc": "宽度",
					"type": "integer",
					"default": 50,
					"editor": {
						"type": "width"
					}
				}, {
					"code": "MultiHeight",
					"name": "高度",
					"desc": "高度",
					"default": 50,
					"type": "integer",
					"editor": {
						"type": "height"
					}
				},{
					"code": "datasource",
					"name": "数据源",
					"desc": "绑定数据源",
					"default": null,
					"type": "char",
					"editor": {
						"type": "entity"
					}
				},{
					"code": "fieldCode",
					"name": "字段",
					"desc": "绑定的数据源字段",
					"default": null,
					"type": "char",
					"editor": {
						"type": "field",
						"entityProp":"datasource"
					}
				},{
					"code": "TitleWidth",
					"name": "标题宽度",
					"desc": "标题宽度",
					"default": 76,
					"type": "integer",
					"editor": {
						"type": "integer",
						"min":0
					}
				}, {
					"code": "OnLabelClick",
					"name": "标题点击事件",
					"type": "funtion",
					"desc": "点击标题时触发",
					"editor": {
						"type": "ruleset"
					}
				}, {
					"code": "OnKeyDown",
					"name": "键盘按下事件",
					"type": "funtion",
					"desc": "键盘按下时触发",
					"editor": {
						"type": "ruleset"
					}
				}, {
					"code": "OnLeave",
					"name": "焦点离开事件",
					"type": "funtion",
					"desc": "焦点离开时触发",
					"editor": {
						"type": "ruleset"
					}
				}, {
					"code": "Disabled",
					"name": "禁用",
					"type": "boolean",
					"desc": "禁用控件",
					"editor": {
						"type": "boolean"
					},
					"access": {
						"rule": {
							"readable": true,
							"writable": true
						},
						"webDesigner": {
							"readable": true,
							"writable": true
						}
					}
				}
			]
	}]
}

```

{% embed url="https://元数据文件名称固定为manifest.json，其中各部分定义如下：" %}

### plugins定义

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
      <td style="text-align:left">&#x679A;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63D2;&#x4EF6;&#x7C7B;&#x578B;&#xFF0C;&#x63A7;&#x4EF6;&#x4E3A;widget</td>
    </tr>
    <tr>
      <td style="text-align:left">icon</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x56FE;&#x6807;</td>
    </tr>
    <tr>
      <td style="text-align:left">code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x7F16;&#x7801;&#xFF0C;&#x5E94;&#x5168;&#x5C40;&#x4FDD;&#x6301;&#x552F;&#x4E00;</td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x540D;&#x79F0;&#xFF0C;&#x5E94;&#x7B80;&#x8981;&#x660E;&#x786E;&#x8BF4;&#x660E;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">scope</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">smartclient</td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5E94;&#x7528;&#x8303;&#x56F4;&#xFF0C;&#x53EF;&#x7528;&#x679A;&#x4E3E;&#x503C;&#xFF1A;smartclient</td>
    </tr>
    <tr>
      <td style="text-align:left">catalog</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">businessComponent</td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5206;&#x7C7B;&#xFF0C;&#x9ED8;&#x8BA4;&#x4E3A;&#x4E1A;&#x52A1;&#x6784;&#x4EF6;(businessComponent),&#x53EF;&#x679A;&#x4E3E;&#x503C;&#x53C2;&#x8003;&#xFF1A;
        <a
        href="https://docs.qq.com/doc/DREhCWEZpQ3NKYmVn">&#x63A7;&#x4EF6;&#x5206;&#x7C7B;</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x63A7;&#x4EF6;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">author</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5F00;&#x53D1;&#x8005;</td>
    </tr>
    <tr>
      <td style="text-align:left">visible</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">
        <p>&#x662F;&#x5426;&#x5728;&#x8BBE;&#x8BA1;&#x5668;&#x4E2D;&#x663E;&#x793A;&#xFF0C;</p>
        <p>&#x5982;&#x679C;&#x4E0D;&#x663E;&#x793A;&#xFF0C;</p>
        <p>&#x5219;properties&#x5C5E;&#x6027;&#x53EF;&#x4EE5;&#x4E0D;&#x8BBE;&#x7F6E;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">defineUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">./define.js</td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5B9A;&#x4E49;&#x811A;&#x672C;&#x6587;&#x4EF6;url</td>
    </tr>
    <tr>
      <td style="text-align:left">debugUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">./debug.js</td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x8C03;&#x8BD5;&#x811A;&#x672C;&#x6587;&#x4EF6;url</td>
    </tr>
    <tr>
      <td style="text-align:left">designerDefineUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">./designerDefine.js</td>
      <td style="text-align:left">&#x8BBE;&#x8BA1;&#x5668;&#x5B9A;&#x4E49;&#x811A;&#x672C;&#x6587;&#x4EF6;url</td>
    </tr>
  </tbody>
</table>

### properties属性

properties属性值为数据组，方便属性在编辑器中显示时，进行排序，首先根据属性分类信息进行分组，组内再按照数组中的位置进行排序。其中属性分类信息优先使用属性catalog值，如未设置，则使用编辑器中的分类信息。该属性为可选属性，如未设置，则代表控件无任何属性；properties属性值中每一个数组元素定义一个控件属性，其中控件属性包括以下信息：

定义属性编号，名称，描述及默认值信息；该属性为必填属性，详情如下：

| 编码 | 值类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| code | String | 是 |  | 控件属性编码，在控件中应保持唯一 |
| name | String | 是 |  | 控件属性名称，应简要明确说明属性用途 |
| type | String | 是 |  | 控件属性类型 |
| catalog | String | 否 |  | 控件属性分类，枚举值参考：[控件属性分类枚举](https://docs.qq.com/doc/DREhCWEZpQ3NKYmVn) |
| desc | String | 否 |  | 控件属性描述，详细描述控件属性用途 |
| default | Any | 否 | null | 控件属性默认值 |
| editor | Object | 否 |  | 编辑器信息 |

#### 编辑器定义信息\(editor\)

编辑器信息，描述当前属性使用何种编辑器及编辑器元信息；该属性为可选属性，如未设置，则使用文本编辑器编辑；详细参考[属性编辑器定义](https://docs.qq.com/doc/DREtEV1RRdG9MRm9S)；

#### 访问信息\(access\)

定义属性访问权限，该属性为可选属性，如不存在，则代表其属性都采用默认值，其中：

**设计器\(designer\)**

详细描述设计器中该属性的访问权限信息，详情如下：

| 编码 | 值类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| visible | Boolean | true | 是否在设计器中显示，控件可能定义私有属性，不需要在设计器中显示 |

有些控件在配置时,需要配置子控件信息,且该子控件不单独作为控件提供,如列表的列配置,列表列配置中需要有属性需要标识列类型,就需要用到此属性配置.

**规则（rule）**

详细描述规则中该属性的访问权限信息，详情如下：

| 编码 | 值类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| readable | Boolean | true | 描述该属性是否能在规则中读取 |
| writable | Boolean | true | 描述该属性是否能在规则中编辑 |

**web设计器（webDesigner）**

详细描述web设计器中该属性的访问权限信息（tips:如设计器完全web化后，此配置应与designer合并）。详情如下：

| 编码 | 值类型 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- |
| readable | Boolean | true | 描述该属性是否能在web设计器中读取 |
| writable | Boolean | true | 描述该属性是否能在web设计器中编辑 |

本地开发

本地验证

控件部署

控件安装

控件使用

