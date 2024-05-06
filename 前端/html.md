# HTML

[toc]

B/S

B:Browser浏览器

S:Server服务器

## 基础语法

```html
<!--
    HTML
        超文本标记语言
        基础语法
             标签
                  单标签
                       无属性<标签名/>
                       有属性<标签名属性名="属性值” />
                  双标签
                       无属性<标签名></标签名>
                       有属性<标签名属性名-"属性值"></标签名>
              整体结构
                   <html></html>表示当前是一个网页
                   <head></head>头部信息
                   <body</body>身体部分
              doctype
                    <doctype html> htm15版本声明,需要写在文档的第一行
-->
<!--网页区域-->
<html>
    <doctype html>
    <!--头部区域-->
    <head>
        <meta charset="utf-8" />
        <title>基础语法</title><!-页面的标题,也是收藏网页时默认的名字->
        <link rel="stylesheet" href="引入的css文件的路径" />
        <script src="引入的js文件的路径" type="text/javascript" charset="utf-8"</script
    </head>
    <!--内容区域:浏览器可见内容-->
    <body>
        hello
    </body>
</html>
```

常用标签

上级目录

…/表示源文件所在目录的上一级目录，…/…/表示源文件所在目录的上上级目录，以此类推。

所有标签都有的属性

| 属性  | 作用                             |
| ----- | -------------------------------- |
| id    | 用来标识元素的唯一性             |
| name  | 提交数据时的参数名               |
| style | 设置元素的行内样式（具体的样式） |
| class | 设置元素的样式名                 |

标签之间的属性要以空格隔开

### body标签属性

| 属性    | 作用     | 值                                |
| ------- | -------- | --------------------------------- |
| bgcolor | 背景颜色 | 1.颜色名 <br>2.RGB <br>3.16进制   |
| text    | 字体颜色 | 1.颜色名 <br/>2.RGB <br/>3.16进制 |

### 标题标签

```html
<h1></h1>~~~~<h6></h6>
<!--不建议写多个h1-->
```

### 水平线标签

```html
<hr>
默认居中
```

| 属性  | 作用     | 值                                    |
| ----- | -------- | ------------------------------------- |
| width | 定义宽度 | 1.百分百<br>2.px                      |
| align | 对齐方式 | 1.left左<br>2.right右<br>3.center居中 |
| size  | 线的粗细 |                                       |

段落标签

```html
<p>段落会自动换行
```

| 属性  | 作用     | 值                                                         |
| ----- | -------- | ---------------------------------------------------------- |
| align | 对齐方式 | 1.left左<br>2.right右<br>3.center居中<br>4.justify两端对齐 |

### 换行标签

```html
<br>
```

### 列表

#### 有序列表

```
<ol>
    <li></li>
    <li></li>
</ol>
```

| 属性 | 作用         | 值                                                           |
| ---- | ------------ | ------------------------------------------------------------ |
| type | 定义列表样式 | 1.1数字序号（默认）<br>2.a小写字母<br>3.A大写字母<br>4.i小写罗马字符<br>5.I大写罗马字符 |

#### 无序列表

```html
<ul>
    <li></li>
    <li></li>
</ul>
```

| 属性 | 作用         | 值                                                          |
| ---- | ------------ | ----------------------------------------------------------- |
| type | 定义列表样式 | 1.square 实心方块<br>2.circle空心圆<br>3.dise实心圆（默认） |

### 块级标签

```html
<div></div>
```

| 属性  | 作用     | 值                                                         |
| ----- | -------- | ---------------------------------------------------------- |
| align | 对齐方式 | 1.left左<br>2.right右<br>3.center居中<br>4.justify两端对齐 |

```html
<spean></spean><!--块、行类元素、标签不会自动换行-->
```

### 格式化标签

```html
<font></font>
```

| 属性  | 作用     | 值                                |
| ----- | -------- | --------------------------------- |
| color | 字体颜色 | 1.颜色名 <br/>2.RGB <br/>3.16进制 |
| face  | 更改字体 | 字体                              |
| size  | 字体大小 | 1-7                               |

```html
<pre></pre><!--保留文本中的换行和空格字符-->
```

```html
加粗<b></b>或者<strong></strong>
斜体<i></i>
下划线<u></u>
中划线<del></del>
下标<sub></sub>
上标<sup></sup>
```

### a标签

```html
超链接<a></a>
```

| 属性   | 作用                                                         | 值                                                           |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| herf   | 可能是其他或当前页面<br/>1.可以被点击<br/>2.点击后跳转到指定URL<br/>保留1去掉2,：`href="javascript:void(0)"` | url                                                          |
| target | 规定在何处打开链接文档。<br/>blank:开启新页面显示页面; <br/>self:当前页面显示跳转到页面,默认值。<br/>top:用于有frameset布局的页面,想要覆盖整个页面显示。<br/>Framename:这里framename与上边的值不同,具体以为frame起了什么样的名字为准,该值指示要连接的页面跳转后将在相应名称的框架中显示。 | blank <br/>parent<br/>self<br/>top<br/>Framename作为锚点的a标签的name值 |

锚点

```html
<!--回到当前页面的顶端herf的值等于#-->
<a herf="#"></a>
<!--herf属性指向a标签的name属性值-->
<a name="top"></a>
<a herf="#top"></a>
<!--herf属性指向其他标签的id属性值-->
<p id="top"></p>
<a herf="#top"></a>
```

### 图片标签

```html
<img src="" alt="">
```

