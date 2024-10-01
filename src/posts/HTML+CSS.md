---
title: HTML+CSS
date: 2023-12-04
tags: 前端
cover: https://www.studicore.hu/wp-content/uploads/2019/03/html_css.jpg
category:
  - 前端
---

## HTML

基本结构：

```html
<html>
    <head>
        <meta charset=“UTF-8”>
        <title></title>
    </head>
    <body>
        
    </body>
</html>
```

### 排版

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>排版</title>
</head>
<body>
    <h1>标题1</h1>
    <h2>标题2</h2>
    <h3>标题3</h3>
    <h4>标题4</h4>
    <h5>标题5</h5>
    <p>我是一个段落</p>
    <div></div>
</body>
</html>
```

+ \<div>标签没有实际的用处，CSS中用的多
+ h1~h6标签不能相互嵌套
+ \<p>标签中不能出现\<h1>~\<h6>标签、\<div>、\<p>

​    

### 语义化标签

+ 概念:
  用特定的标签，去表达特定的含义。

+ 原则:
  标签的默认效果不重要 (后期可以通过 CSS 随便控制效果) ，语义最重要!

+ 举例: 对于 h1 标签，效果是文字很大 (不重要)，语义是网页主要内容 (很重要)

+ 优势:

  + 代码结构清晰可读性强

  + 有利于 SEO (搜索引擎优化)
  + 方便设备解析 (如屏幕阅读器、盲人阅读器等)



### 块级元素与行内元素

 <strong>块级元素</strong>：独占一行

+ \<marquee>

+ \<h1>

+ \<p>

+ \<div>

<strong>行内元素</strong>：不占一行

+ \<input>

<mark>规则</mark>：

1. 块级元素 中能写 行内素和 块级元素 (简单记: 块级素中几乎什么都能写)

2. 行内元素 中能写 行内元素，但不能写 块级元素

3. 一些特殊的规则:

  + h1~h6 不能互相嵌套
  + p 中不要写块级元素

  我们以后还会学到一些特殊的规则，但不会很多。



### 文本标签

1. 用于包裹:词汇、短语等
2. 通常写在排版标签里面
3. 排版标签更宏观 (大段的文字) ，文本标签更微观 (词汇、短语)
4. 文本标签通常都是行内元素

常用的：

| 标签名 | 标签语义                         |
| ------ | -------------------------------- |
| em     | 要着重阅读的内容                 |
| strong | 十分重要的语气                   |
| span   | 没有语义，用于包裹短语的通用容器 |

### 图片

| 标签名 | 标签语义 | 标签属性                                                     | 单/双标签 |
| ------ | -------- | ------------------------------------------------------------ | --------- |
| img    | 图片     | `src`:图片路径 `alt`:图片描述  `width`:图片宽度，单位是像素 `height`:图片高度(px) | 是        |

1. 像素 ( px )是一种单位，学到 CSS 时，我们会详细讲解
2. 尽量不同时修改图片的宽和高，可能会造成比例失调。
3. 暂且认为 img 是行内元素(学到 CSS 时，会认识一个新的元素分类，目前咱们只知道: 块、行内)。
4. alt 属性的作用:
  + 搜索引擎通过 alt 属性，得知图片的内容。-- 最主要的作用
  + 当图片无法展示时候，有些浏览器会呈现 alt 属性的值
  + 盲人阅读器会朗读 alt 属性的值



### 常见的图片格式

1. `jpg`格式：

   > <strong>概述</strong>:扩展名为`jpg` 或`jpeg` ，是一种有损的压缩格式(把肉眼不容易观察出来的细节丢弃了)。
   >
   > 主要特点:支持的颜色丰富、占用空间较小、不支持透明背景、不支持动态图
   >
   > 使用场景:对图片细节没有极高要求的场景，例如: 网站的产品宣传图等。-- 该格式网页中很常见。

2. `png`格式：

   > <strong>概述</strong>:扩展名为.png，是一种无损的压缩格式，能够更高质量的保存图片
   >
   > 主要特点:支持的颜色丰富、占用空间略大、支持透明背景、不支持动态图
   >
   > 使用场景:
   >
   > + 想让图片有透明背景
   > + 想更高质量的呈现图片，例如:公司logo图、重要配图等

3. `bmp`格式：

   > <strong>概述</strong>:扩展名为 bmp ，不进行压缩的一种格式，在最大程度上保留图片更多的细节。
   >
   > 主要特点:支持的颜色丰富、保留的细节更多、占用空间极大、不支持透明背景、不支持动态图
   >
   > 使用场景: 对图片细节要求极高的场景，例如:一些大型游戏中的图片。(网页中很少使用)

4. `gif`格式：

   > <strong>概述</strong>: 扩展名为 .gif ，仅支持256种颜色，色彩呈现不是很完整
   >
   > 主要特点:支持的颜色较少、支持简单透明背景、支持动态图
   >
   > 使用场景:网页中的动态图片

5. `webp`格式：

   > 概述: 扩展名为 .webp ，谷歌推出的一种格式，专门用来在网页中呈现图片。
   >
   > 主要特点: 具备上述几种格式的优点，但兼容性不太好，一旦使用务必要解决兼容性问题
   >
   > 使用场景: 网页中的各种图片。

6. `base64`格式：

   > 1. 本质:一串特殊的文本，要通过浏览器打开，传统看图应用通常无法打开
   > 2. 原理: 把图片进行 base64 编码，形成一串文本。
   > 3. 如何生成:靠一些工具或网站。
   > 4. 如何使用: 直接作为 img 标签的 src 属性的值即可，并且不受文件位置的影响
   > 5. 使用场景:一些较小的图片，或者需要和网页一起加载的图片。

### 超链接

| 标签名 | 标签语义 | 常用属性                                             |
| ------ | -------- | ---------------------------------------------------- |
| a      | 超链接   | `href`:要跳转的具体位置；`target`:跳转时如何打开界面 |

```html
<a href= "网址" target="_blank">超链接的文字</a>//跳转另一个界面页面
<a href= "网址" target="_self">超链接的文字</a>//跳转当前页面
```

> 注意：
>
> 1. 代码中的多个空格、多个回车，都会被浏览器解析成一个空格
> 2. a标签是行内元素，a元素可以包裹出他自身外的任何元素

### 跳转到锚点

1. 设置锚点

   ```html
   <!-- 方式一：a标签+name-->
   <a name = "test1"></a>
   <!-- 方式二：其他标签配合id属性-->
   <h1 id="test2">这是第一个位置</h1>
   ```

   > 注意点：
   >
   > 1. 具有 href 属性的 a 标签是超链接，具有 name 属性的 a 标签是锚点
   > 2. name 和 id 都是区分大小写的，且 id 最好别是数字开头

2. 跳转锚点

   ```html
   <!--跳转到Test1锚点-->
   <a href="#test1">去test1锚点</a>
   
   <!--跳转到页面顶部-->
   <a href="#"></a>
   
   <!--跳转到其他页面的锚点-->
   <a href = "demo.html#test1"></a>
   
   <!--刷新页面-->
   <a href=">刷新页面</a>
   ```

   

### 列表

#### 有序列表

```html
<ol>
        <li>列1</li>
        <li>列2</li>
        <li>列3</li>
