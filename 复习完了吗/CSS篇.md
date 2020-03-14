# CSS

1. css单位

   | 单位 | 描述                                                         |
   | :--: | :----------------------------------------------------------- |
   |  em  | 它是描述相对于应用在当前元素的字体尺寸，所以它也是相对长度单位。一般浏览器字体大小默认为16px，则2em == 32px； |
   |  px  | 像素                                                         |
   |  vw  | viewpoint width，视窗宽度，1vw=视窗宽度的1%                  |
   |  vh  | viewpoint height，视窗高度，1vh=视窗高度的1%                 |
   | rem  | 根元素（html）的 font-size                                   |

2. 盒模型

   盒模型由：元素的内容 + 内边距(padding) + 边框(border) + 外边距(margin)组成 

   > 页面渲染时，`dom` 元素所采用的 布局模型。可通过`box-sizing`进行设置。根据计算宽高的区域可分为（最常用的两种）

   - `content-box` (`W3C` 标准盒模型) 宽度为内容
   - `border-box` (`IE` 盒模型)   宽度为内容+padding+border （即除了margin）

3. 垂直居中方法

   flex布局

   ```css
   div.parent {
       display: flex;
       justify-content: center;
       align-items: center;
   }
   ```

   或者用定位

   ```css
   div.parent {
       position: relative; 
   }
   div.child {
       position: absolute; 
       top: 50%;
       left: 50%;
       transform: translate(-50%, -50%);  
   }
   ```

   **img垂直居中**

   ```css
   .tablebox{ /*图片的容器的父级*/
       width: 300px;
       height: 250px;
       background: #fff;
       display: table}
   
   #imgbox{ /*图片的容器*/
       display: table-cell;
       vertical-align: middle;
   }
   
   #imgbox img{width: 100px} /*img*/
   ```

4. 三栏布局

   实现三栏布局：两栏定宽，第三个自适应：

   子项使用flex-grow：1，占满剩余空间

5. 选择器权重计算方式

   ```css
   !important > 行内样式style > ID > class/伪类/属性 > 标签 
   ```

6. 清除浮动的方法

   - 父级定义 `overflow:hidden ` （简单，但超出隐藏，不能和position配合使用）
   - 父级固定高度  （简单，但是高度被固定了）
   - after伪元素+zoom （ 需要两句代码结合使用才能让主流浏览器支持 ）用zoom缩放伪元素实现占位

7. flex

8. 什么是BFC、可以解决哪些问题

   **块级格式化上下文(block formatting context)** 是页面盒模型布局中的一种 CSS 渲染模式，相当于一个独立的容器，里面的元素和外部的元素相互不影响。 

   - 创建规则：
     - 根元素
     - 浮动元素（`float`不取值为`none`）
     - 绝对定位元素（`position`取值为`absolute`或`fixed`）
     - `display`取值为`inline-block`、`table-cell`、`table-caption`、`flex`、`inline-flex`之一的元素
     - `overflow`不取值为`visible`的元素
   - 作用：
     - 清除浮动
     - 覆盖嵌套盒子，给父级加overflow:hidden)

9. position属性

   - `absolute`：生成绝对定位的元素，相对于 `static` 定位（即默认定位）以外的第一个父元素进行定位
   - `fixed`：生成绝对定位的元素，相对于浏览器窗口进行定位
   - `relative`：生成相对定位的元素，相对于其本身正常位置进行定位，它原本所占的空间仍保留

10. 如何实现一个自适应的正方形

  - ```css
    .placeholder {
      width: 100%;
      height: 100vw; /*是vw不是vh*/
    }
    ```

  - ```css
    .placeholder {
      width: 100%;
      height:0px;
      padding-bottom: 100%; /*用padding撑开*/
    }
    ```

11. 如何用css实现一个三角形

    利用border，把内容宽高设为0，然后其他三边设为透明色，只留下一边有颜色

12. 不定宽高居中

    ```css
    .container {
      position: relative;
    }
    .inner {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    ```

13. 单行省略号

    ```css
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
    ```

14. @import和link

    > 1.从属关系区别 @import是 CSS 提供的语法规则，只有导入样式表的作用；link是HTML提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。 
    >
    > 2.加载顺序区别 加载页面时，link标签引入的 CSS 被同时加载；@import引入的 CSS 将在页面加载完毕后被加载。
    >
    > 3.兼容性区别 @import是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link标签作为 HTML 元素，不存在兼容性问题。 
    >
    > 4.DOM可控性区别 可以通过 JS 操作 DOM ，插入link标签来改变样式；由于 DOM 方法是基于文档的，无法使用@import的方式插入样式。
    >
    > 5.权重区别 link引入的样式权重大于@import引入的样式。 
    
15. 选择器的解析是从右到左的，建立的树节点会少很多，快速找到公共样式，从右往左进行解析会比从左往右解析要少很多次的匹配，这样带来的效率提升是显而易见的