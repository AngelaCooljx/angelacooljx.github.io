// JavaScript Document
/*
$("").mChange({
	auto  : 1,       //是否自动播放,1为自动,0为手动
	arrow : 1,       //是否反转箭头,1为点击左侧向右滚动,0则相反
	speed : 500,     //效果速度,大于0.3
	time  : 5000,    //周期时间，大于1
	nav   : null,    //导航
	nave  : "click", //导航事件
	navs  : 0,  //导航滚动
	prev  : null,    //上一个
	next  : null,    //下一个
	cycle : 1,       //是否循环
	mousestop : 0,   //是否鼠标划入停止
	mousewheel : 0,  //是否开启滚轮事件
	count : null,    //总数
	index : null,    //当前
	fnCome: null,    //回调前函数
	fnBack: null     //回调函数
});
*/
(function($) {
	$.fn.mChange = function(options) {
		var w1,np,ns,v;
		var opts = $.extend({},$.fn.mChange.defaults,options); 
		//初始化
		var c=$(this);
		var f=c.parent();
		var n=$(opts.nav);
		var i=0;
		var sw=1;
		c.hide();
		
		if(opts.navs){
			w1 = n.outerWidth()+(parseInt(n.css("margin-left"))?parseInt(n.css("margin-left")):0)+(parseInt(n.css("margin-right"))?parseInt(n.css("margin-right")):0);
			np= $(opts.nav).parent();
			n.wrapAll("<div class='scroll' style='height:100%;'></div>");
			ns=np.find(".scroll");
			ns.width(n.length*w1);
			np.stop().animate({scrollLeft:0},100);
		}
			
		function run(){
			if(sw){
				i++;
				i=change(i);
			}
		}
		
		$(opts.count).text(c.length);
		
		function change(idx){
			if(c.length>1 || idx=="begin"){
				sw=0;
				if(idx=="begin"){
					idx=0;
					speed=0;
				}
				else{
					speed=opts.speed;
					c.stop(true,true).fadeOut(speed);
				}
				
				n.removeClass("now");
				if(idx==c.length){idx=0;}
				if(idx<0){idx=c.length-1;}
				
				
				$(opts.index).text(idx+1);
				
				c.eq(idx).stop().fadeIn(speed,function(){
					if(typeof(opts.fnBack)=="function"){
						opts.fnBack(idx);//执行自定义动画2
					}
					sw=1;
				});
				if(typeof(opts.fnCome)=="function"){
					opts.fnCome(idx);//执行自定义动画1
				}
				
				n.eq(idx).addClass("now");			
				if(opts.navs){autonav(idx);}
				
				return idx;
			}
		}
		change("begin");
		
		if(opts.auto==1){
			v=setInterval(run,opts.time);
		}
		
		if(opts.mousestop==1){
			c.hover(
				function(){sw=0;},
				function(){sw=1;}
			);
		}
		
		//导航溢出部分滑动显示
		function autonav(idx){
			np.animate({scrollLeft:idx*w1});
		}
			
		n.each(function(index, element) {
            $(this).bind(opts.nave,function(){
				if(c.eq(index).length>0){
					change(index);
					i=index;
					if(opts.auto){
						clearInterval(v);
						v=setInterval(run,opts.time);
					}
				}
			});
        });
		
		$(opts.prev).click(function(){
			if(sw==1){
				if(opts.cycle==1 || (opts.cycle==0 && i>0)){
					i--;
					i=change(i);
					if(opts.auto==1){
						clearInterval(v);
						v=setInterval(run,opts.time);
					}
				}
			}
		});
		$(opts.next).click(function(){
			if(sw==1){
				if(opts.cycle==1 || (opts.cycle==0 && i<c.length-1)){
					i++;
					i=change(i);
					if(opts.auto){
						clearInterval(v);
						v=setInterval(run,opts.time);
					}
				}
			}
		});
		
		if(opts.mousewheel){
			f.mousewheel(function(event,delta,deltaX,deltaY){
				if(delta<0){
					if(sw==1){
						if(opts.cycle==1 || (opts.cycle==0 && i<c.length-1)){
							i++;
							i=change(i);
							if(opts.auto){
								clearInterval(v);
								v=setInterval(run,opts.time);
							}
						}
					}
				}
				else{
					if(sw==1){
						if(opts.cycle==1 || (opts.cycle==0 && i>0)){
							i--;
							i=change(i);
							if(opts.auto){
								clearInterval(v);
								v=setInterval(run,opts.time);
							}
						}
					}
				}
				event.stopPropagation();
				event.preventDefault();
			});
		}
			
	};
	$.fn.mChange.defaults = {
		auto  : 1,
		arrow : 1,
		speed : 800,
		time  : 5000,
		nav   : null,
		nave  : "click",
        navs  : 0,
		prev  : null,
		next  : null,
		cycle : 1,
		mousestop : 0,
	    mousewheel : 0,
		count : null,
		index : null,
		fnCome: null,
		fnBack: null
	}
})(jQuery);