</ol>
```



#### 无序列表

```html
    <ul>
        <li>列1</li>
        <li>列2</li>
        <li>列3</li>
    </ul>
```



#### 自定义列表

```html
    <dl>
        <dt>Title_1</dt>
        <dd>content_1</dd>
    </dl>
```

#### 列表嵌套

```html
<ul>
        <li>中国</li>
        <li>
            <span>
                <ul>
                    <li>江苏省</li>
                    <li>
                        <span>
                            <li>
                                邳州市
                            </li>
                        </span>
                    </li>
                </ul>
            </span>
        </li>
    </ul>
```

### 表格

包括：表格标题、表格头部、表格主体、表格脚注

```html
    <table border="1">
        <!-- 表格标题 -->
        <caption>标题</caption>
        <!-- 头部 -->
        <thead>头部</thead>
        <tr>
            <th>属性1</th>
            <th>属性2</th>
            <th>属性3</th>
            <th>属性4</th>
        </tr>
        <!-- 主体 -->
        <tbody>主体</tbody>
        <tr>
            <td>内容1</td>
            <td>内容2</td>
            <td>内容3</td>
            <td>内容4</td>
        </tr>
        <!-- 脚注 -->
        <tfoot>脚注</tfoot>
    </table>
```

![](https://cdn.jsdelivr.net/gh/czlifetime/img/HTML_%E8%A1%A8%E6%A0%BC.png)

#### 常用属性

| 标签名 | 标签语义   | 常用属性                                                     |
| ------ | ---------- | ------------------------------------------------------------ |
| table  | 表格       | `width`:设置表格宽度<br>`height`:设置表格最小宽度，表格最终高度可能比设置的值大<br>`boder`:设置表格边框高度`cellspacing`:设置单元格之间的间距 |
| thead  | 表格头部   | `height`:设置表格头部高度<br>`align`:设置单元格的水平对齐方式`left`:左对齐、`center`:中间对齐、`right`:右对齐<br>`valign`：设置单元格的垂直对齐方式：`top`:顶部对齐、`middle`:中间对齐、`bottom`:底部对齐 |
| tbody  | 表格主体   | 属性与Thread相同                                             |
| tr     | 行         | 属性与Thread相同                                             |
| tfoot  | 表格脚注   | 属性与Thread相同                                             |
| td     | 普通单元格 | `width`:设置单元格的宽度，同列所有单元格全都受影响<br>`heigth`:设置单元格的高度，同行所有单元格全懂受影响<br>`align`:设置单元格的水平对齐方式<br>`rowspan`:设置要跨的行数<br>`colspan`:设置要跨的列数 |
| th     | 表头单元格 | 属性与`td`相同                                               |

![](https://cdn.jsdelivr.net/gh/czlifetime/img/HTML_%E8%A1%A8%E6%A0%BC%E5%B8%B8%E7%94%A8%E5%B1%9E%E6%80%A7.png)

### 表单

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form action="https://baidu.com/s">
        <input type="text" name="wd">
        <button>去百度搜索</button>
    </form>
</body>
</html>
```

