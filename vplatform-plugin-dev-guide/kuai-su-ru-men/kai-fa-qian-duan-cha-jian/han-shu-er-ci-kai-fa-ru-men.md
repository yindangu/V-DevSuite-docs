---
description: >-
  本文档将详细介绍前端函数如何进行二次开发，并辅以样例进行说明；适合无任何V平台前端函数二次开发经验的开发人员进行阅读。本文以将金额转换成中文为例（453.564转换为：肆佰伍拾叁元伍角陆分肆毫），详细阐述整个开发过程。
---

# 函数二次开发入门

## 开发流程

         在进行前端函数二次开发之前，首先需要了解前端函数二次开发的开发流程，以便于在整体轮廓上理解二次开发流程。如下图

![&#x524D;&#x7AEF;&#x51FD;&#x6570;&#x5F00;&#x53D1;&#x6D41;&#x7A0B;](../../../.gitbook/assets/image.png)

## 本地开发

        抛开V平台函数二次开发规范，在本地需要实现此需求，我们该怎么做？ 首先新建一个js文件（如：moneyToChinese.js），在js文件中定义一个方法，在方法体中实现需求，如下所示：

```bash
var moneyToChinese = function(money){
    //这里编写实现逻辑，并返回结果
}
```

         如此，该需求实现完毕。现在深入思考下，上面存在什么问题？ 因moneyToChinese定义为全局方法，有可能会被其他引入的第三方js库或其他开发人员编写的代码给覆盖掉，因此平台建议给函数添加命名空间，命名空间规范建议使用java的包名规范。现在我们改造下上述代码：

```bash
//命名空间为：com.yindangu.client.function.convert
com = this.com||{};
com.yindangu = com.yindangu||{};
com.yindangu.client = com.yindangu.client||{};
com.yindangu.client.function = com.yindangu.client.function||{};
com.yindangu.client.function.moneyToChinese = function(money){
    //这里编写实现逻辑，并返回结果
}
```

       至此，整个函数逻辑开发完毕。

## 本地验证

      沿用普通js验证方法，首先创建一个html文件（如：index.html），引入上述新建的js文件，编写验证逻辑进行验证。

```bash
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>函数验证</title>
        <script src="./moneyToChinese.js"></script>
        <script>
            var res = com.yindangu.client.function.moneyToChinese(456.14);
            console.log(res);
        </script>
    </head>
    <body>
    </body>
</html>
```

## 元数据编辑

平台前端函数中，除了函数的实现逻辑外，还需要一些其他的信息（如函数描述，入参及返回值定义等），因此需要添加一份元数据。元数据文件名称固定为manifest.json，其内容格式如下：

```bash
{
    groupId:"com.yindangu.vplatform",//组织id
    code:"moneyToChinese",//插件编号
    plugins:[{
        type:"function",//插件类型
        code:"moneyToChinese",//函数编号
        name:"金额转大写汉字",//函数名称
        entry:"com.yindangu.client.function.moneyToChinese",//函数主入口
        desc:"将金额转换成大写汉字，如：453.564 -> 肆佰伍拾叁元伍角陆分肆毫",//函数描述
        author:"",//开发者
        example:"moneyToChinese(514.24)",//使用样例
        defineUrl:"./moneyToChinese.js",//函数定义文件url
        debugUrl:"",//函数测试验证文件url
        inputs:[{//函数入参信息定义,可选
            type:"number",//入参类型，
            desc:"金额",//入参描述，
            required:true,//是否必填
            default:null//默认值
        }],
        output:{//可选
            type:"char",//函数输出类型,
            desc:""//函数输出描述
        }
    }]
}

```

### plugins定义

定义函数基本信息，属性值为数组，详细描述如下：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7F16;&#x7801;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">&#x679A;&#x4E3E;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x524D;&#x7AEF;&#x51FD;&#x6570;&#x4E3A;function</td>
    </tr>
    <tr>
      <td style="text-align:left">code</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>&#x51FD;&#x6570;&#x7F16;&#x7801;&#xFF0C;&#x5E94;&#x5168;&#x5C40;&#x4FDD;&#x6301;&#x552F;&#x4E00;&#xFF0C;&#x672C;&#x6587;&#x4E2D;&#x4E3A;&#xFF1A;</p>
        <p>moneyToChinese</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x540D;&#x79F0;&#xFF0C;&#x5E94;&#x7B80;&#x8981;&#x660E;&#x786E;&#x8BF4;&#x660E;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">entry</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x5165;&#x53E3;&#x65B9;&#x6CD5;&#xFF0C;&#x672C;&#x6587;&#x4E2D;&#x4E3A;&#xFF1A;com.yindangu.client.function.moneyToChinese</td>
    </tr>
    <tr>
      <td style="text-align:left">defineUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">./define.js</td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x5B9A;&#x4E49;&#x811A;&#x672C;&#x6587;&#x4EF6;url&#xFF0C;&#x76F8;&#x5BF9;&#x4E8E;&#x5143;&#x6570;&#x636E;&#x6587;&#x4EF6;&#x8DEF;&#x5F84;</td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x51FD;&#x6570;&#x7528;&#x9014;</td>
    </tr>
    <tr>
      <td style="text-align:left">author</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x5F00;&#x53D1;&#x8005;</td>
    </tr>
    <tr>
      <td style="text-align:left">example</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x4F7F;&#x7528;&#x6837;&#x4F8B;</td>
    </tr>
    <tr>
      <td style="text-align:left">debugUrl</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">./debug.js</td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x6D4B;&#x8BD5;&#x811A;&#x672C;&#x6587;&#x4EF6;url</td>
    </tr>
  </tbody>
</table>

### inputs定义

定义函数入参，属性值为数组，详细描述如下：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7F16;&#x7801;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">&#x679A;&#x4E3E;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>&#x5165;&#x53C2;&#x7C7B;&#x578B;&#xFF0C;&#x679A;&#x4E3E;&#x9879;&#xFF1A;</p>
        <p>char-&#x6587;&#x672C;&#xFF0C;</p>
        <p>text-&#x957F;&#x6587;&#x672C;&#xFF0C;</p>
        <p>number-&#x5C0F;&#x6570;&#xFF0C;</p>
        <p>boolean-&#x5E03;&#x5C14;&#xFF0C;</p>
        <p>date-&#x65E5;&#x671F;&#xFF0C;</p>
        <p>longDate-&#x957F;&#x65E5;&#x671F;&#xFF0C;</p>
        <p>integer-&#x6574;&#x578B;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x5165;&#x53C2;&#x63CF;&#x8FF0;,&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x5165;&#x53C2;&#x4FE1;&#x606F;</td>
    </tr>
    <tr>
      <td style="text-align:left">required</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x586B;</td>
    </tr>
    <tr>
      <td style="text-align:left">default</td>
      <td style="text-align:left">Any</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">null</td>
      <td style="text-align:left">&#x5165;&#x53C2;&#x9ED8;&#x8BA4;&#x503C;</td>
    </tr>
  </tbody>
</table>

### output定义

定义函数输出信息，属性值为Object，详细描述如下：



<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7F16;&#x7801;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>&#x8F93;&#x51FA;&#x7C7B;&#x578B;:</p>
        <p>char-&#x6587;&#x672C;&#xFF0C;</p>
        <p>text-&#x957F;&#x6587;&#x672C;&#xFF0C;</p>
        <p>number-&#x5C0F;&#x6570;&#xFF0C;</p>
        <p>boolean-&#x5E03;&#x5C14;&#xFF0C;</p>
        <p>date-&#x65E5;&#x671F;&#xFF0C;</p>
        <p>longDate-&#x957F;&#x65E5;&#x671F;&#xFF0C;</p>
        <p>integer-&#x6574;&#x578B;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">desc</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x51FD;&#x6570;&#x8F93;&#x51FA;&#x63CF;&#x8FF0;&#xFF0C;&#x8BE6;&#x7EC6;&#x63CF;&#x8FF0;&#x51FD;&#x6570;&#x8F93;&#x51FA;</td>
    </tr>
  </tbody>
</table>

## 函数部署

函数部署前，需要将元数据manifest.json文件及函数定义js文件打包成zip，其中manifest.json文件需放置在根目录下，其他文件可以自定义目录，在元数据中填入相对路径即可。

![&#x51FD;&#x6570;&#x538B;&#x7F29;&#x5305;](../../../.gitbook/assets/image%20%284%29.png)

此时函数二次开发工作已完成，进入开发系统（开发系统使用参考这里），在开始-》扩展管理-》上传中，选择函数压缩包即可，如下图：

![&#x51FD;&#x6570;&#x90E8;&#x7F72;](../../../.gitbook/assets/image%20%281%29.png)

## 函数安装

函数部署完毕后，函数已提交到平台仓库受控，开发系统中还未安装该函数，此时需要使用开发系统中开始-》安装构件-》搜索（搜索值为插件编号）-》安装，如下图：

![&#x51FD;&#x6570;&#x5B89;&#x88C5;](../../../.gitbook/assets/image%20%283%29.png)

待提示构件安装成功后，构件安装完成。

## 函数使用

待开发系统安装完成后，二次开发函数的使用方法与平台内部提供的函数一样，在表达式编辑器中直接使用，如下图：

![](../../../.gitbook/assets/image%20%285%29.png)

## 高阶晋级

### nodejs环境

随着nodejs在前端开发中盛行，以下介绍如何在nodejs环境中二次开发函数。相较于普通方式二次开发函数，在nodejs环境中开发函数多了一个步骤，即将源码打包成适合在浏览器中运行的脚本。

首先按照nodejs规范创建nodejs插件，编写源码。如下图：

![](../../../.gitbook/assets/image%20%282%29.png)

使用打包插件打包源码，本文已rollup为例，配置如下：

```bash
import babel from "rollup-plugin-babel";
import { terser } from 'rollup-plugin-terser';
// rollup.config.js
export default {
  input: 'src/moneyToChineseFunc.js',//源码主入口路径
  output: {
    file: 'dist/moneyToChineseFunc.js',//打包输出路径
    format:'umd',//编译出umd格式
    name:'com.yindangu.client.function',//定义全局命名空间
    sourcemap:true
  },
  plugins: [
    babel({ runtimeHelpers: true }),//babel转换
    terser()//脚本压缩
  ]
};
```

配置详细含义请前往rollup官网查看，待打包完成后，调整manifest.json文件，将函数定义中defineUrl执行打包结果文件即可。

### 集成使用vds

