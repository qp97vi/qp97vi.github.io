---
title: 自己用的jquery效果
tags: jQuery
categories: 笔记
---
1.轮播图效果

html代码

```
  <div class="banner">
        <!-- 图片 -->
        <ul class="lunbo">
            <li><img src="../images/banner_1.png" alt=""></li>
            <li><img src="../images/banner_2.png" alt=""></li>
            <li><img src="../images/banner_1.png" alt=""></li>
                <div class="circleNide">
                    <span class="circleSelect"></span>
                    <span></span>
                    <span></span>
                </div>
        </ul>
       
    </div>

```
css
```
.banner{
	padding-top: 106px;
	height: 480px;
	position: relative;
}
.banner .lunbo{
	
	height:480px;
}
.banner .lunbo img{
	width: 100%;
	height: 480px;
}
.banner .lunbo li{
	position:absolute;
	left:0;
	opacity:0;
	cursor: pointer;
	height:480px;
	overflow:hidden;
}
.banner .lunbo li:first-child{
	opacity:1;
}
.circleNide{
	position: absolute;
	bottom: 13px;
	right: 15%;
	z-index: 200;
}
.circleNide span{
	display:block;
	float:left;
	height: 10px;
	width: 10px;
	border: 1px solid #fff;
	-moz-border-radius:50%;
	-ms-border-radius:50%;
	-webkit-border-radius:50%;
	-o-border-radius:50%;
	border-radius: 50%;
	cursor: pointer;
	margin-left: 8px;
 -webkit-transition: .4s ease-in-out;
    -o-transition: .4s ease-in-out;
    transition: .4s ease-in-out
}
.circleNide span:first-child{
	margin-left:0;
}
.circleNide .circleSelect{
	background: #ededed;
	width:26px;
	border-radius: 8px;
	
}
.lunbo{
	position: absolute;
	top: 106px;
	width: 100%;
}
```
js代码
```
;$(function(){
	var li=$(".lunbo li").length;
	// console.log(li)
	var num=-1;
	
	function move(){
		$(".lunbo li").eq(num).stop().animate({
			"opacity":"1",
			"z-index":"1"
		}).siblings("li").stop().animate({
			"z-index":"-1",
			opacity:"0"
		})
		$(".circleNide span").eq(num).addClass("circleSelect").siblings().removeClass("circleSelect")
	}
	var timer = setInterval(go, 3000);
	function go(){
		num++;
		// console.log(num)
		if(num>=li){
			num=0;
		}
		move()
	}
	go()
	$(".circleNide span").hover(function(){
		var index=$(this).index()
		num=index
		$(this).addClass("circleSelect").siblings().removeClass("circleSelect")
		$(".lunbo li").eq(index).stop().animate({
			"z-index":"1",
			"opacity":"1"
		}).siblings("li").stop().animate({
			"z-index":"-1",
			opacity:"0"
		})
		 clearInterval(timer)
	},function(){
		timer = setInterval(go, 3000)
	})
	$(".lunbo li").hover(function(){
		 clearInterval(timer)
	},function(){
		timer = setInterval(go, 3000)
	})
})
```
2.无缝滚动效果

HTML
```
	<div class="scrollBox" id="scrollBox" >
        <ul class="clearfloat scrollUl">
            <li><img src="../images/aboutCdd/scroll1.png" alt=""></li>
            <li><img src="../images/aboutCdd/scroll2.png" alt=""></li>
            <li><img src="../images/aboutCdd/scroll3.png" alt=""></li>
            <li><img src="../images/aboutCdd/scroll4.png" alt=""></li>
            <li><img src="../images/aboutCdd/scroll5.png" alt=""></li>
        </ul>
    </div>
```
css
```
 .scrollBox {
  width: 1200px;
  height: 360px;
  overflow: hidden;
  margin-top: 69px;
  position: relative;
}
 .scrollBox ul {
  height: 360px;
  width:1000%;
   position: absolute;
 right: 0;
  overflow: hidden;
}
.scrollBox li {
 /* margin-left: 12px;*/
 position:relative;
   float: right;

}
 .scrollBox li img{
	margin:0 6px;
}
.scrollBox li:last-child{
	margin-left:0;
}
  .he{
	    position: absolute;
    font-size: 40px;
    font-family: SourceHanSansCN-Normal;
    top: 46px;
    left: 0;
    right:0;
     margin: auto;
	    width: 458px;
    color: #fff;
     text-shadow: 1px 0px 0px #06050D, 
     					-1px 0px 0px #06050D,
     					 0px 1px 0px #06050D, 
     					 0px -1px 0px #06050D;
}
```
js
```
$(function() {
        var odiv = $("#scrollBox");
        var oul = $("#scrollBox ul");
        var ali = $("#scrollBox li");
        var spa = 2;
        var width = 0;
        ali.each(function(index, el) {
            width += $(this).innerWidth()
        });
        oul.width(width * 2)
        oul.html(oul.html() + oul.html());

        function move() {
            if (oul.css('left') == '0px') {
                oul.css('left', -oul.width() / 2 + 'px');
            }
            oul.css('left', '+=' + spa + 'px');
        }
        var timer = setInterval(move, 30)

    })
```