| 标签名 | 标签语义 | 常用属性                                                     |
| ------ | -------- | ------------------------------------------------------------ |
| form   | 表单     | `action`:用于提交表单的提交地址<br>`target`:用于控制表单提交后，如何打开页面：`_self`:在本窗口打开、`_blank`:在新窗口打开 |
| input  | 输入框   | `type`:设置输入框的类型，`text`表文本<br>`name`:用于提交数据的名字 |
| buttom | 按钮     | 暂无                                                         |

#### 常用表单控价

1. 文本

   ```html
   <input type = "text">
   ```

   > name：数据的mingcheng
   >
   > value：输入框的默认输入值
   >
   > maxlength：输入框的最大长度

2. 密码

   ```html
   <input type="password">
   ```

   > name:数据的名称
   >
   > value：输入框的默认值
   >
   > maxlength:输入框输入的最大长度

3. 单选框

   ```html
   <input type="radio" name = "sex" value = "male">男
   <input type="radio" name = "sex" value = "famale">女
   ```

   >  name:数据的名称<font color="red">注意：想要单选多个`radio`</font>的`name`属性值要保持一致
   >
   > value:提交的数据值
   >
   > checked：让该单选按钮默认选中

4. 复选框

   ```html
   <input type="checkbox" name = "bobby" value = "smoke">抽烟
   <input type="checkbox" name = "bobby" value = "drink">喝酒
   ```

   > name:数据的名称
   >
   > value：提交的数据值
   >
   > checked：让该复选框默认选中

5. 隐藏域

   ```html
   <input type = "hidden" name = "tag" value="100">
   ```

   > 用户不可见的一个输入区域，作用是：提交表单的时候，携带一些固定的数据
   >
   > `name`:指定数据的名称
   >
   > `value`:指定真正提交的数据

6. 提交按钮

   ```html
   <input type = "submit value = “点我提交表单">
   <button>点我提交表单</button>
   ```

   > 1. `button`标签type属性的默认值是`submit`
   > 2. `button`不要指定`name`属性
   > 3. `input`标签编写的按钮，使用`value`属性指定按钮文字

7. 重置按钮

   ```html
   <input type = "reset" value = "点我重置">
   <buttom type = "reset">点我重置</buttom>
   ```

   > 1. `buttom`不指定`name`属性
   > 2. `input`标签编写的按钮，使用`value`属性指定按钮文字

8. 普通按钮

   ```html
   <input type = "button" value="普通按钮">
   <button type="button">普通按钮</button>
   ```

   > 普通按钮的`type`值为`button`，默认为`submit`，记得更改

9. 文本域

   ```html
   <textarea name = "msg" rows = "2" cols = "3">这里是文本域</textarea>
   ```

   > 1. `rows`:行数
   > 2. `cols`:列数

10. 下拉框

    ```html
    <select name="from">
        <option value = "黑">黑龙江</option>
        <option value = "苏">江苏</option>
    </select>
    ```

    > 1. `name`：指定数据的名称
    > 2. `option`：设置`value`属性，如果没有`value`属性，提交的数据是`option`之间的文字；如果设置了`value`属性，提交的数据是`value`的值
    > 3. `option`标签设置了`selected`属性，表示默认选中

## 框架标签

| 标签名 | 功能和语义 | 属性                                                         |
| ------ | ---------- | ------------------------------------------------------------ |
| iframe | 框架       | `name`:框架的名字，可以与`target`属性配合<br>`width`:框架的高度<br>`height`：框架的高度<br>`frameborder`:是否显示边框，值为0或1 |

> 用途：
>
> 1. 在网页中嵌入广告
> 2. 与超链接或表单的`target`配合，展示不同的内容





## CSS

### CSS简介

+ CSS(Cascading Style Sheets)：层叠样式表
+ CSS也是一种标记语言，用于给`HTML`结构样式，例如：文字大小、颜色、元素宽高等等

### CSS编写位置

####  行内样式

+ 写在标签的`style`属性中

+ 语法：

  ```html
  <h1 style = "color:red;font-size:60px;">I'm Lifetime Max</h1>
  ```

  > 行内样式表，只能控制当前标签的样式，对其他样式无效

#### 内部样式

+ 写在`HTML`页面内部，将所有的`CSS`代码提取出来，单独放在`<style>`标签中

