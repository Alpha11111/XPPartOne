---
layout: default
title: div + css 弹窗
excerpt: 'div弹出层，div+css弹出层'
image: /images/feature/first-ft.png
---	
<h4>css样式：</h4>
<pre>
<xmp>
<style>
    .point{
    	position:relative;
    }
    .pop{
    	position:relative; 
    	/*top:20%;*/
    	/*left:50%;*/ 
    	width:90%;
    	height:100%; 
    	margin-top: 10%;
    	margin-left: 5%; 
    	margin-right: 5%;
    	background-color: white;
    	overflow:auto;
    }
    .shadow{
    	z-index:9;width:100%; 
    	height:100%;
    	left:0;
    	top:0; 
    	position:fixed;
    	background:rgba(0,0,0,0.3);
    }
</style>
</xmp>
</pre>

<h4>div代码段：</h4>
<pre>
<xmp>
<div  style="">
<div class="point">
    <div class="pop">
   		弹窗内容
    </div>
</div>
</div>
</xmp>
</pre>
