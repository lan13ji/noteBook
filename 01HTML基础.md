# HTML是什么

> 什么是HTTP协议？即Hypertext Transfer Protocol的缩写，意思是“超文本传输协议”。 

## HTML基础知识

​		HTML	是	英	语	HyperText	Markup 	Language的缩写，超文本标记语言，它是一种负责描述文档语义的语言。HTML通过标签给文本添加语义。HTML之所以成为 ”超文本“ 是因为它可以通过超链接，连接不同空间的文档，进而与整个web网络连接起来。 

## HTML常用标签

```html
HTML 标记标签通常被成为 HTML 标签 （HTML tag）
HTML 标签是有尖括号包围的关键词，比如<html>
HTML 标签都是成对出现的，比如<p>和</p>
标签对中的第一个标签是开始标签，第二个标签是结束标签。
```

**常用的标签**

- html基本骨架标签

  ```html
  <!DOCTYPE>
  <html>
  	<head>
          <title>文档的标题</title>
      </head>
      <body>
          文档的内容……
      </body>
  </html>
  
  <!DOCTYPE>声明不是	HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令，	没有结束标签，必须是 HTML 文档的第一行，位于<html>标签之前。
  
  <html>是文档的根元素，<html>与</html>标签限定了文档的开始点和结束点，在它们之间是文档的头部和	主体。文档的头部由<head>标签定义，主体由<body>标签定义，所有html文档都有这个基本骨架。
  ```

- h系列

  ```html
  <h1>一级标题</h1>
  <h2>二级标题</h2>
  	 ………
  <h6>六级标题</h6>
  ```

  h标签没有嵌套关系，是一个容器集标签，理论上里面可以放文本级标签。

- p标签

  英语	paragraph 	段落”缩写，给文本添加段落语义。p标签是一个文本级标签，里面只能放文字、图片、表单元素。

## HTML分类

​		HTML是一种标记语言，所以存在大量用来给文本定义语义的标签，这些标签就是HTML语言的血肉。HTML标签**根据形式的不同**，可分为对儿标签和自闭标签。

- 对儿标签

  ```html
  1.<html></html>
  2.<title></title>
  3.<body></body>
  4.<h1></h1>
  5.<p></p>
  
  未完待续……
  ```

- 自闭标签

  ```html
  1.<img /> 给文本定义图像
  2.<br />给文本换行
  3.<input />
  
  未完待续……
  ```

**根据HTML标签容量**的特性，可分为容器级和文本级标签

- 容器级标签

  ```html
  1.<div></div>	division 定义文档中的分区或节，重要的布局标签
  2.<h></h>
  3.<ul></ul>		unorderlist 定义无序列表	
  4.<ol></ol>		orderlist 定义有序列表
  5.<dl></dl>		definition 定义定义列表
  6.<li></li>		list 定义列表项目
  7.<dt></dt>		definition title 定义标题
  8.<dd></dd>		definition description 定义表述词儿
  ```

- 文本级标签

  ```html
  1.<span></span>	组合行内元素，以便通过样式来格式化它们
  2.<p></p>
  
  文本标签里面只能放文字、图片、表单元素，不能放其他任何标签
  ```



# HTML基本骨架详解

## 文档声明头

​		不管是HTML4.01还是HTML5，任何html文档开头都是<!DOCTYPE……>开头，这一行就叫文档声明头，DocType Declaration(DTD)。

​		此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。

### HTML4.01

HTML4.01有两种大规范，每种大规范里面又各有3中小规范。所以一共6中规范：![](assets/01doctype.jpg)

- HTML4.01-**Strict**

  > strict表示“严格的”，这种模式里面的要求更为严格。HTML原本表示样式的标签都不能用，比如：<u></u>给文本加下划线，但是和HTML的本质冲突(HTML只能负责语义)，不能负责样式。所以，在strict中不能使用类似标签

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
  ```

- HTML4.01-**Transitional**

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
  "http://www.w3.org/TR/html4/loose.dtd">
  ```