+ 语法：

  ```html
  <style>
      h1{
          color:red;
          font-size: 40px;
      }
  </style>
  ```

+ > + `<style>`：标签理论上可以放在`HTML`的任何位置，但一般放在`<head>`标签中
  > + 样式可以复用、代码结构清晰

+ 问题：

  > 1. 并没有实现：结构与样式完全分离
  > 2. 多个`HTML`页面无法复用样式

#### 外部样式

+ 写在单独的`.css`文件中，随后在`HTML`文件中引用。

+ 语法：

  1. 新建一个拓展名为`.css`的样式文件，把所有的`CSS`代码放在此文件中

     ```html
     h1{
     	color:red;
     	font-size: 40px;
     }
     ```

  2. 在`HTML`文件中引入`.css`文件

     ```html
     <link rel = "stylesheet" href = "./xxx.css">
     ```

+ 注意：

  > 1. `<link>`标签要写在`<head>`标签中
  > 2. `<link>`标签属性说明：
  >    + `href`:引入的文件路径
  >    + `rel`：说明引入的文档与当前文档之间的关系
  > 3. 外部样式的优势：复用、结构清晰、可触发浏览器的缓存机制，提高访问速度，实现结构与样式的完全分离

### 样式表的优先级

+ 优先级规则：<strong>行内样式</strong>><strong>内部样式</strong>=<strong>外部样式</strong>

  > 1. 内部样式、外部样式，这二者的优先级相同，且:后面的会覆盖 前面的(简记:“后来者居上”)
  > 2. 同一个样式表中，优先级也和编写顺序有关，且:后面的 会覆盖 前面的 (简记:“后来者居上”)

  | 分类     | 优点                                                         | 缺点                                                      | 使用频率 | 作用范围 |
  | -------- | ------------------------------------------------------------ | --------------------------------------------------------- | -------- | -------- |
  | 行内样式 | 优先级最高                                                   | 1. 结构与样式未分离<br>2. 代码结构混乱<br>3. 样式不能复用 | 低       | 当前标签 |
  | 内部样式 | 1. 样式可复用<br>2. 代码结构清晰                             | 1. 结构与样式未彻底分离<br>2. 样式不能多页面复用          | 一般     | 当前页面 |
  | 外部样式 | 1. 样式可复用<br/>2. 代码结构清晰<br>3. 可触发浏览器的缓存机制<br>4. 结构与样式彻底分离 | 需要引入才能使用                                          | 最高     | 多个页面 |

  

### CSS语法规范

CSS语法由两部分构成：

+ 选择器
+ 声明块

### 代码风格

+ 展开风格
+ 紧凑风格

### CSS基本选择器

基本选择器包括：

1. 统配选择器
2. 元素选择器
3. 类选择器
4. `id`选择器
5. 交集选择器

#### 统配选择器

+ 作用：可以选中所有的`HTML`元素

+ 语法：

  ```css
  * {
  	属性名: 属性值
  }
  ```

  例如：

  ```css
  * {
      color: red;
      font-size: 40px;
  }
  ```

  

#### 元素选择器

+ 为页面中某种元素统一设置标签

+ 语法：

  ```html
  与以上相类似
  ```

  例如：

  ```css
  h1 {
      color: orange;
      font-size: 10px;
  }
  p {
      color: red;
      font-size: 50px;
  }
  ```

  > 元素选择器无法实现差异化设置，例：以上的标签中，所有的`<p>`标签样式相同

#### 类选择器

+ 作用：根据元素的`class`值，选中某些元素

+ 语法：

  ```css
  .类名 {
      属性名: 属性值;
  }
  ```

  例如：

  ```css
  .speak {
      color: red;
  }
  /*为选中的所有class值为speak的元素*/
  .answer {
      color: black;
  }/*为选中的所有class值为answer的元素*/
  ```

  

#### `id`选择器

+ 根据元素的`id`属性值，来选中某个元素

+ 语法：

  ```css
  #id值 {
      属性名: 属性值;
  }
  ```

  例如：

  ```css
  /*选中id值为earth的那个元素*/
  #earth {
      color: red;
      font-size: 50px;
  }
  ```

+ `id`属性值：尽量由<strong>数字、字母、下划线、短杠</strong>组成，以字母开头、区分大小写、中间不空格

+ 一个元素只能拥有一个`id`属性，多个元素的`id`属性值不能相同

+ 一个元素可以同时拥有`id`与`class`属性



### CSS复合选择器

#### 交集选择器

+ 作用：选中同时符合多个条件的元素

+ 语法：

  选择器1 选择器2 选择器3 …n{}

  例如：

  ```css
  p.beatufy {
      color: blue;
  }
  .rich.beauty{
      color: green;
  }
  ```

