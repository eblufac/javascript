## BFC及其背后的 float absolute inline-block

#### BFC(Block formatting context)
```js
   BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。
```
#### BFC布局规则：
  - 内部的Box会在垂直方向，一个接一个地放置
  - 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。inline float)(浮动流)
  - BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

  - Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
    - [解决 margin 重叠](https://liubin915249126.github.io/BFC/bfc.html)
  - BFC的区域不会与float box重叠(absolute 与float会重叠)
    [两栏布局](https://liubin915249126.github.io/BFC/bfc.html)
  - 计算BFC的高度时，浮动元素也参与计算
    - 解决父元素高度塌陷 [float](https://liubin915249126.github.io/BFC/float.html)

#### 3.怎样触发BFC
- 根元素
- float属性不为none
- position为absolute或fixed
- display为inline-block, table-cell, table-caption, flex, inline-flex
- overflow不为visible

#### float
- 最初的目的:
  - 是为了实现 文字环绕效果。
- 实现方式:
  - 破坏行框盒子从而导致父元素高度塌陷
- 表现形式:
  - 宽度收缩至最小，和absolute,inline-block表现一致
- 现在的应用:
  - 根据BFC的规则浮动的元素不会重叠,从而形成浮动流，超过父元素宽度就会折行。
    - [栅格布局](https://liubin915249126.github.io/BFC/bfc.html)：float+百分比  
- 清除浮动带来的影响:父元素高度塌陷
- ![line](./line.png)
- [float](https://liubin915249126.github.io/BFC/float.html)

#### absolute,fixed
- 脱离文档流使父元素高度塌陷，不可避免
- 相对于第一个非static定位的父元素，查找链
- transform 截断向上查找链
- 应用:
  - 不定宽高元素垂直水平居中
- [absolute](https://liubin915249126.github.io/BFC/absolute.html)  

#### inline-block

- line-height 是行内元素占据的高度
- 图片底部有空白
  - 默认基线对齐
  - line-height<height
  - font-size==0

一个inline-block元素，
如果里面有inline内联元素，或者overflow是visible，其基线就是元素里面最后一行内联元素的基线
否则该元素的基线就是其margin底边缘。
- ![baseLine](./baseLine.jpg)

- [inline-block](https://liubin915249126.github.io/BFC/inline-block.html)