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

元数据文件名称固定为manifest.json，其中各部分定义如下

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
      <td style="text-align:left">
        <p>&#x63A7;&#x4EF6;&#x5206;&#x7C7B;&#xFF0C;&#x679A;&#x4E3E;&#x503C;&#xFF1A;</p>
        <p>generalComponent&#xFF08;&#x901A;&#x7528;&#x63A7;&#x4EF6;&#xFF09;&#x3001;fieldComponent&#xFF08;&#x5B57;&#x6BB5;&#x63A7;&#x4EF6;&#xFF09;&#x3001;businessComponent&#xFF08;&#x4E1A;&#x52A1;&#x63A7;&#x4EF6;&#xFF09;</p>
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
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x7F16;&#x7801;&#xFF0C;&#x5728;&#x63A7;&#x4EF6;&#x4E2D;&#x5E94;&#x4FDD;&#x6301;&#x552F;&#x4E00;</td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x540D;&#x79F0;&#xFF0C;&#x5E94;&#x7B80;&#x8981;&#x660E;&#x786E;&#x8BF4;&#x660E;&#x5C5E;&#x6027;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x7C7B;&#x578B;</td>
    </tr>
    <tr>
      <td style="text-align:left">catalog</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x5206;&#x7C7B;&#xFF0C;&#x679A;&#x4E3E;&#x503C;&#xFF1A;</p>
        <p>Event&#xFF08;&#x4E8B;&#x4EF6;&#xFF09;&#x3001;</p>
        <p>Layout&#xFF08;&#x683C;&#x5F0F;&#xFF09;&#x3001;</p>
        <p>Data&#xFF08;&#x6570;&#x636E;&#xFF09;&#x3001;</p>
        <p>Other&#xFF08;&#x5176;&#x4ED6;&#xFF09;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">default</td>
      <td style="text-align:left">Any</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">null</td>
      <td style="text-align:left">&#x63A7;&#x4EF6;&#x5C5E;&#x6027;&#x9ED8;&#x8BA4;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">editor</td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x7F16;&#x8F91;&#x5668;&#x4FE1;&#x606F;</td>
    </tr>
  </tbody>
</table>

#### 编辑器定义信息\(editor\)

编辑器信息，描述当前属性使用何种编辑器及编辑器元信息；该属性为可选属性，如未设置，则使用文本编辑器编辑；详细参考属性编辑器定义；

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

## 本地开发

目前平台控件是基于smartclient UI框架进行封装的，因此控件二次需要先了解smartclient相关知识，以下提供smartclient官方文档：

1、[smartclient属性说明文档](https://www.smartclient.com/smartclient-release/isomorphic/system/reference/?id=group..docViewerHelp)

2、[smartclient在线样例](https://www.smartclient.com/smartclient/showcase/?id=Welcome)

在了解smartclient相关知识后，就可以按照smartclient扩展规范扩展控件，平台完成对接smartclient数据源，开发人员无需学习平台任何其他控件规范信息，控件定义脚本如下：

```text
isc.ClassFactory.defineClass("JGDevTextBox", "DynamicForm");
isc.JGDevTextBox.addProperties({
	//文本标题
	Alias: "文本",
	//文本高度
	MultiHeight: 30,
	//文本宽度
	MultiWidth: 235,
	//左边距
	Left : 50,
	//绑定数据源
	datasource:null,
	//绑定字段
	fieldCode:null,
	//标题宽度
	TitleWidth:76,
	//上边距
	Top : 50,
	//标题点击事件
	OnLabelClick: null,
	//键盘按下事件
	OnKeyDown: null,
	//焦点离开事件
	OnLeave: null
});
isc.JGDevTextBox.addMethods({
	init: function () {
		this.titleWidth = this.TitleWidth;
		this.left = this.Left;
		this.top = this.Top;
		this.width = this.MultiWidth;
		this.height = this.MultiHeight;
		this.enabled = !this.Disabled;
		this.valuesManager = isc.ValuesManager.getByDatasource(this.datasource);
		this.items = [{
			width:"*",
			title : this.Alias,
			type : "text",
			name : this.fieldCode,
			titleClick : this.OnLabelClick,
			blur : this.handleBlur
		}];
		return this.Super("init", arguments);
	},
	handleBlur : function(){
		//焦点离开后同步文本框的数据到数据源
		this.form.valuesManager.saveData();
		if(this.OnLeave){
			//触发焦点离开事件
			this.OnLeave();
		}
	}
});
```

## 本地验证

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>控件测试页面</title>
    <script src="http://localhost:8080/module-operation!executeOperation?operation=vds-sdk-js"></script>
    <script>
        vds.config({
            debug: true,
            import : "vds.mock.*"
        }).ready(function () {
            vds.mock.init("./manifest.json").then(function (mock) {
                mock.get("JGDevTextBox").then(function (widgetMock) {
                    widgetMock.exec(function(properties){
                        var widget = isc.JGDevTextBox.create(properties);
                        widget.show();
                    });
                }).catch(function (error) {
                    console.error(error.message);
                    throw error;
                });;
            }).catch(function (error) {
                console.error(error.message);
                throw error;
            });;
        });
    </script>
</head>
<body>
    
</body>
</html>
```

其中http://localhost:8080为执行系统服务链接。

## 控件部署

        控件部署前，需要将元数据manifest.json文件及控件定义js文件打包成zip，其中manifest.json文件需放置在根目录下，其他文件可以自定义目录，在元数据中填入相对路径即可。

![&#x63A7;&#x4EF6;&#x538B;&#x7F29;&#x5305;](../../../.gitbook/assets/image%20%2812%29.png)

        此时控件二次开发工作已完成，进入开发系统（开发系统使用参考这里），在开始-》扩展管理-》上传中，选择控件压缩包即可，如下图：

![&#x63A7;&#x4EF6;&#x90E8;&#x7F72;](https://gblobscdn.gitbook.com/assets%2F-MKdnMpEXew2dgfykkLs%2F-MZRI-pVTRR1BShvh5cM%2F-MZRJgelG6oBavhO9LdY%2Fimage.png?alt=media&token=129a4f19-a633-42a2-bc64-daa0c10fc3b6)

## 控件安装

        控件部署完毕后，控件已提交到平台仓库受控，开发系统中还未安装该控件，此时需要使用开发系统中开始-》安装构件-》搜索（搜索值为插件编号）-》安装，如下图：

![&#x63A7;&#x4EF6;&#x5B89;&#x88C5;](../../../.gitbook/assets/image%20%2813%29.png)

待提示构件安装成功后，控件安装完成。

## 控件使用

        待开发系统安装完成后，二次开发控件的使用方法与平台内部提供的控件一样，在普通窗体中拖拽出来使用，如下图：

![&#x63A7;&#x4EF6;&#x4F7F;&#x7528;](../../../.gitbook/assets/image%20%2814%29.png)

