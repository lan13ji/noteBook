# 初识CSS及常见属性

## CSS是什么

CSS	是	cascading	style	sheet	的缩写。意为层叠式样式表，功能：是从审美的角度给html页面提供样式的

## CSS的基本语法

```html
<head>
    <style type="text/css">
        选择器 {
            key: value;
            key: value;
        }
    </style>
</head>

style标签写在head标签里面
type		类型
text/css	表示纯文本
key			代表属性
value		代表属性值
```

## CSS常见属性

```css
字符颜色——color: colorname/十六进制(#开头)
背景颜色——background-color: colorname/十六进制(#开头)
字号大小——font-size: number(单位px/em/rem/%)
字体加粗/不加粗——font-weight: bold/normal/100~900(整倍数)
斜体/不斜体——font-style: italic/normal
有/无下划线——text-decoration: underline/none
```

**注意：写css样式时，必须通过选择器把想要添加样式的标签选上**



# CSS基础选择器

## 标签选择器

用标签名当做选择器。基本语法是：

```css
element {
    key: value;
}

/* element 代表所有标签(div,p,img,form等)
	1) 所有标签都能够作	选择器
	2) 用标签作选择器，样式会作用所有相同的标签，体现了一种共性 */
```

## id选择器

id，就是标签的id属性基本语法是：

```css
#idName {
    key: value;
}

/* 1) 任何标签都可以定义id
   2) id命名：以 字母 或 下划线 开头，其中可以有数字、下划线、字母 */
```

**注意：**

​	**id名称要严格区分大小写，例如mm和MM，是两个不同的id**

​	**同一个页面(.html文件)内不能重复出现同一id名称**

## 类选择器

类，就是标签的class属性。基本语法：

```css
.classname {
    key: value;
}

/*	1) class 属性可以同时携带多个classname，要用 空格 隔开
	2) classname 可以重复，同一个页面上可以有多个同样的classname出现 */
```

**注意：**

​	**class要尽可能小，要有 “公共类” 概念，可以提供 “公共服务”，任一标签一旦携带了这个classname，就有了相应的样式变化**

> 默认：class定义样式，id定义行为。即JS要通过 id属性 操作标签，给标签添加一些交互行为。
>
> css层面尽可能用class，除非极特殊的情况可以用id。



# CSS高级选择器

高级选择器中含有简单的逻辑关系

## 后代选择器

后代选择器，描述的是祖先结构。当要把某一部分的所有嵌套内容，进行样式改变，就要用后代选择器。基本语法：

```css
.classname .classname { }
element element element { }
.classname element .classname .classname { }
element .classname element element .classname { }

/* 中间空格隔开，空格前选择器是父级及上选择器，空格后选择器是前选择器的后代。
   可以罗列多个层级标签或类名*/
```

## 交集选择器

交集选择器，用来选择两个不同标签或类名交集的选择器。如果先选择两个同属性的标签或类名，后筛选需要改变样式的类名

```css
element.classname { }
.classname.classname { }

/* 交集选择器不限制选择器个数，可以连续多个相交 */
```

**注意：交集选择器中有标签选择器的，要把标签选择器放在前面，因为两个选择器之间没有空格**

## 并集选择器

```css
element,.classname1,.classname2 { }

/* 选择器之间用 “ , ” 隔开，节省了样式渲染，和文件大小 */
```

## 通配符 *

*** ** 表示所有元素，基本语法：

```css
* { }

/* 效率不高，如果页面上的标签越多，效率越低 */
```



# CSS三大特性

## CSS继承性、层叠性

* 继承性。有一些属性，会继承到所有后代元素上

  1)关于文字样式的(color、font-、text-、line-)，都能够**继承**

  2)关于盒子的、定位的、布局的属性，都**不能继承**

