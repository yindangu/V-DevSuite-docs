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
        type:"widget",
        icon:"",//控件图标
        code:"JGDevTextBox",//控件编号
        name:"二次开发文本",//控件名称
        scope:"smartclient",//控件应用范围
        desc:"",//控件描述
        author:"",//开发者
        defineUrl:"",//控件脚本定义url
        debugUrl:"",//控件测试脚本定义url
        designerDefineUrl:"",//设计器定义脚本url
        visible:true//是否在设计器中显示
	    properties:[{//使用数组，方便属性排序,可选
            code:"",//属性编号，
            name:"".//属性名称，
            type:"",//属性类型
            desc:""//属性描述，
            default:null//默认值,
		    editor:{//编辑器信息，可选
			    type:"",//编辑器类型
		    },
		    access:{//访问权限信息，可选
			    designer:{
				    visible:true,//是否显示
			    },
			    rule:{//规则
				    readable:true,//是否可读
				    writable:true//是否可写
			    },
			    webDesigner:{
				    readable:true,//是否可读
				    writable:true//是否可写
			    }
		    }
	    }],
	    dependencies:[{//控件依赖信息，可选
		    type:""//依赖类型,枚举值：本地资源(asset),云控件(cloud)
	    }]
    }]
}

```

本地开发

本地验证

控件部署

控件安装

控件使用

