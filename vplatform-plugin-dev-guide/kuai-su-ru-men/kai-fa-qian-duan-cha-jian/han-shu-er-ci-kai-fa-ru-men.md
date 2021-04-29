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
com = com||{};
com.yindangu = com.yindangu||{};
com.yindangu.client = com.yindangu.client||{};
com.yindangu.client.function = com.yindangu.client.function||{};
com.yindangu.client.function.moneyToChinese = function(money){
    //这里编写实现逻辑，并返回结果
}
```

       至此，整个函数开发完毕。

## 本地验证

      沿用普通js验证方法，首先创建一个html文件（如：index.html），引入上述新建的的js文件，编写验证逻辑进行验证。

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