+ 注意：

  1. 有标签名，标签名必须写在前面。

  2. id 选择器、理论上可以作为交集的条件，但实际应用中几乎不用--因为没有意义
  3. 交集选择器中不可能出现两个元素选择器，因为一个元素，不可能即是p 元素又是 span 元素
  4. 用的最多的交集选择器是: 元素选择器配合类名选择器，例如: p.beauty 。



#### 并集选择器

+ 作用：选中多个选择器对应的元素，又称:分组选择器

+ 语法：

  > 与以上相似
  >
  > 多个选择器通过“,”连接，“,”的含义就是或

+ 例子：

  ```css
  #peiqi,
  .rich,
  .beauty {
      font-size: 10px;
      width: 200px;
  }
  ```

+ 1. 并集选择器，我们一般竖着写.
  2. 任何形式的选择器，都可以作为并集选择器的一部分
  3. 并集选择器，通常用于集体声明，可以缩小样式表体积

#### 后代选择器

+ 作用：选中指定元素中，符合要求的后代元素

+ 语法：选择器1 选择器2 选择器3 …选择器n{} (先写祖先，后写后代)

  > 以上语法中，选择器之间用空格隔开

+ 例如：

  ```css
  /*选中ul中的所有li*/
  ul li{
      color: red;
  }
  /*选中ul中所有li中的a*/
  ul li a {
      color: red;
  }
  /*选中类名为subject元素中的所有类名为font-end的li*/
  .subject li.font-end {
      color: blue;
  }
  ```

+ > 1. 后代选择器，最终选择的是后代，不选中祖先。
  > 2. 儿子、孙子、重孙子，都算是后代。
  > 3. 结构一定要符合之前讲的 HTML 嵌套要求，例如:不能p 中写 h1 ~ h6。

#### 子代选择器

+ 作用：选定指定元素中，符合要求的子元素（儿子元素）

  > 子选择器又称：子选择器、子选择器

+ 语法：选择器1> 选择器2>选择器3>…选择器n{}

  > 选择器之间，用>隔开

+ 例如：

  ```css
  /* div中的子代a的元素 */
  div>a{
      color: red;
  }
  /*类名为person的元素中子代a元素*/
  .person>a{
      color: red;
  }
  ```

+ 子代选择器，最终选择的是子代，不是父级

+ 子、孙…统称为后代

#### 兄弟选择器

+ 相邻兄弟选择器

  + 作用：符合条件的相邻兄弟元素

  + 语法：

    ```css
    选择器1+选择器2{}
    ```

    ```css
    div+p{
        color:red;
    }
    ```

+ 通用兄弟选择器

  + 作用：选中指定元素后，符合条件的所有兄弟元素

  + 语法：

    ```css
    选择器1~选择器2{
        
    }
    ```

    ```css
    div~p{
        color:red;
    }
    ```

+ > 两种兄弟选择器，选中的是下面的兄弟元素

#### 属性选择器

+ 作用：选中属性值具有一定要求的元素
+ 语法：
  1. `[属性名]`：选中具有某个属性的元素
  2. `[属性名="值"]`：选中包含某个属性，且属性值<strong>等于</strong>指定值的元素
  3. `[属性名^="值"]`：选中包含某个属性，且属性值以指定的值<strong>开头</strong>的元素
  4. `[属性名$ ="值"]`：包含某个属性，且属性值以指定的值<strong>结尾</strong>的元素
  5. `[属性名*="值"]`：包含某个属性，属性<strong>包含</strong>指定值的元素

#### 伪类选择器

+ 作用：选中特殊状态的类

### CSS选择器优先级

+ <mark>行内样式>id选择器>类选择器>元素选择器>统配选择器</mark>

+ 样式的权重：(a,b,c)

>a: <strong>ID</strong> 选择器的个数
>
>b:<strong>类、伪类、属性</strong> 选择器的个数
>
>c:<strong>元素、伪元素</strong> 选择器的个数

+ 例如：

