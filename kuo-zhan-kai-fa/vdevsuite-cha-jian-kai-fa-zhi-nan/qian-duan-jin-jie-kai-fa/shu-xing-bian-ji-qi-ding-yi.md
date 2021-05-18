---
description: 属性编辑器定义为用户在开系统中使用前端二次开发插件（如：规则、控件等），编辑插件属性时所使用属性编辑器的元数据，本文将详细说明平台目前所支持的属性编辑器。
---

# 属性编辑器定义

|  |  |
| :--- | :--- |
|  |  |

### 编号编辑器

编号编辑器会根据当前上下文自动生成窗体内唯一的编号;如按钮控件，窗体中已存在编号为JGButton1的按钮控件后，用户添加一个按钮到窗体中时，该按钮的编号自动为JGButton2。

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | code | 编辑器类型 |

### 使用样例

```text
{
    type："code"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2819%29.png)

## 文本编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | text | 编辑器类型 |
| required | Boolean | 否 | false | 是否必填 |
| requiredMessage | String | 否 | \[属性名称\]不能为空 | 必填提示 |

### 使用样例

```text
{
    type："text",
    required:true,
    requiredMessage:"账号不能为空"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2821%29.png)

## 日期编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | date | 编辑器类型 |
| required | Boolean | 否 | false | 是否必填 |
| requiredMessage | String | 否 | \[属性名称\]不能为空 | 必填提示 |

### 使用样例

```text
{
    type："date",
    required:true,
    requiredMessage:"出生日期不能为空"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2818%29.png)

## 日期时间编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | dateTime | 编辑器类型 |
| required | Boolean | 否 | false | 是否必填 |
| requiredMessage | String | 否 | \[属性名称\]不能为空 | 必填提示 |

### 使用样例

```text
{
    type："dateTime",
    required:true,
    requiredMessage:"注册时间不能为空"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2818%29.png)

## 布尔编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | boolean | 编辑器类型 |

### 使用样例

```text
{
    type："boolean"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2820%29.png)

## 整数编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | integer | 编辑器类型 |

### 使用样例

```text
{
    type："integer"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2817%29.png)

## 小数编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | float | 编辑器类型 |

### 使用样例

```text
{
    type："float"
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2822%29.png)

## 下拉选择编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | select | 编辑器类型 |
| options | Array | 是 | null | 候选项 |
| required | Boolean | 否 | false | 是否必填 |
| requiredMessage | String | 否 | \[属性名称\]不能为空 | 必填提示 |

其中options为数组，其每个数组元素定义如下：

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| value | Any | 是 |  | 标识值 |
| label | String | 是 |  | 显示值 |

### 使用样例

```text
{
    type:"select",
    required:true,
    requiredMessage:"请选择城市",
    options:[{
        value: 'New York',
        label: 'New York'
    },{
        value: 'London',
        label: 'London'
    }]
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2823%29.png)

## 单选组编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | radioGroup | 编辑器类型 |
| options | Array | 是 | null | 候选项 |
| required | Boolean | 否 | false | 是否必填 |
| requiredMessage | String | 否 | \[属性名称\]不能为空 | 必填提示 |

其中options为数组，其每个数组元素定义如下：

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| value | Any | 是 |  | 标识值 |
| label | String | 是 |  | 显示值 |

### 使用样例

```text
{
    type:"radioGroup",
    required:true,
    requiredMessage:"请选择性别",
    options:[{
        value:"male",
        label:"男"
    },{
        value:"female",
        label:"女"
    }]
}
```

### 界面效果

![](../../../.gitbook/assets/image%20%2816%29.png)

## 宽度编辑器

### 属性列表

| 编码 | 类型 | 必填 | 默认值 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| type | String | 是 | width | 编辑器类型 |
| required | Boolean | 否 | true | 是否必填 |
| requiredMessage | String | 否 | \[属性名称\]不能为空 | 必填提示 |
| disabled | Array | 否 | null | 禁用选项 |

### 使用样例

### 界面效果

## 高度编辑器

### 属性列表

### 使用样例

### 界面效果

## 实体选择器

### 属性列表

### 使用样例

### 界面效果

## 字段选择器

### 属性列表

### 使用样例

### 界面效果

## 实体&字段选择器

### 属性列表

### 使用样例

### 界面效果

## 方法选择器

### 属性列表

### 使用样例

### 界面效果

## 资源选择器

### 属性列表

### 使用样例

### 界面效果

## 左边距编辑器

### 属性列表

### 使用样例

### 界面效果

## 上边距编辑器

### 属性列表

### 使用样例

### 界面效果

## 表达式编辑器

### 属性列表

### 使用样例

### 界面效果









