# Html

## 简介

### 基本结构

```html
<!--
	这是一个展示html基本结构的示例代码
	根标签下有两个一级子标签
	<head>头标签，定义那些不直接展示在页面主体上，但是又很不重要的内容
			字符集、css引入、js引入
	<body>体标签，定义要展示到页面主题上的标签
-->
<!DOCTYPE html>
<html>
    <head>
        <title>第一个页面</title>
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>
            这是一个一级标题
        </h1>
    </body>
</html>
```

- 标签 tag	<>单双标签
- 属性 attribute 对标签特征进行一些设置
- 文本 text 双标签中间的文字
- 元素 element 开始标签+属性+文本+结束标签成为一个元素

### 语法细节

- 根标签有且只能有一个
- 单双标签都要正确关闭
- 标签可以嵌套，但不能交叉嵌套
- 属性必须有值，且必须加引号。H5不严格区分单双引号
- 标签不严格区分大小写，但不能大小写混用
- 不允许自定义标签名

## html常见标签

### 标题、段落、换行标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>这是一个一级标题</h1>
    <h2>这是一个二级标题</h2>
    <h3>这是一个三级标题</h3>
    <!--标题标签从h1到h6-->
    <p>这是第一段
        这里不会换行
    </p>
    <p>这是第二段<br/>
        这里会换一行
    </p>
    <p>
        这是第三段<hr/>
        上面会有一个分割线
    </p>
</body>
</html>
```

### 列表标签

```html
<!--
        有序列表 ol
        无序列表 ul
        列表项   li
    -->
    <ol>
        <li>数据类型</li>
        <li>变量</li>
        <li>函数</li>
        <li>对象</li>
        <li>继承</li>
    </ol>
    <ul>
        <li>C</li>
        <li>C#</li>
        <li>C++</li>
        <li>JAVA</li>
        <li>PYTHON</li>
    </ul>
```

### 超链接标签

```html
<!--
        超链接标签
            a
                href用于定义跳转的地址
                    完整url
                    相对路径    可以以./或者../开头
                    绝对路径
                target用于定义目标资源的打开方式
                    _self在当前页面打开
                    _blank在新窗口打开
    -->
    <a href = 'https://www.baidu.com' target = '_self'>百度一下你就知道</a>
    <a href = '03列表标签.html' target = '_blank'>列表标签</a>
```

P14