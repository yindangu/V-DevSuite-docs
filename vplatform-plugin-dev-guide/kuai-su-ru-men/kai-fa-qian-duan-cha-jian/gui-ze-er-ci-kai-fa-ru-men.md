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
			},{
				"code":"sum",
				"name":"总价",
				"type":"number",
				"desc":"转换的总价数值",
				"default":null,
				"editor":{
					"type":"expression"
				}
			},{
				"code":"entity",
				"name":"实体",
				"type":"entity",
				"desc":"转换的实体数值",
				"default":null,
				"editor":{
					"type":"entity"
				},
				"fields":[{
					"code":"id",
					"name":"编码",
					"type":"char",
					"desc":"编码数据"
				},{
					"code":"sum",
					"name":"总价",
					"type":"integer",
					"desc":"总价数据"
				},{
					"code":"sum_cn",
					"name":"总价（汉字）",
					"type":"char",
					"desc":"总价数据"
				}]
			},{
				"code":"field",
				"name":"字段编码",
				"type":"char",
				"desc":"需要转换成大写金额的字段编码",
				"default":null,
				"editor":{
					"type":"expression"
				}
			},{
				"code":"outField",
				"name":"字段编码",
				"type":"char",
				"desc":"转换成大写金额保存的字段编码",
				"default":null,
				"editor":{
					"type":"expression"
				}
			}],
			"outputs":[{
				"code":"price_cn",
				"type":"char",
				"name":"单价",
				"desc":"转换后的单价数值"
			},{
				"code":"sum_cn",
				"type":"char",
				"name":"总价",
				"desc":"转换后的总价数值"
			},{
				"code":"entity",
				"name":"实体",
				"type":"entity",
				"desc":"转换的实体数值",
				"default":null,
				"editor":{
					"type":"entity"
				},
				"fields":[{
					"code":"id",
					"name":"编码",
					"type":"char",
					"desc":"编码数据"
				},{
					"code":"sum",
					"name":"总价",
					"type":"integer",
					"desc":"总价数据"
				},{
					"code":"sum_cn",
					"name":"总价（汉字）",
					"type":"char",
					"desc":"总价数据"
				}]
			}]
	}]
}
```

## 本地开发

## 本地验证

## 规则部署

## 规则安装

## 规则使用

