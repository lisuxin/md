# css

[toc]

## 基本语法

```
<样式类型= “文本/css” > 
选择器{
    属性：属性值；
    ...
}
< /风格>
```

- 用鲜花封起来
- 如果属性值由多个单词组成，要给值加上引号

### 行内式

```
<p style = "属性：属性值；" > < / p >
```

### 嵌入式

```
<p > < / p > 
<样式>
p{
    属性：属性值；
}
< /风格>
```

### 引入外联样式文件

```
<link rel = "stlesheet"  type = "text/css"  href = "url" > 
rel = "stlesheet"样式表
type = "text/css"什么样式表
```

- 优先级：就近原则

## 选择器

### 通用选择器

```
* {
    属性：属性值；
}
```

### 元素选择器

```
标签名{
    属性：属性值；
}
```

### id选择器

```
# id属性值{
    属性：属性值；
}
```

- id定义规则以数字线、下不能划线数字划线，

### 类类选择器

```
. 类属性值{
    属性：属性值；
}
```

### 分组选择器

```
元素组合器，id选择器，class类选择器;任意组合{
    属性：属性值；
}
```

- 选择器优先级
- id > 类类选择器 > 元素选择器 > 通用选择器
- 权重：id 100 > class10 > 元素选择器 1 > 通用选择器没有权重
- 行内样式权重最高权重1000

## 组合选择器

### 后代选择器

- 选择指定元素隔开的所有元素（以空格打开）

```
指定元素 指定的子代元素{
    属性：属性值；
}
```

### 子元素选择器

- 选择指定元素的第一代元素（已大于号）

```
元素>指定的第一代元素{
    属性：属性值；
}
```

### 相邻兄弟选择器

- 选择元素的基本的一个指定元素（只找一个）（以加号下）

```
元素+挨着的指定元素{
    属性：属性值；
}
```

### 普通兄弟选择器

- 选择元素后指定的同级元素（已指定的同级线）

```
指定元素~指定元素后面的元素{
    属性：属性值；
}
```

## 常用属性

### 原来

| 属性     | 值                                                         | 作用                           |
| -------- | ---------------------------------------------------------- | ------------------------------ |
| 背景颜色 | rgb;corloname                                              | 设置背景颜色                   |
| 背景图片 | 网址（网址）                                               | 设置元素的背景图像（默认平铺） |
| 背景重复 | no-repeat/不重复 repeat;repeat/横向重复 repeat-y重复重复-x | 是否设置及如何重复背景图像     |
| 背景尺寸 | 像素                                                       | 设置大小                       |

### 设置网页渐变色

```css
background-image: linear-gradient(to top,#4568DC,#B06AB3);
background-image: linear-gradient(方向,颜色1,颜色2.....);
background-image: linear-gradient(1-360deg,颜色1,颜色2.....);
```

| 值              | 方向       |
| --------------- | ---------- |
| 默认            | 向上       |
| to right        | 从左到又   |
| to bottom right | 左上到下右 |

* 如果希望对渐变角度做更多的控制，您可以定义一个角度，来取代预定义的方向（向下、向上、向右、向左、向右下等等）。值 0deg 等于向上（to top）。值 90deg 等于向右（to right）。值 180deg 等于向下（to bottom）。
  180deg

### div常用css属性

* border-style属性用于设置元素所有边框的样式，或者单独地为各边设置边框样式。

```html
<!DOCTYPE html>

<html> 
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            div {
                margin: 10px 0;
            }             
            div.dotted {
                border-style: dotted
            }            
            div.dashed {
                border-style: dashed
            }             
            div.solid {
                border-style: solid
            }             
            div.double {
                border-style: double
            }             
            div.groove {
                border-style: groove
            }             
            div.ridge {
                border-style: ridge
            }             
            div.inset {
                border-style: inset
            }             
            div.outset {
                border-style: outset
            }
        </style>
    </head>
    <body>
        <div class="dotted">点状边框</div>
        <div class="dashed">虚线边框</div>
        <div class="solid">实线边框</div>
        <div class="double">双线边框</div>
        <div class="groove">3D 凹槽边框</div>
        <div class="ridge">3D 垄状边框</div>
        <div class="inset">3D inset 边框</div>
        <div class="outset">3D outset 边框</div>
    </body>
</html>
```