![](https://cdn.jsdelivr.net/gh/czlifetime/img/CSS_%E9%80%89%E6%8B%A9%E5%99%A8%E6%9D%83%E9%87%8D.png)

+ 比较规则：按照<strong>从左到右</strong>的顺序，依次比较大小

+ 特殊规则：

  > <strong>行内样式</strong>权重大于所有选择器
  >
  > `!important`的权重，大于所有的样式



### CSS三大特性

1. <strong>层叠性</strong>

   如果发生了样式冲突，就按照(选择器优先级)进行样式的层叠

   > 冲突：元素的同一个属性，被设置了不同的值

2. <strong>继承性</strong>

   元素会自动拥有其父元素、或其祖先元素上所设置的某些样式

   + 规则：优先继承离得近的

   + 常见的可继承属性：

     > `text-??`、`font-??`、`line-??`、`color`…

3. <strong>优先级</strong>

   <mark>`!important`>行内样式>id选择器>类选择器>元素选择器>统配选择器</mark>

### CSS颜色 `HEX`或`HEXA`

`HEX`的原理同与`RGB`一样，依然是通过: 红、绿、蓝色 进行组合，只不过要用 6个数字，分成3组来表达
格式为: #rrggbb

> 每一个数字的取值范围是0~f，最大值是ff，最小值是00

### CSS常用的字体属性

#### 字体大小

+ 属性名：`font-size`

+ ```css
  div {
      font-size:20px;
  }
  ```

#### 字体族

+ 属性名：`font-family`

+ ```css
  div {
      font-family: "Microsoft Yahei"
  }
  ```

#### 字体风格

+ 属性名：`font-style`

+ 常用值：

  + `normal`: 正常
  + `italic`:斜体
  + `oblique`:倾斜

  > 使用斜体，推荐使用`italic`

#### 字体的粗细

+ 属性名：`font-size`

+ 常用值：

  + 关键词：

    1. `lighter`:细
    2. `normal`:正常
    3. `bold`:粗
    4. `bolder`:很粗

  + 数值：

    > 1. `100~1000`且无单位，数值越大，字体越粗
    > 2. `100~300`等于`lighter`,`400~500`等于`normal`,`600`及以上等同于`bold`

+ 语法：

  ```css
  div {
      font-weight: bold;
  }
  div {
      font-weight: 600;
  }
  ```

  

#### 字体复合

+ 属性名：`font`,可以把上述字体合并成一个属性
+ 规则
  1. 字体大小、字体族必须都写上
  2. 字体族必须是最后一位、字体大小必须是倒数第二位
  3. 各个属性之间，用空格隔开

#### 字体颜色

+ 属性名：`color`
+ 可选值：
  1. 颜色名
  2. `rgb`或`rgba`
  3. `HEX`或`HEXA`(十六进制)
  4. `HSL`或`HSLA`

#### 文本间距

+ 字母间距：`letter-spacing`
+ 单词间距：`word-spacing`(通过空格识别此)
+ 属性值为像素(px),正值间距增大，负值间距缩小

#### 文本修饰

+ 属性名：`text-decoration`

+ 可选值：

  1. `none`: 无修饰线(常用)
  2. `underline`: 下划线
  3. `overline`: 上划线
  4. `line-through`: 删除线

  可搭配如下值使用：

  1. `dotted`: 虚线
  2. `wavy`: 波浪线

+ ```css
  div {
      text-decoration: overline dotted green;
  }
  ```

#### 文本缩进

+ 属性名：`text-indent`

+ 属性名：`CSS`中的长度单位，`mm,cm,px`

+ ```css
  div {
      text-indent: 40px;
  }
  ```



#### 文本水平对齐

+ 属性名：`text-align`
+ 常用值：
  1. `left`: 左对齐(默认值)
  2. `right`: 右对齐
  3. `center`:居中对齐

#### 行高

+ 属性名：`line-height`

+ 可选值：

  1. `normal`: 由浏览器根据文字大小决定的一个默认值
  2. 像素(px)
  3. 数字：参考自身`font-size`的倍数
  4. 百分比：参考自身`font-size`的百分比

  > 由于字体设计原因，文字在一行中，并不是绝对垂直居中，若一行中都是文字，不会太影响观感。

+ ```css
  div {
      line-height: 90px;
  }
  ```



#### 垂直对齐

+ 属性名：`vertical-align`
+ 作用：用于指定同一行元素之间，或表格单元格内文字的垂直对齐方式
+ 常用值：
  1. `baseline` （默认值）:使元素的基线与父元素的基线对齐
  2. `top`：使元素的顶部与其梭子行的顶部对齐
  3. `middle`：使元素的中部与其父元素的基线加上父元素的字母x的一般对齐
  4. `bottom`:使元素的底部与其所在行的底部对齐



#### 列表属性

可作用于`ul`、`ol`、`li`元素

| CSS属性名           | 功能               | 属性值                                                       |
| ------------------- | ------------------ | ------------------------------------------------------------ |
| list-style-type     | 设置列表符号       | `none`:不显示前面的标识(常用)<br>`square`:实心方框<br>`disc`:圆形<br>`decimal`:数字<br>`lower-roman`:小写罗马字<br>`upper-roman`:大写罗马字<br>`lower-alpha`:小写字母<br>`upper-alphe`:大写字母<br> |
| list-style-position | 设置列表符号的位置 | `inside`:在`li`的里面<br>`outside`:在`li`的外面              |
| list-style-image    | 自定义列表符号     | `url`                                                        |
| list-style          | 符合属性           | 没有数量、顺序的要求                                         |



#### 表格属性

| 属性名        | 功能         | 属性值                                                       |
| ------------- | ------------ | ------------------------------------------------------------ |
| `boder-width` | 边框宽度     | CSS中可用的长度值                                            |
| `boder-color` | 边框颜色     | CSS中可用的颜色值                                            |
| `boder-style` | 边框风格     | `none`:默认值<br>`solid`:实线<br>`dashed`:虚线<br>`dotted`:点线<br>`double`:双实线 |
| `boder`       | 边框复合属性 | 没有数量、顺序的要求                                         |

##### 表格独有的属性

| CSS属性名        | 功能                 | 属性值                                                    |
| ---------------- | -------------------- | --------------------------------------------------------- |
| `table-layout`   | 设置列宽度           | `auto`:自动，列宽根据内容计算<br>`fixed`:固定列宽、平局分 |
| `boder-spacing`  | 单元格间距           | CSS中可用的长度值（边框不合并）                           |
| `boder-collapse` | 合并单元格边框       | `collapse`:合并<br>`separate`:不合并                      |
| `empty-cells`    | 隐藏没有内容的单元格 | `show`: 显示<br>`hide`: 隐藏<br>单元格不合并              |
| `caption-side`   | 设置表格标题位置     | `top`:上面（默认）<br>`bottom`:下                         |

### CSS背景属性

| CSS属性名             | 功能             | 属性值                                                       |
| --------------------- | ---------------- | ------------------------------------------------------------ |
| `background-color`    | 设置背景颜色     | 符合`CSS`中颜色规范的值<br>默认图片颜色是`transparent`       |
| `background-image`    | 设置背景图片     | `url(图片的地址)`                                            |
| `background-repect`   | 设置背景重复方式 | `repect`:重复，铺满整个元素，默认值。<br>`repect-x`：只在水平方向重复<br>`repect-y`：只在垂直方向重复<br>`no-repect`：不重复 |
| `background-position` | 设置背景图位置   | 通过关键字设置位置：<br>水平：`left`、`center`、`right`<br>垂直：`top`、`center`、`bottom`<br>如果只写一个值，另一个方向的值去`center`<br><br>通过长度指定坐标位置：<br>以元素左上角，为坐标原点，设置图片左上角的位置。两个值，分别是`x`坐标和`y`坐标。<br>只写一个值，会被当做`x`坐标，`y`坐标取`center` |
| `background`          | 符合属性         | 没有数量和顺序的要求                                         |



### 鼠标相关的属性

| CSS属性名 | 功能               | 属性值                                                       |
| --------- | ------------------ | ------------------------------------------------------------ |
| `cursor`  | 设置鼠标光标的样式 | `pointer`<br>`move`<br>`text`<br>`crosshair`<br>`wait`<br>`help`<br> |



### 盒子模型

##### CSS长度单位

1. `px`：像素
2. `em`：相对元素`font-size`的倍数
3. `rem`：相对更字体大小，HTML标签就是根
4. `%`：相对父元素计算。

##### 元素的显示模式

+ 块元素(block)

  > 又称块级元素
  >
  > 特点：
  >
  > 1. 在页面中独占一行，从上到下排列
  > 2. 默认元素：撑满父元素
  > 3. 默认高度：由内容撑开
  > 4. 可以通过CSS设置宽高

+ 行内元素(inline)

  > 又称：内联元素
  >
  > 特点：
  >
  > 1. 在页面中不独占一行，一行中不能容下行内元素，会在下一行继续从左到右排列
  > 2. 默认宽度：由内容撑开
  > 3. 默认高度：有内容撑开
  > 4. 无法从CSS设置宽高

+ 行内块元素(inline-block)

  > 又称：内联块元素
  >
  > 特点：
  >
  > 1. 在页面中不独占一行，一行中不能容下的行内元素，会在下一行继续从左到右排列
  > 2. 默认宽度：由内容撑开
  > 3. 默认高度：有内容撑开
  > 4. 可以通过CSS设置宽高

##### 总结各元素的显示模式

+ 块元素

  > 1. 主题结构标签:<html>、<body>
  > 2. 排版标签：<h1>~<h6>、<hr>、<p>、<pre>、<div>
  > 3. 列表标签：<ul>、<ol>、<li>、<dl>、<dt>、<dd>
  > 4. 表格相关标签：<table>、<tbody>、<thead>、<tfoot>、<tr>、<caption>
  > 5. \<form>与\<option>

+ 行内元素

  > 1. 文本标签：\<br>、\<em>、\<strong>、<sup>、\<del>、\<button>

+ 行内块元素

  > 1. 图片：\<img>
  > 2. 单元格：\<td>、\<th>
  > 3. 表单控件：\<input>、\<textarea>、\<select>、\<buttom>
  > 4. 框架标签：\<iframe>

##### 修改元素显示模式

通过`CSS`中的`display`属性可以修改元素的默认显示模式;

|       值        |          描述          |
| :-------------: | :--------------------: |
|     `none`      |       元素被隐藏       |
|     `block`     | 元素将作为块级元素显示 |
|    `incline`    |    作为内敛元素显示    |
| `incline-block` |    作为行内元素显示    |

##### 盒子模型的组成

`CSS`会把所有的`HTML`元素都看成一个盒子，所有的样式也是基于这个盒子的

1. <strong>margin(外边距)</strong>：盒子与外界的距离
2. <strong>border(边框)</strong>：盒子的边框
3. <strong>padding(内边距)</strong>：紧贴内容的不白区域
4. <strong>content(内容)</strong>：元素中的文本或后代元素都是他的内容

图示：

<img src="https://cdn.jsdelivr.net/gh/czlifetime/img/%E7%9B%92%E5%AD%90%E6%A8%A1%E5%9E%8B.png" style="zoom:50%;" />

盒子的大小=`content` + 左右`padding` + 左右`border`

##### 盒子内容区

| CSS属性名  | 功能     |
| ---------- | -------- |
| width      | 宽度     |
| max-width  | 最大宽度 |
| min-width  | 最小宽度 |
| height     | 高度     |
| max-height | 最大高度 |
| min-height | 最小高度 |

##### 盒子内边距

| CSS属性          | 功能     |
| ---------------- | -------- |
| `padding-top`    | 上       |
| `padding-right`  | 右       |
| `padding-bottom` | 下       |
| `padding-left`   | 左       |
| `padding`        | 复合属性 |

`padding`复合属性的使用规则

1. `padding:10px`四个方向内边距都是10px
2. `padding:10px 20px`上10px,左右20px
3. `padding:10px 20px 30px`（上、左右、下）
4. `padding:10px 20px 30px 40px`（上、右、下、左）



##### 盒子边框

| CSS属性                                                      | 功能                                   | 属性值                                          |
| ------------------------------------------------------------ | -------------------------------------- | ----------------------------------------------- |
| `border-style`                                               | 边框线风格<br>复合了四个方向的边框风格 | `solid`:实线<br>`dahed`:虚线<br>`double`:双实线 |
| `border-width`                                               | 边框线宽度<br>复合了四个方向的边框宽度 | 长度默认为3px                                   |
| `border-color`                                               | 边框颜色<br>复合了四个方向的边框颜色   | 默认为黑色                                      |
| `border`                                                     | 复合属性                               | 没有顺序和数量的要求                            |
| `border-left`<br>`border-left-style`<br>`border-left-width`<br>`border-left-color`<br><br>`border-right`<br/>`border-right-style`<br/>`border-right-width`<br/>`border-right-color`<br/><br/>`border-top`<br/>`border-top-style`<br/>`border-top-width`<br/>`border-top-color`<br/><br/>`border-bottom`<br/>`border-bottom-style`<br/>`border-bottom-width`<br/>`border-bottom-color`<br/> | 分别设置各个方向的边框                 | 同上                                            |

##### 盒子外边距

| CSS属性名       | 功能                    |
| --------------- | ----------------------- |
| `margin-left`   | 左外边距                |
| `margin-right`  | 右外边距                |
| `margin-top`    | 上外边距                |
| `margin-bottom` | 底外边距                |
| `margin`        | 复合属性，可以写1~4个值 |

##### 注意事项

> 1. 子元素的`margin`，是参考父元素的`content`计算的。
> 2. 上`margin`、左`margin`：影响自己的位置；下`margin`、右`margin`：影响后面兄弟元素的位置
> 3. 块级元素、行内元素，局可以完美的设置四个方向的`margin`;当行内元素，左右`margin`可以完美设置，上下`margin`设置无效
> 4. `margin` 的值也可以是 `auto`，如果给一个块级元素设置左右`margin` 都为 `auto`，该块级元素会在父元素中水平居中。
> 5. `margin`的值可以是负值。

##### `margin`塌陷问题

+ 什么是`margin`塌陷？

  第一个子元素的上`margin`会作用在父元素上，最后一个元素的下`margin`会作用在父元素上

+ 解决`margin`塌陷？

  + 方案一：给父元素设置不为0的padding
  + 方案二：给父元素设置宽度不为0 的border
  + 方案三：给父元素设置CSS样式`overflow:hidden`

##### `margin`合并问题

+ 什么是`margin`合并：

  上面兄弟元素的下外边框和下面兄弟元素的上外边框会合并，去一个最大的值，而不是相加

+ 解决：

  + 无需解决，布局的时候上下的兄弟元素，只给一个设置上下外边距就可以了

### 浮动

#### <strong>简介</strong>

在最初，浮动用来实现文字环绕图片效果的，现在浮动是主流的页面布局方式之一

#### 元素浮动后的特点

1. 脱离文档流。
2. 不管浮动前是什么元素，浮动后: 默认宽与高都是被内容撑开 (尽可小)，而且可以设置宽高
3. 不会独占一行，可以与其他元素共用一行。
4. 不会 margin 合并，也不会 margin 塌陷，能够完美的设置四个方向的 margin和 padding。
5. 不会似行内块一样被当做文本处理 (没有行内块的空白问题)