- HTML4.01-**Frameset**

  ```
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
  "http://www.w3.org/TR/html4/frameset.dtd">
  ```

### HTML5

HTML5极大地简化了DTD，文档声明头变为：

```html
<!DOCTYPE html>
```

综上所述，**HTML总共有7中DTD规范**。

## 字符集

```html
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
```

字符集用meta标签定义，**meta**表示“元”。“元”配置，表示基本的配置项目。**chartset**就是charactor set	“字符集”的意思。

中文能使用的字符集有两种：

- 第一种：UTF-8

  > UTF-8是国际通用字库，里面涵盖了所有地球上所有人类的语言文字，比如阿拉伯文、汉语、英语、法语……
  >
  > UTF-8 虽然有各种国家的语言，但是UTF-8里面存储一个汉字要3个字节，保存尺寸大，文件臃肿。

  ```html
  <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
  ```

- 第二种：gb2312/gbk

  > gb2312 是国标，是中国的字库，里面仅涵盖了汉字和一些常用外文，比如日文片假名，和常见的符号，
  >
  > gb2312存储一个汉字只需要2个字节，文件尺寸相对较小小，文件小巧。

  ```html
  <meta http-equiv="Content-Type" content="text/html;charset=gb2312">
  ```

**注意：同一个字在两种不同的字符集里面编码也不一样。用meta标签声明当前html文档的字库时，一定要和保存的类型一样，否则会乱码！！！！**

## 关键字和页面描述

​		meta除了可以设置字符集，还可以设置关键字和页面描述。只要设置的Description页面，那么搜索引擎的结果，就能够显示这些语句，这个技术叫	SEO，search engine optimization，搜索引擎优化。

- 关键字的设置（以网易为例）

  ```html
  <meta name="Keywords" content="网易,游戏,邮箱,体育,新闻,娱乐,女性,亚运" />
  
  这些关键词，就是告诉搜索引擎，这个网页的作用的，能够提高搜索命中率。
  ```

- 页面描述的设置（以聚美优品为例）

  ```html
  <meta name="Description" content="聚美优品是国内知名正品女性团购网站,也是领先的品牌化妆品团购和护肤品团购网,聚美优品团购化妆品每天有超值的化妆品和护肤品团购信息,详情登陆聚美优品官网:jumei..." />
  
  这些网页描述，更加全面告诉搜索引擎，这个网页的内容和作用，能够提高搜索命中率。
  ```




# 如何给网页添加图片和超链接

### 如何给网页插入图片

> 图片有很多格式，但是并不是所有格式的图片都能插入到网页中去。只有jpg（jpeg）、png、gif、bmp等格式能插入网页，而psd、ai格式的图片却不能插入。

​		HTML页面不是直接插入图片，而是插入图片的引用地址，所以要把图片上传到服务器上。我们使用<img/>标签插入图片。其基本语法如下：

```html
<img src="imgURL.jpg" alt="图片路径错误时替代文本" />

img是image		“图片”的简写。
src是source		“资源”的简写，是img标签的属性
alt是alternate	“替代”的简写，是img标签的属性，当图片无法显示的时候，出现的替代文字。

```

> <img/>标签是一个自闭合标签，因为图片就是一个图片，不需要给什么文字增加语义，所以只用单标签就行。

- imgURL的相对路径和绝对路径：

  ​		**绝对路径**：是文件的真正存储的路径，是从硬盘的根目录(盘符)开始，进行一级一级目录指向文件。通常以	http	或者	/	开头的链接都是绝对路径。

  ​		**相对路径**：即使这个网站项目，被用U盘拷给了别人，只要相对路径不变，图片一定能够正常显示。通常以	../	或者	./	开头的链接都是相对路径

### 如何给网页插入超链接

> 超链接：通过超链接形式，让在不同空间的文档都保存进一个文本文档。它更像是网页的灵魂