| 属性   | 作用                                             | 值                                                 |
| ------ | ------------------------------------------------ | -------------------------------------------------- |
| alt    | 规定图像的替代文本，一般在图片无法显示占位得文字 | text                                               |
| src    | 规定显示图像的url                                | url                                                |
| align  | 规定如何根据周围的文本来排列图像                 | 1.top<br>2.bottom<br>3.middle<br>4.left<br>5.right |
| border | 定义图像周围的边框                               | px                                                 |
| height | 定义图像的高度                                   | px,%                                               |
| width  | 定义图像的宽度                                   | px,%                                               |
| title  | 当鼠标咋子图片上时显示的文字                     | 文本                                               |

### 表格

```html
<table style="border-collapse:collapse;">
    <!--border-collapse:collapse;css样式合并边框-->
    <tr>
        <!--标签定义表格的行,tr元素包含一个或多个th或td元素-->
        <th><!--定义表格内的表头单元格。--></th>
    </tr>
    <tr>
        <td><!--标签定义HTML表格中的标准单元格。--></td>
    </tr>
</table>
```

| 属性   | 作用             | 值                |
| ------ | ---------------- | ----------------- |
| algin  | 表格对齐方式     | right,center,left |
| border | 规定表格边框宽度 | px                |
| width  | 规定表格的宽度   | px,%              |

`<tr>`属性

| 属性    | 作用                 | 值                |
| ------- | -------------------- | ----------------- |
| align   | 定义表格横向对齐方式 | right,left,center |
| bgcolor | 定义背景颜色         | rgb,#,colorname   |
| valgin  | 定义纵向对齐方式     | top,middil,bottom |
| colspan | 横向合并单元格       | 数字              |
| rowspan | 纵向合并单元格       | 数字              |

### 表单

```html
<from></from>
```

| 属性   | 作用                             | 值                                     |
| ------ | -------------------------------- | -------------------------------------- |
| action | 规定提交表单时向何处发送表单数据 | URL                                    |
| method | 规定表单发送form-data的http方法  | get,post                               |
| name   | 规定表单的名称                   | from_name                              |
| target | 规定在何处打开action URL         | \_biank,\_self\_parent,_\top framename |

**method:表单提交方式：get,post**

* get:默认,主动的获取方式,数据放在url上,数据的容量有限,安全性差,有缓存git比post快两倍
* post:数据放在请求实体中,数据量理论上没有限制,相对安全,没有缓存 

### input元素

```html
<input>
```

| 属性      | 作用                                                         | 值                                                           |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| disabled  | 禁用提交                                                     | disabled                                                     |
| alt       | 定义图像输入的替代文本                                       | text                                                         |
| checked   | 规定input元素首次加载时应当被选中                            | checked                                                      |
| disabled  | 当input元素加载时禁用此元素                                  | disabled                                                     |
| readonly  | 规定输入字段为只读                                           | readonly                                                     |
| maxlength | 规定输入字段中的字符的最大长度                               | number                                                       |
| value     | 规定input元素的值                                            | value                                                        |
| type      | 规定input元素的类型，按钮复选框文件隐藏<br/>域或图像形按钮密码单选框重置按钮提交按钮文本 | 1.button普通按钮<br>2.checkbox<br/>3.file<br/>4.hidden隐藏域<br/>5.image<br/>6.password<br/>7.radio<br/>8.text<br/>9.submit提交按钮<br/>10.reset重置按钮<br/>11.date日期框 |

* 单选框需要使用name属性设置为一组
* 如果上传文件的表单，则表单需要设置一个属性值enctype="nultipart/form-data",提交方式为post请求
* 没有name属性无法提交数据

### textarea

```html
<textarea></textarea>
多行文本输入控件
```

| 属性 | 作用     | 值   |
| ---- | -------- | ---- |
| cols | 可见宽度 | px   |
| rows | 可见行数 | px   |

### lable

```html
<lable for="uname"><input type="text" name="uname" id="uname"/></lable>
```

* 当for属性与元素的id属性值一致时，点击lable会自动元素聚焦
* 是for元素与id元素连接

### 按钮标签button

| 属性     | 作用             | 值                                                  |
| -------- | ---------------- | --------------------------------------------------- |
| disabled | 禁用该按钮       | disabled                                            |
| type     | 规定按钮的类型   | button普通按钮<br/>submit提交按钮<br/>reset重置按钮 |
| value    | 规定按钮的初始值 | text                                                |
| name     | 规定按钮的名称   | button_name                                         |

### select下拉列表

```html
<select name="color">
    <option value="red"></option>
</select>
```

| 属性《select》 | 作用     | 值                         |
| -------------- | -------- | -------------------------- |
| disabled       | disabled | 禁用该下拉框               |
| multiple       | multiple | 规定可选择多个选项         |
| name           | name     | 规定下拉列表的名称         |
| size           | namber   | 规定下拉列表可见选项的数目 |

| 属性《option》 | 作用         | 值                                             |
| -------------- | ------------ | ---------------------------------------------- |
| disabled       | disabled     | 禁用该下拉框                                   |
| selected       | selected默认 | 规定选项（在首次显示在列表中时）表现为选中状态 |
| value          | text         | 定义送往服务器的选项值                         |

### 常用字符实体

| 显示结果 | 描述   | 实体名称 | 实体编号 |
| -------- | ------ | -------- | -------- |
|          | 空格   | \&nbsp;  | \&#160   |
| <        | 小于号 | \&lt;    | \&#60    |
| >        | 大于号 | \&gt;    | \&#38    |
| ©        | 版权   | \&copy   | \&#169   |

### 标签分类

* 块状元素
* 行内元素
* 行内块状元素



## flex弹性布局

# Bootstrap
