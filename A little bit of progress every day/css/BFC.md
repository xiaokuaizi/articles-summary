### BFC (Block Formatting Context) 块格式化上下文


决定块盒子的布局及浮动相互影响范围的一个区域

#### BFC的创建方法

- 根元素或其它包含它的元素；
- 浮动 (元素的float不为none)；
- 绝对定位元素 (元素的position为absolute或fixed)；
- 行内块inline-blocks(元素的 display: inline-block)
- 表格单元格(元素的display: table-cell，HTML表格单元格默认属性)；
- overflow的值不为visible的元素；
- 弹性盒 flex boxes (元素的display: flex或inline-flex)；

#### 最常见的就是overflow:hidden、float:left/right、position:absolute


```一个元素不能同时存在于两个BFC中,BFC一个最重要的效果是：让处于BFC内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响```
```
<div id='div_1' class='BFC'>
	<div id='div_2'>
		<div id='div_3'></div>
		<div id='div_4'></div>
	</div>
	<div id='div_5' class='BFC'>
		<div id='div_6'></div>
		<div id='div_7'></div>
	</div>
</div>
```
这段代码表示，#div_1创建了一个块格式上下文，这个上下文包括了#div_2、#div_3、#div_4、#div_5。即#div_2中的子元素也属于#div_1所创建的BFC。但由于#div_5创建了新的BFC，所以#div_6和#div_7就被排除在外层的BFC之外。

#### BFC可以解决的问题
1.（BFC与margin）同一个父级块框下，兄弟元素和父子元素的margin会发生重叠问题

2.（BFC与float）父元素高度塌陷问题、兄弟元素覆盖问题



[原文链接](http://web.jobbole.com/83274/)
