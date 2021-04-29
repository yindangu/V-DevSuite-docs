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

元数据文件名称固定为manifest.json，其中各部分定义如下：

本地开发

本地验证

控件部署

控件安装

控件使用