| 值      | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| none    | 定义无边框。                                                 |
| hidden  | 与 "none" 相同。不过应用于表时除外，对于表，hidden 用于解决边框冲突。 |
| dotted  | 定义点状边框。在大多数浏览器中呈现为实线。                   |
| dashed  | 定义虚线。在大多数浏览器中呈现为实线。                       |
| solid   | 定义实线。                                                   |
| double  | 定义双线。双线的宽度等于 border-width 的值。                 |
| groove  | 定义 3D 凹槽边框。其效果取决于 border-color 的值。           |
| ridge   | 定义 3D 垄状边框。其效果取决于 border-color 的值。           |
| inset   | 定义 3D inset 边框。其效果取决于 border-color 的值。         |
| outset  | 定义 3D outset 边框。其效果取决于 border-color 的值。        |
| inherit | 规定应该从父元素继承边框样式。                               |

```html
<style type="text/css">
.box1 {border:1px #cccccc solid;  width:500px; height:600px;position:relative;}
.box2 {border-top:1px #cccccc solid; background:#f2f6fb; width:498px; height:22px; position:absolute; bottom:1;background-color:red;}
</style>
<div class="box1">
    <div class="box2"></div>
</div>
```

### 图片旋转

```css
@-webkit-keyframes rotation {
    from {
        -webkit-transform:rotate(0deg);
    }
    to {
        -webkit-transform:rotate(360deg);
    }
}
.tp {
    -webkit-transform: rotate(360deg);
    animation: rotation 3s linear infinite;
    -moz-animation: rotation 3s linear infinite;
    -webkit-animation: rotation 3s linear infinite;
    -o-animation: rotation 3s linear infinite;
}
```

### 文字居中

```
text-align: center; /*让div内部文字居中*/
```

### div居中

```\
top: 0;
left: 0;
right: 0;
bottom: 0;
```

### css设置背景图片

```
曾经在html中编写网页的时候，<link rel="stylesheet" type="text/css" href="css/css.css"/> 将外部的css样式表链接到网页中，其它像：background-color . padding , margin 等都可以正常起作用，但就是background-image不起作用，而且有时一气之下将background-image:url(“”绝对路径“”) ;就可以显示了，但是我们非常不提倡这种绝对路径的写法，那么出现这个现象的原因到底是什么呢？
注意：：在css样式表中写的background-image:url(图片的路径为相对本css文件的路径，而不是我们通常认为的相对加入css样式的网页的路径);
例如：在当前目录下有 index.html 和 css文件夹(里面包含：css.css) 和 images文件夹（里面包含top.jpg）
错误的认为和写法：background-image:url("images/top.jpg"); ----------------------------------->>错误的认为图片的路径应该是针对index.html网页来说的。
正确的认为和写法：background-image:url("../images/top.jpg");----------------------------------->图片的路径应该写的是相对css.css文件的路径
其中     ../     表示的是上一级目录，不要写成 ./ 这是表示当前目录。
```

###A标签

```
a:link { 
font-size: 12px; 
color: #000000; 
text-decoration: none; 
} 
a:visited { 
font-size: 12px; 
color: #000000; 
text-decoration: none; 
} 
a:hover { 
font-size: 12px; 
color: #999999; 
text-decoration: underline; 
}
a:link {color: #FF0000}     /* 未访问的链接 */
a:visited {color: #00FF00}  /* 已访问的链接 */
a:hover {color: #FF00FF}    /* 当有鼠标悬停在链接上 */
a:active {color: #0000FF}   /* 被选择的链接 */
```