给网页插入超链接的基本语法：

```html
<a href="#" title="悬停文本" target="_blank" name="girl">文本内容</a>

a是anchor		“超链接--锚”的简写，一个页面往另一个页面扔出一个锚，文本级标签
href是hypertext reference	超文本地址的缩写。
title			悬停文本，当鼠标放在超链接上时，出现的提示文字
target			目标，意为是否在新窗口打开。
name			用来设置锚点，name属性值或者id属性值可设置为锚点。用href值，指向页面中的锚点，就是下面方式：
<a href="#demo">文本内容</a> 超链接
<a name="demo">文本内容</a> 锚点
	或者
<a id="demo">文本内容</a> 锚点
```

| 值        | 描述                                       |
| --------- | ------------------------------------------ |
| _blank    | 空白，意为在新窗口中打开被链接文档。       |
| _self     | 默认。在相同的框架、标签页中打开被链接文档 |
| _parent   | 在父框架集中打开被链接文档                 |
| _top      | 在整个窗口中打开被链接文档。               |
| framename | 在指定的框架中打开被链接文档。             |



# HTML的列表和表单

### 列表

列表总共有三种：无序列表、有序列表和定义列表

- 无序列表：列表项和列表项之间部分先后顺序

  ```html
  <ul>
      <li>列表项1</li>
      <li>列表项2</li>
  </ul>
  ```

  浏览器会默认添加 “ · ” 作为先导符号。

- 有序列表：列表项和列表项之间有先后顺序

  ```html
  <ol>
      <li>列表项</li>
      <li>列表项</li>
  </ol>
  
  ol 表示 ordered list	意为有序列表
  ```

  浏览器会默认添加 number 作为序列号

  > li是一个容器级标签，里面可以是任何标签

  **注意：li不能单独存在，必须包裹在ul、ol里面，反过来，ul、ol里面只能有li。**

- 定义列表

  ```html
  <dl>
      <dt>定义标题</dt>
      <dd>定义描述</dd>
  </dl>
  <dl>
      <dt>定义标题</dt>
      <dd>定义描述</dd>
      <dd>定义描述</dd>
  </dl>
  <dl>
      <dt>定义标题</dt>
      <dd>定义描述</dd>
      <dt>定义标题</dt>
      <dd>定义描述</dd>
  </dl>
  
  dl 表示definition list		意为定义列表
  dt 表示definition title		意为定义标题
  dd 表示definition description	意为表述词
  ```

  > dt、dd都是容器级标签，里面可以是任何标签

  **注意：dt、dd只能在dl里面，反过来，dl里面只能有dt、dd**

### 表单

表单作用是收集用户信息，就是让用户填写、选择信息

```html
<form>
	所有的表单内容，都要写在form标签里面
</form>

form	表单，中间可以添加文本框、密码框、单选按钮、复选框、下拉列表、按钮、文本域等内容
```

- 文本框

  ```html
  <input type="text" value="默认值" />
  ```

- 密码框

  ```html
  <input type="password" />
  ```

- 单选按钮

  ```html
  <input type="radio" name="name" checked /> 文本1
  <input type="radio" name="name" /> 文本2
  
  radio	收音机，这里意为单选按钮
  ```
  

**注意：radio必须要有相同的name属性值，radio才能互斥**

- 复选框

  ```html
  <input type="checkbox" name="name1" /> 文本1
  <input type="checkbox" name="name2" /> 文本2
  ```
  
- 下拉列表

  ```html
  <select>
      <option selected>文本1</option>
      <option>文本2</option>
      <option>文本3</option>
  </select>
  ```
  
- 文本域

  ```html
  <textarea cols="number" rows="number"></textarea>
  ```
  

**注意：number意为cols和rows的值是整数数值**

- 按钮

  ```html
  <input type="button" value="我是一个普通按钮" />
  <input type="submit" value="我是一个提交按钮" />
  <input type="reset" value="我是一个重置按钮" />
  ```