* 层叠性。层叠性是浏览器的一种能力，可以处理冲突。

  **冲突**	当不同选择器，对一个标签的同样的样式属性，有不同的值，听谁的？这就是冲突。CSS通过什么机制处理冲突呢？答案是：权重

  **注意：只覆盖同样的不可重复的样式属性，不会覆盖不重复的属性，不重复的属性会合并下来，包括那些允许设置多个值的属性也会合并**

## CSS优先级（特异性）

**优先级：**

> !important	>	标签内style(行内样式)	>	id选择器	>	类/属性/伪元素/伪类选择器	>	标签(元素)选择器 	>	通配符选择器 (*)	>	继承样式

优先级高的规则会忽视层叠性，忽视**就近原则**来定义样式。特别是!important，即使行内样式离得近，最终生效的还是!important标注的属性

### 权重的计算方法

|                        | 贡献值      |
| ---------------------- | ----------- |
| !important             | **∞**无穷大 |
| 标签内**style属性**    | 1，0，0，0  |
| id选择器               | 0，1，0，0  |
| 类、属性、伪元素、伪类 | 0，0，1，0  |
| 标签                   | 0，0，0，1  |
|                        | 0，0，0，0  |

**注意：权重之和(权值)没有进位制，不能用数学进位相加运算计算权值。比如：10个类选择器权重加和，也比不上1个id选择器**

### !important标记的性质

基本语法：

```css
{
    key: value!important;
}
```

**注意：**

​	**1)	!important	提升的是属性的权重，不是一个选择器的。**

​	**2)	!important	无法提升继承的权重**

​	**3)	!important	实操中尽量不使用，仅在极特殊情况下可以使用**

​	**4） 如果都是继承来的，！important 不影响就近原则。**

### 选择器间如何计算权重

* 情况一：三个不同权重的选择器作用在同一标签上

  ```css
  /* 1个id选择器，1个类选择器，1个标签选择器————权重记作：0,1,1,1 */
  #idname .classname ele { }
  
  /* 1个id选择器，0个类选择器，3个标签选择器————权重记作：0,1,0,3*/
  ele ele #idname ele { }
  
  /* 0个id选择器，3个类选择器，4个标签选择器————权重记作：0,0,3,4 */
  ele.classname ele.classname ele.classname ele { }
  
  /* 三个权重比较后，第一个组合选择器的样式会作用于内容 */
  ```

* 情况二：如果权重是一样，考虑**就近原则**

  ```css
  /* 1个类选择器，1个标签选择器————权重记作：0,0,1,1*/
  .classname ele { }
  
  /* 1个类选择器，1个标签选择器————权重记作：0,0,1,1 */
  ele.classname { }
  
  /* 1个类选择器，1个标签选择器————权重记作：0,0,1,1 */
  ele .classname { }
  
  /*	1)css文件中	哪组选择器写在样式表后面
  	2)style标签中	哪组选择器描述的最靠近内容
  它的样式就会覆盖前面的样式。那它的样式就会作用于内容 */
  ```
  

  
* 情况三：通过继承影响的，权重为0

**注意：标签中携带多个类名，在有冲突情况下，样式的作用与调用类名的顺序无关，只和定义样式的顺序有关**



# CSS盒模型

## CSS盒子模型基本属性

> 一个盒子中主要的属性：width、height、padding、border。

width	指的是内容的宽度，而不是盒子的宽度

height	指的是内容的高度，而不是盒子的高度

padding	是盒子的——内边距

border	是盒子的——边框

> 盒子的真实宽度为：**border**+**padding**+**width**
>
> 盒子的真实高度为：**border**+**padding**+**height**

![](assets/02css-model.jpg)

**margin	是盒子的——外边距，不是盒模型范畴**

##	详说padding

padding的四个方向一级表述方式：

- 小属性(单独写)

  ```css
  padding-top: number(单位px/em/rem/%);		/*上*/
  padding-right: number(单位px/em/rem/%);	/*右*/
  padding-bottom: number(单位px/em/rem/%);	/*下*/
  padding-left: number(单位px/em/rem/%);	/*左*/
  ```

