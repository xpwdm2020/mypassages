今天早上刚来就逛了一下公司内部交流平台的前端开发模块，看到一个关于“完美css绝对底部”的话题，然后就想起了自己以前在移动端实现底部footer时遇到的问题，于是就来总结一下：

    <!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	    <style>
	        .g-doc{width:100%;height:100%;}
	        .g-hd{height:40px;background: green;}
	        .g-ft{position:absolute;bottom:0;width:100%;height:40px;background: black;}
	    </style>
	</head>
	<body>
	<div class="g-doc">
	    <div class="g-hd"></div>
	    <div class="g-bd">
	        Google一下可以找到很多让页脚紧贴页面底部的方法，我试过其中的很多，但他们总会在某些方面存在一些问题。之所以有这些问题，可能是因为出现了更新版本的浏览器。一些方法因为太过久远，原本在老版本浏览器可以正常工作，却不再适用更新之后的版本。也因为这些页面太过久远，过去曾被大量链接过，所以在Google的结果中排名很高。这样，一些网站管理员在搜索sticky footer方案的时候，对搜索出的结果都很挠头，因为排在搜索结果前列的方法都有这样那样的问题。
	        众所周知的是Ryan Fait的方案，它的确工作的很好。但是，它必须要单独写一个没有内容的div，来提供额外的"push"。对HTML语义要求严格的人可以说代码这么写是不符合规范的，我们的方案不用附加的div。
	        Google一下可以找到很多让页脚紧贴页面底部的方法，我试过其中的很多，但他们总会在某些方面存在一些问题。之所以有这些问题，可能是因为出现了更新版本的浏览器。一些方法因为太过久远，原本在老版本浏览器可以正常工作，却不再适用更新之后的版本。也因为这些页面太过久远，过去曾被大量链接过，所以在Google的结果中排名很高。这样，一些网站管理员在搜索sticky footer方案的时候，对搜索出的结果都很挠头，因为排在搜索结果前列的方法都有这样那样的问题。
	        众所周知的是Ryan Fait的方案，它的确工作的很好。但是，它必须要单独写一个没有内容的div，来提供额外的"push"。对HTML语义要求严格的人可以说代码这么写
	        Google一下可以找到很多让页脚紧贴页面底部的方法，我试过其中的很多，但他们总会在某些方面存在一些问题。之所以有这些问题，可能是因为出现了更新版本的浏览器。一些方法因为太过久远，原本在老版本浏览器可以正常工作，却不再适用更新之后的版本。也因为这些页面太过久远，过去曾被大量链接过，所以在Google的结果中排名很高。这样，一些网站管理员在搜索sticky footer方案的时候，对搜索出的结果都很挠头，因为排在搜索结果前列的方法都有这样那样的问题。
	        众所周知的是Ryan Fait的方案，它的确工作的很好。但是，它必须要单独写一个没有内容的div，来提供额外的"push"。对HTML语义要求严格的人可以说代码这么写
	    </div>
	    <div class="g-ft"></div>
	</div>
	</body>
	</html>
一般，自己都会像上面这样去布局，但是很明显，内容区域的文字是比较少的，于是在改变浏览器窗口大小的时候就会出现底部遮盖文字的现象：

