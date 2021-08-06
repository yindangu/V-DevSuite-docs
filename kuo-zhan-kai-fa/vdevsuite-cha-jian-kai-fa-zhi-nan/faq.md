# FAQ

1、发布的构件不生效，优先检查构件时间戳是否相同

a\)每个错误必须的第一项检查：构件是否发布到执行系统。构件时间戳是否相同就表示构件系统

打开本地的jar下的META-INF/MANIFEST.MF 的Bnd-LastModified属性值，对照系统构件的时间戳

![&#x672C;&#x5730;&#x6784;&#x4EF6;](../../.gitbook/assets/image%20%2839%29.png)

打开执行系统的本地构件管理，点击对应的构件，显示详细信息

![&#x7CFB;&#x7EDF;&#x751F;&#x6548;&#x7684;&#x6784;&#x4EF6;](../../.gitbook/assets/image%20%2837%29.png)

1、引用第三放jar，运行时报ClassNotFoundException.

a\)每个错误必须的第一项检查：构件是否发布到执行系统。构件时间戳是否相同就表示构件系统：

b\)检查云编译时的jar是否有包含lib目录，并且第三方的jar也在里面。

c\)检查本地构件的信息是否有包含第三方的依赖。

![&#x4F9D;&#x8D56;&#x4E86;&#x7B2C;&#x4E09;&#x65B9;&#x7684;jar](../../.gitbook/assets/image%20%2838%29.png)

d\)检查发布到执行的信息是否有包含第三方的依赖。

![&#x4F9D;&#x8D56;&#x7B2C;3&#x65B9;&#x5C5E;&#x6027;&#x4FE1;&#x606F;](../../.gitbook/assets/image%20%2840%29.png)