* 综合属性

  * 4个属性值写在一起，顺序是：上，右，下，左

    ```css
    padding: top right bottom left;
    ```

  * 3个属性值写在一起，顺序是：上，左右，下

    ```css
    padding: top left-right bottom;	/* 左右的边距一样 */
    ```

  * 2个属性值写在一起，顺序是： 上下，左右

    ```css
    padding: top-bottom left-right; /* 上下边距一样，左右边距一样 */
    ```

  * 1个属性值，顺序是：上右下左

    ```css
    padding: top-right-bottom-left; /* 上下左右的边距一样 */
    ```

* 小属性层叠大属性

  ```css
  padding: number(单位px/em/rem/%);
  padding-top(right/bottom/left): number(单位px/em/rem/%);
  
  /* 小属性特指的值覆盖大属性对应的值 */
  ```

## 详说border

边框三要素：宽度(粗细)、线型、颜色。颜色如果不定义，默认值是黑色

* 小属性(单独写)

  ```css
  border-top/right/bottom/left-width: number(单位px/em/rem)
  border-top/right/bottom/left-style: solid/dotted/dashed/double
  border-top/right/bottom/left-color: colorname/十六进制(#开头)
  
  /* 实线solid、虚线dotted、点状dashed、双线double */
  ```

* 小属性层叠大属性

  ```css
  /* 边框颜色不同 */
  border: width style color;
  border-color: top-color right-color bottom-color left-color
  border-right-color: color; /* 实例：右边框颜色小属性 */
  
  /* 边框样式不同 */
  border: width style color;
  border-style: solid dashed double dotted;
  border-bottom-style: dotted; /* 实例：下边框样式小属性 */
  
  /* 边框粗细不同 */
  border: width style color;
  border-width: width width width width;
  border-left-width: width; /* 实例：左边框粗细小属性 */
  ```



# CSS标准文档流

web页面制作，是个 “流” ，必须从上往下，一点点绘制。

## 标准文档流的微观现象

### 空白折叠现象

* 标签与标签之间紧密连接，浏览器呈现的两个内容也是紧密相连，中间没有空格
* 标签与标签之间有一个空格，浏览器呈现的两个内容中间也有一个空格的间隙
* 标签与标签之间有一个以上的空格（n>1），浏览器呈现的两个内容之间也只有一个空格的间隙

通过第三个现象可知，多出的空格折叠了，这就是所谓的**空白折叠现象**。

### 高矮不齐，底边对齐

浏览器中两个不同内容出现高低不一致时，底边对齐![](assets/03baseline.jpg)

### 自动换行

块级元素和行内元素

在HTML中，标签被分为：文本级、容器级

## css标准流将标签分为：

### 块级元素

* 霸占一行，不能与其他任何元素并列一行
* 能接受宽、高
* 如果不设置宽度，默认为父盒子的100%

### 行内元素

* 与其他行内元素并排
* 不能设置宽、高。由内容撑起盒子的宽高，即文本宽高

### p元素

p是文本级标签，但是个块级元素。其他文本级标签，都是行内元素![](assets/04ele-cate.jpg)

### 块级元素和行内元素的互换

> display 是 “ 显示模式 ” 的意思，用来改变元素的行为、块级性质。

* 块级元素可以设置为行内元素

  基本语法：

  ```css
  display: inline;
  
  /* inline 就是 “行内”。会将块级元素立即变为行内元素。*/
  /* 此时的块级元素，不能设置宽度、高度；可以并排显示 */
  ```

* 行内元素可以设置为块级元素

  基本语法：

  ```css
  display: block;
  
  /* block 就是 “块”。会将行内元素立即变为块级元素。*/
  /* 此时的行内元素，可以设置宽度、高度； 独立一行，无法并排显示。如果不设置宽度，值为100%。 */
  ```

  