![](https://github.com/Anjing1993/mypassages/blob/master/images/footer.png)

### 这时候我会使用两种方法去解决 ：

- **给底部footer去加固定定位**
 - 在ie6中是失效的（固要考虑项目的兼容范围，或者利用css hack对ie6利用绝对定位，和`_top:expression(eval(document.documentElement.scrollTop+document.documentElement.clientHeight-this.offsetHeight-(parseInt(this.currentStyle.marginTop,10)||0)-(parseInt(this.currentStyle.marginBottom,10)||0)));`进行特殊处理）
 - 移动端中，在ios8以下系统，当小键盘激活时，都会出现位置浮动问题----------->可使用第三方库iscroll.js或者原生css中的absolute+将原body滚动的区域域移到g-bd内部，即`overflow-y: scroll;-webkit-overflow-scrolling: touch`去解决。（但是移动端的坑还是非常多的，不保证这样完美可以所有机型下的这个问题，具体就得另当别论了）
- **让头部，内容区域与底部平分100%**--------->这样失去了灵活性，合理的内容区域应该是自适应的，而不是给死高度（适用于特殊情况）

### 而今天了解到两种好的解决方法：

- **Ryan Fait的方案：提供额外的空div**
		
		<html>
		<head>
		    <meta charset="UTF-8">
		    <style>
		        * {
		            margin: 0;
		        }
		        html, body {
		            height: 100%;
		        }
		        .wrapper {
		            min-height: 100%;
		            height: auto !important;
		            height: 100%;
		            margin: 0 auto -4em;
		        }
		        .footer, .push {
		            height: 4em;
		        }
		        .footer{   background: red;}
		    </style>
		</head>
		<body>
		<div class="wrapper">
		    Google一下可以找到很多让页脚紧贴页面底部的方法，我试过其中的很多，但他们总会在某些方面存在一些问题。之所以有这些问题，可能是因为出现了更新版本的浏览器。一些方法因为太过久远，原本在老版本浏览器可以正常工作，却不再适用更新之后的版本。也因为这些页面太过久远，过去曾被大量链接过，所以在Google的结果中排名很高。这样，一些网站管理员在搜索sticky footer方案的时候，对搜索出的结果都很挠头，因为排在搜索结果前列的方法都有这样那样的问题。
		    众所周知的是Ryan Fait的方案，它的确工作的很好。但是，它必须要单独写一个没有内容的div，来提供额外的"push"。对HTML语义要求严格的人可以说代码这么写是不符合规范的，我们的方案不用附加的div。
		    Google一下可以找到很多让页脚紧贴页面底部的方法，我试过其中的很多，但他们总会在某些方面存在一些问题。之所以有这些问题，可能是因为出现了更新版本的浏览器。一些方法因为太过久远，原本在老版本浏览器可以正常工作，却不再适用更新之后的版本。也因为这些页面太过久远，过去曾被大量链接过，所以在Google的结果中排名很高。这样，一些网站管理员在搜索sticky footer方案的时候，对搜索出的结果都很挠头，因为排在搜索结果前列的方法都有这样那样的问题。
		    众所周知的是Ryan Fait的方案，它的确工作的很好。但是，它必须要单独写一个没有内容的div，来提供额外的"push"。对HTML语义要求严格的人可以说代码这么写
		    Google一下可以找到很多让页脚紧贴页面底部的方法，我试过其中的很多，但他们总会在某些方面存在一些问题。之所以有这些问题，可能是因为出现了更新版本的浏览器。一些方法因为太过久远，原本在老版本浏览器可以正常工作，却不再适用更新之后的版本。也因为这些页面太过久远，过去曾被大量链接过，所以在Google的结果中排名很高。这样，一些网站管理员在搜索sticky footer方案的时候，对搜索出的结果都很挠头，因为排在搜索结果前列的方法都有这样那样的问题。
		    众所
		    <div class="push"></div>
		</div>
		<div class="footer">
		    <p>Copyright (c) 2008</p>
		</div>
		</body>
		</html> 
上面代码实现的思路就是给wrapper设置负的下边距，然后的.push类是没有内容的div，因为它是一个隐藏的元素“推”下页脚，因此不会重叠任何东西。经过测试，发现这种效果是很好的，但是它有个缺陷：

 - 添加了无语义的标签：对HTML语义要求严格的人可以说代码这么写是不符合规范的，我们的方案不用附加的div。所以这取决于我们项目的规范。
 
- **Sticky Footer方案：**在Chrome和其他浏览器中，当我们缩放窗口的时候，页脚会浮上来。这个方案会应用一种Clear fix hack方法，把页脚固定在适当的位置上，这种方法同时也解决了页面布局是两列或三列悬浮可能会带来的问题。在超过50种以上的浏览器测试中，它都能很好的工作。

        <!-- 这个页面的结构是有要求的，footer <div> 标签在wrap <div>标签的外面。总之就是将footer提出来 -->
	    <div id="wrap">

			<div id="header">
		      头部
			</div>
		
			<div id="main" class="clearfix">
		     内容区域
			</div>

		</div>
		    
		<div id="footer">
		
		</div>
但是，如果我们需要在wrap或者footer的外面放一些元素，他们必须使用绝对位置；否则，页面上计算好的100%的高度会被弄乱掉。
布局有了，这时候就来说说最关键的东西，“样式”：

		 html,body,#wrap{height:100%;}/* wrap <div>的height属性把自己拉伸至窗口全部高度的尺寸 */
		 body>#wrap{height:auto;min-height:100%;}
		 #main{padding-bottom:150px;}/* 必须和底部footer的高度相同 */
		 #footer{position:relative;margin-top:-150px;height:150px;clear:both;}/* 负的margin会把footer提高到main <div>的padding的位置上去 */
 
          /* 主要是解决元素悬浮问题，例如两列悬浮布局：内容在一列，sidebar放在另一列，个别浏览器下面main <div>里面的悬浮的内容导致页脚浮上来，这时就需要清除一下了。 */
         .clearfix:after {content: ".";display: block;height: 0;clear: both;visibility: hidden;}
		 .clearfix {display: inline-block;}
		 /* Hides from IE-mac \*/
		 * html .clearfix { height: 1%;}
		.clearfix {display: block;}
		 /* End hide from IE-mac */
当然上面的Ryan Fait的方法，在多列悬浮的页面中，同样需要用到clearfix。

> 注意1：高度和边距

Header，wrap或者main `<div>`标签内部，如果对一些元素使用top或者bottom margin，可能会出现footer被向下移动的现象，移动距离一般是所用的margin的高度。这种情况下，可以使用padding替代margin来填充元素间隙。在页面内容少的情况下，footer本来应该在页面的底部，窗口的滚动条告诉你footer在页面底部偏下的位置。找到那个捣乱的margin，并用padding替换掉。
为main <div>声明padding的时候要多加小心，如果你添加了这样的代码：padding:0 10px 0 10px，你就覆盖了那个至关重要的本来应该和footer一样的padding。Google Chrome中，在页面内容很多的情况下，footer就会和你的页面内容重叠在一起。



> 注意2：字体大小：

设置字体大小的时候，如果你使用相对尺寸，要注意有些访问者可能会在显示器配置中使用较大字体。如果footer下面没有剩余足够的空间来容纳大字体，页面高度的设置就会被破坏，从而导致footer下面有多余的空隙。所以，请使用绝对大小(px)，不要使用pt或者em。

今天学些到的这两种方法是很值得推荐的，他们都巧妙的解决了我们底部绝对定位的问题，希望自己以后多实践，多积累，尽量积累更多的解决方式。