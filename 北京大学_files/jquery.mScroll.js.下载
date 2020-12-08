/*
======示例=====
<style>
body{margin:20px;}
#focus{height:200px;width:500px;position:relative;margin:auto;border:5px solid #ccc;}
.frame{width:100%;height:100%;overflow:hidden;}
.frame .child{height:100%;float:left;}
.nav{position:absolute;width:60px;height:20px;overflow:hidden;left:50%;bottom:5px;margin-left:-31px;border:1px solid #aaa;}
.nav a{float:left;width:20px;height:20px;line-height:20px;font-size:12px;color:#000;text-align:center;background:#f5f5f5;}
.nav a.now{background:#aaa;color:#fff;}
.prev{right:30px;bottom:5px;width:20px;height:20px;line-height:20px;text-align:center;background:#f5f5f5;position:absolute;color:#000;font-size:12px;font-family:Arial;}
.next{right:5px;bottom:5px;width:20px;height:20px;line-height:20px;text-align:center;background:#f5f5f5;position:absolute;color:#000;font-size:12px;font-family:Arial;}
.title{height:30px;line-height:30px;float:left;}
.count{height:30px;line-height:30px;float:right;}
.count b{font-weight:normal;}
.count em{font-style:normal;}
</style>
<div class="focus"><a href="javascript:;" class="prev">&lt;</a><a href="javascript:;" class="next">&gt;</a>
  <div class="frame">
	<div class="child" style="background:#faa;" title="c1"></div>
	<div class="child" style="background:#afa;" title="c2"></div>
	<div class="child" style="background:#aaf;" title="c3"></div>
	<div class="child" style="background:#ffa;" title="c4"></div>
	<div class="child" style="background:#aff;" title="c5"></div>
  </div>
  <div class="nav">
	<i>1</i>
	<i>2</i>
	<i>3</i>
	<i>4</i>
	<i>5</i>
  </div>
  <div class="title"></div>
  <div class="count"><b></b>/<em></em></div>
</div>
<script>
$('.focus .frame').mScroll({
		     auto : 1,                   //自动开始
		direction : "h",                 //滚动方向,h横向,v纵向
		    dtype : "left",              //正反方向
		  isfocus : 0,                   //是否作为焦点图
			minsize :	[
		  						{
										width:0,
										size:1
									},
									{
										width:1000,
										size:4
									}
								],                 //最小数量
		    speed : 500,                 //滚动速度
		   easing : "",                  //缓冲类型
				delay : 5000,                //自动滚动间隔
				  nav : ".focus .nav i",     //导航按钮
				event : "click",             //导航按钮事件类型
		scrollnav : 0,                   //导航滚动
nav_direction : "h",                 //导航方向,h横向,v纵向
				 prev : ".focus .prev",      //前一个
				 next : ".focus .next",      //后一个
				index : ".focus .index",     //当前序号
				count : ".focus .count b",   //总数
				title : ".focus .count em",  //标题
				arrow : 1,                   //是否反转
				cycle : 1,                   //是否循环
		mousestop : 1,                   //鼠标划入停止
	 mousewheel : 0,                   //开启滚轮事件
				touch : 0,                   //开启触摸事件
		 callback : function(idx){}      //回调函数
});
</script>
===============
*/
//变量解释
/*
f=对象主体frame
s=frame内滚动元素
c=s内子元素
n=导航子元素
np=导航父元素
ns=导航内滚动元素
w,h=滚动距离
ww,hh=原始总长度
size=s内子元素原始数量
iv,ti=定时器
sw=控制开关
idx=当前序号
cm=s内子元素边距
*/
(function($) {
	$.fn.mScroll = function(options) {
		var opts = $.extend({},$.fn.mScroll.defaults,options);
		this.each(function(){
			//初始化变量
			var f = $(this);
			var s,c,n,np,ns,w,ww,h,hh,wn,hn,size,iv,ti,sw=1,sw1=0,idx=0,ids=0,idx1=0,cm=0;
			//var tt=5000;
			
			//控制判断初始化
			if(opts.cycle==0){opts.auto=0;}
			if(opts.touch==1){
				opts.minsize=1;
				opts.mousestop=0;
				opts.mousewheel=0;
			}
			
			function getMinsize(){				
				if(typeof(opts.minsize)=="object"){
					var minsize=0;//var minsize=opts.minsize[0].size;
					for(var i=0;i<opts.minsize.length;i++){
						var mz=new Object(opts.minsize[i]);
						if($(window).width()>mz.width){
							minsize=mz.size;
						}
					}
					return minsize;
				}
				else{
					return opts.minsize;
				}
			}
			
			if(f.children().size==1){return false;}
			
			//生成scroll结构，赋值s
			if(f.children().is("ul") && f.children().length>1 && !f.children().hasClass("child")){
				f.children().addClass("scroll");
			}
			else{
				f.children().wrapAll("<div class='scroll' style='height:100%;'></div>");
			}
			s = f.find(".scroll");
			
			//初始化size
			size=s.children().length;			
			
			
			//创建c镜像，赋值c
			if(opts.cycle==1 && size>getMinsize()){s.append(s.html());}
			c = s.children();
			
			//初始化导航
			n = $(opts.nav);
			if(opts.scrollnav){
				wn = parseInt(n.outerWidth()+parseInt(n.css("margin-left"))+parseInt(n.css("margin-right")));
				hn = parseInt(n.outerHeight()+parseInt(n.css("margin-top"))+parseInt(n.css("margin-bottom")));
				np= $(opts.nav).parent();
				n.wrapAll("<div class='scroll' style='height:100%;'></div>");
				n.width(wn);
				ns=np.find(".scroll");
				if(opts.nav_direction=="h"){
					ns.width(n.length*wn);
					np.stop().animate({scrollLeft:0},100);
				}
				if(opts.nav_direction=="v"){
					ns.height(n.length*hn);
					np.stop().animate({scrollTop:0},100);
				}
			}
			n.eq(0).addClass("now");
			if(opts.cycle!==1){$(opts.prev).css("opacity","0.3");}
			
			//初始化各元素尺寸
			function setWH(){
				if(opts.direction=="h"){
					setH();
					s.width(100000);
					s.height("100%");
					f.stop().animate({scrollLeft:0},100);
				}
				if(opts.direction=="v"){		
					setV();		
					s.height(100000);				
					f.stop().animate({scrollTop:0},100);
				}
			}
			setWH();
			
			//尺寸设置函数
			function setH(){
				f.css("width","");
				c.css("width","");
				cm=parseInt(c.last().css("margin-left"))+parseInt(c.last().css("margin-right"));
				if(cm==0){
					w = Math.floor(f.width()/getMinsize());
					if(opts.isfocus!=1){
						f.width(w*getMinsize());
					}
					else{
						f.width("auto");
					}
					c.width(w);
				}
				else{
					//if(opts.isfocus!=1){
						w=Math.floor((f.width()+cm)/4);
						c.width(w-cm);
						f.width(w*getMinsize()-cm);
					//}
				}
				ww=c.length*w;
			}
			function setV(){
				f.height("auto");
				c.css("height","");
				cm=parseInt(c.css("margin-top"))+parseInt(c.css("margin-bottom"));
				if(cm==0){
					h = Math.floor(f.height()/getMinsize());
					if(opts.isfocus!=1){
						f.height(h*getMinsize());
					}
					else{
						f.height("auto");
					}
					c.height(h);
				}
				else{
					if(opts.isfocus!=1){
						h=c.height()+cm;
						f.height(h*getMinsize()-cm);
					}
				}
				hh=c.length*h;
			}
			
			//设置title
			$(opts.count).text(size);
			$(opts.title).text(c.eq(0).attr("title"));
			$(opts.index).text(1);
			
			//焦点图自适应
			$(window).resize(function(){
				if(f.is(":visible")){rs();}
			});
			rs();
			
			//自适应
			function rs(){
				sw==0;
				clearTimeout(ti);
				if(getMinsize()!=0){
					if(opts.direction=="h"){
						setH();
						f.stop().scrollLeft(idx*w);
					}
					if(opts.direction=="v"){
						setV();
						f.stop().scrollTop(idx*h);
					}
					ti=setTimeout(function(){
						sw=1;
					},500);
					//恢复轮播
					if(opts.direction=="h"){
						if(s.width()!==100000){
							setWH();
						}
					}
					if(opts.direction=="v"){
						if(s.height()!==100000){
							setWH();
						}
					}
					if(size<=getMinsize()){
						s.css({margin:"auto",width:w*size});
						$(opts.prev).hide();
						$(opts.next).hide();
					}
					else{
						if(opts.direction=="h"){
							s.removeAttr("style").width(100000);
						}
						if(opts.direction=="v"){
							s.removeAttr("style").height(100000);
						}
						$(opts.prev).show();
						$(opts.next).show();
					}
				}
				else{
					//解除轮播
					f.removeAttr("style");
					s.removeAttr("style");					
				}
				
			}
			
			//判断c数量是否满足开始条件
			if(size>getMinsize()){
			
			//自动开始
			if(opts.auto==1){
				run();
			}
			
			function run(){				
				var t=opts.delay;
				if(idx==0){
					//t=tt;
				}				
				clearTimeout(iv);
				iv=setTimeout(function(){
					move(opts.dtype);
					run();
				},t);
			}
			
			//执行回调函数
			if(typeof(opts.callback)=="function"){
				opts.callback(idx);
			}
			
			//-------------start-------------//
			//滚动函数
			function move(act,speed){
				if(!speed){speed=opts.speed;}
				if(sw==1){
					sw=0;
					if(act=="left"){
						if(opts.cycle!=1){
							if(idx+getMinsize()<size){
								idx++;ids++;
								if(opts.direction=="h"){
									f.animate({scrollLeft:ids*w},speed,opts.easing,function(){sw=1;});
								}
								if(opts.direction=="v"){
									f.animate({scrollTop:ids*h},speed,opts.easing,function(){sw=1;});
								}
								$(opts.prev).css("opacity","1");
								if(idx+getMinsize()==size){
									$(opts.next).css("opacity","0.3");
								}
							}
							else{
								sw=1;								
							}							
						}
						if(opts.cycle==1){	
							if(idx==size-1){idx=0;}
							else{idx++;}
							ids++;
							if(opts.direction=="h"){
								f.animate({scrollLeft:ids*w},speed,opts.easing,function(){									
									if(f.scrollLeft()>=ww*0.5){f.scrollLeft(0);ids=0;}
									sw=1;
								});
							}
							if(opts.direction=="v"){
								f.animate({scrollTop:ids*h},speed,opts.easing,function(){
									if(f.scrollTop()>=hh*0.5){f.scrollTop(0);ids=0;}
									sw=1;
								});
							}
							
						}
					}
					if(act=="right"){
						if(opts.cycle!=1){
							if(idx>0){
								idx--;ids--;
								if(opts.direction=="h"){
									f.animate({scrollLeft:ids*w},speed,opts.easing,function(){sw=1;});
								}
								if(opts.direction=="v"){
									f.animate({scrollTop:ids*h},speed,opts.easing,function(){sw=1;});
								}
								$(opts.next).css("opacity","1");
								if(idx==0){
									$(opts.prev).css("opacity","0.3");									
								}
							}
							else{
								sw=1;
							}
						}
						if(opts.cycle==1){
							if(idx==0){idx=size-1;ids=size;}
							else{idx--;}
							ids--;
							if(opts.direction=="h"){
								if(f.scrollLeft()<=0){f.scrollLeft(ww*0.5);}
								f.animate({scrollLeft:ids*w},speed,opts.easing,function(){sw=1;});
							}
							if(opts.direction=="v"){
								if(f.scrollTop()<=0){f.scrollTop(hh*0.5);}
								f.animate({scrollTop:ids*h},speed,opts.easing,function(){sw=1;});
							}
						}
					}						
					n.removeClass("now");
					n.eq(idx).addClass("now");
					$(opts.title).text(c.eq(idx).attr("title"));
					$(opts.index).text(idx+1);					
					if(opts.scrollnav){autonav();}
					if(typeof(opts.callback)=="function"){
						opts.callback(idx);//执行自定义动画
					}
				}
			}
			//左右按钮
			if(opts.prev){
				$(opts.prev).hover(function(){sw=1;});
				$(opts.prev).unbind("click");
				$(opts.prev).click(function(){
					if(opts.arrow==1){move("right");}
					else{move("left");}
					if(opts.auto){
						//clearInterval(iv);
						//iv = window.setInterval(function(){move(opts.dtype);},opts.delay);
						run();
					}
					if(idx1>0){idx1--;c.eq(idx1).click();}
					
				});
				
			}
			if(opts.next){
				$(opts.next).hover(function(){sw=1;});
				$(opts.next).unbind("click");
				$(opts.next).click(function(){
					if(opts.arrow==1){move("left");}
					else{move("right");}
					if(opts.auto){
						//clearInterval(iv);
						//iv = window.setInterval(function(){move(opts.dtype);},opts.delay);
						run();
					}
					if(idx1<size-1){idx1++;c.eq(idx1).click();}
					
				});
			}
			c.click(function(){
				idx1=$(this).index();
			});
			
			//导航溢出部分滑动显示
			function autonav(){
				if(opts.nav_direction=="h"){					
					if(np.width()==wn){					
						np.stop().animate({scrollLeft:wn*idx},opts.navspeed);
					}
					else{
						if(idx*wn==np.scrollLeft()){
							np.stop().animate({scrollLeft:np.scrollLeft()-wn},opts.navspeed);
						}
						if((idx+1)*wn==np.scrollLeft()+np.width()){
							np.stop().animate({scrollLeft:np.scrollLeft()+wn},opts.navspeed);
						}
						if(idx==0){np.stop().animate({scrollLeft:0},opts.navspeed);}
						if(idx==size-1){np.stop().animate({scrollLeft:size*wn},opts.navspeed);}
						if(np.width()%wn!=0){console.log('宽度设置错误');}
					}
				}
				if(opts.nav_direction=="v"){
					if(idx*hn==np.scrollTop()){
						np.stop().animate({scrollTop:np.scrollTop()-hn},opts.navspeed);
					}
					if((idx+1)*hn==np.scrollTop()+np.height()){
						np.stop().animate({scrollTop:np.scrollTop()+hn},opts.navspeed);
					}
					if(idx==0){np.stop().animate({scrollTop:0},opts.navspeed);}
					if(idx==size-1){np.stop().animate({scrollTop:size*hn},opts.navspeed);}
				}
			}
			//导航点击
			n.each(function(index, element) {
				$(this).bind(opts.event,function(){
					if(opts.direction=="h"){f.stop().animate({scrollLeft:index*w},opts.speed,opts.easing,function(){sw=1;});}
					if(opts.direction=="v"){f.stop().animate({scrollTop:index*h},opts.speed,opts.easing,function(){sw=1;});}
					idx=index;
					ids=index;
					$(opts.prev).css("opacity","1");
					$(opts.next).css("opacity","1");
					if(idx+getMinsize()==size){
							$(opts.next).css("opacity","0.3");
					}
					if(idx==0){
							$(opts.prev).css("opacity","0.3");
					}
					n.removeClass("now");
					n.eq(idx).addClass("now");
					if(opts.scrollnav){autonav();}
					$(opts.title).text(c.eq(idx).attr("alt"));
					//执行回调函数
					if(typeof(opts.callback)=="function"){
						opts.callback(idx);
					}
					if(opts.auto){
						//clearInterval(iv);
						//iv = window.setInterval(function(){move(opts.dtype);},opts.delay);
						run();
					}						
				});
			});
			//鼠标滚轮
			if(opts.mousewheel){
				f.mousewheel(function(event,delta,deltaX,deltaY){
					if(delta<0){
						if(opts.arrow==1){move("left");}
						else{move("right");}
					}
					else{
						if(opts.arrow==1){move("right");}
						else{move("left");}
					}
					event.stopPropagation();
					event.preventDefault();
				});
			}
			//鼠标划入停止
			if(opts.mousestop && !opts.mousewheel){
				f.hover(function(){sw=0},function(){sw=1});
			}
			
			//触摸控制
			if(opts.touch && document.addEventListener){
				f.attr("id","frame"+f.offset().top);
				var touch,p0,fl,m;
				var obj1=document.getElementById(f.attr("id"));
				var start,end="";
				
				obj1.addEventListener('touchstart',function(event){
					if(sw==1){
						sw1=1;
						touch = event.targetTouches[0];
						if(opts.direction=="h"){
							p0=touch.screenX;
							start=touch.screenX;
							fl=f.scrollLeft();
							m=w;
						}
						if(opts.direction=="v"){
							p0=touch.screenY;
							start=touch.screenY;
							fl=f.scrollTop();
							m=h;
						}						
						if(opts.auto){
							clearInterval(iv);
						}
					}
				},false);
				obj1.addEventListener('touchmove',function(event){
					if(sw==1 && sw1==1){
						touch = event.targetTouches[0];
						if(opts.direction=="h"){
							f.scrollLeft(fl-(touch.screenX-p0));
							end=touch.screenX;
							if(Math.abs(touch.screenX-p0)>$(window).width()*0.05){
								event.preventDefault();//阻止浏览器默认事件
							}
						}
						if(opts.direction=="v"){
							f.scrollTop(fl-(touch.screenY-p0));
							end=touch.screenY;
							if(Math.abs(touch.screenY-p0)>f.height()*0.05){
								
							}
							event.preventDefault();//阻止浏览器默认事件
						}
					}
				},false);
				obj1.addEventListener('touchend',function(event){
					if(sw==1 && end!=""){
						if(end-start<m*-0.1){
							move("left",(m-Math.abs(end-start))/m*opts.speed);
						}
						else if(end-start>m*0.1){
							move("right",(m-Math.abs(end-start))/m*opts.speed);
						}
						else{
							sw=0;						
							if(opts.direction=="h"){
								f.stop().animate({scrollLeft:ids*m},opts.speed*0.5,opts.easing,function(){sw=1;});
							}
							else{
								f.stop().animate({scrollTop:ids*m},opts.speed*0.5,opts.easing,function(){sw=1;});
							}
							
						}
						if(opts.auto){
							//clearInterval(iv);
							//iv = window.setInterval(function(){move(opts.dtype);},opts.delay);
							run();
						}
						sw1=0;
						end="";
					}
				},false);
			}
				
			//-------------end-------------//
			}
		})
	};
	$.fn.mScroll.defaults = {
		     auto : 1,                    //自动开始
		direction : "h",                  //滚动方向,h横向,v纵向
		    dtype : "left",               //正反方向
		  isfocus : 0,                    //是否作为焦点图
		  minsize : 1,                    //最小数量
		    speed : 500,                  //滚动速度
		   easing : "",                   //缓冲类型
			delay : 5000,                 //自动滚动间隔
			  nav : null,                 //导航按钮
			event : "click",              //导航事件
        scrollnav : 0,                    //导航滚动
		 navspeed : 500,                  //导航滚动速度
    nav_direction : "h",                  //导航方向,h横向,v纵向
			 prev : null,                 //前一个
			 next : null,                 //后一个
		    index : null,                 //当前序号
			count : null,                 //总数
			title : null,                 //标题
			arrow : 1,                    //是否反转
			cycle : 1,                    //是否循环
		mousestop : 1,                    //鼠标划入停止
	   mousewheel : 0,                    //开启滚轮事件
	        touch : 0,                    //开启触摸事件
		 callback : function(idx){}       //回掉函数
	}
})(jQuery);