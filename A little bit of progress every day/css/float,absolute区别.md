### float和absolute的区别

一个html文档的正常文档流应该是所有块级元素从上往下依次排列，所有行内元素沿着行间排列。

而bfc则是打破了这种排列，float(不为none)和position(不为默认的static或relative)就是bfc的两种用例，均会脱离文档流，float会挤占文档流的空间，position不会

当float的属性值不为none的时候，就会触发bfc，它可以让块元素脱离文档流原本的排列顺序也沿着行间排列，这就是浮动。主要来解决图文混排中文字环绕问题。

position的属性值不为默认的static或relative的时候也会触发元素的bfc，使得元素脱离原文档流，拥有定位的功能。


###### 当一个元素设置了absolute，但是未设置left/top的时候，那么这个元素的位置会在何处？


绝对定位元素如果申明了置入值(left,top等)，那么其置入值的参照物即为最近的父级定位元素。

如果没有申明置入值，只申明了position:absolute，left/top值为‘auto’，那么其自身定位以及margin的参照物即为其最近的块级、单元格（table cell）或者行内块（inline-block）祖先元素的内容框。

[在线预览效果](https://xiaokuaizi.github.io/case-css/float-position/float-position.html)

[了解BFC点击此处](https://github.com/xiaokuaizi/articles-summary/blob/master/A%20little%20bit%20of%20progress%20every%20day/css/BFC.md)

