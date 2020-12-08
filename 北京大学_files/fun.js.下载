function loadimg(imglist){
	var i=0;
	var run;	
	$(imglist).each(function(index, element) {
		$(this).attr("data",$(this).attr("src"));
		$(this).attr("src","");
		$(this).addClass("unload");
	});
	
	run = function(img){
		i++;
		if($(window).scrollTop()+$(window).height()>img.offset().top){
			img.load(function(){
				if($("img.unload").eq(0).length>0 && i<1000){
					run($("img.unload").eq(0));
				}
			});
			img.attr("src",img.attr("data")).removeClass("unload");
		}
	}
	run($("img.unload").eq(0));
	$(window).scroll(function(){
		if($("img.unload").eq(0).length>0 && i<1000){
			run($("img.unload").eq(0));
		}
	});
}

//滚动触发,fix:0-10
function scrollact(e,fix,fncome){
	var h=0;
	if(!fncome){fncome=function(){};}
	//if(!fnback){fnback=function(){};}
	if($(e).length>0){
		if(!fix && fix!=0){fix=5;}
		fix=$(window).height()*fix*0.1;
		//var h=$(window).height()-$(e).height()>0?$(window).height()-$(e).height():0;//补偿
		if($(window).scrollTop()+fix+h>=$(e).offset().top){
			if(!$(e).hasClass("showdiv")){
				$(e).addClass("showdiv");
				fncome();
			}		
			//return true;
		}
		/*else{
			if($(e).hasClass("showdiv")){
				$(e).removeClass("showdiv");
				fnback();
			}
			//return false;
		}*/
	}
}
//移动端简易分页
function split_page(e,btn,num){
	num=num==undefined?8:num;
	$(e).children().hide();
	$(e).children().slice(0,num).show();
	$(e).attr("page",num);
	if($(e).children().length>num){
		$(btn).show();
	}
	else{
		$(btn).hide();
	}
	$(btn).click(function(){
		$(e).children().slice(0,parseInt($(e).attr("page")+num)).show();
	});
}

//视频自适应
function videofix(e,w,h,fw,fh){
	if(w>=h){
		$(e).css({width:fw,height:fw*(h/w)});
	}
	else{
		$(e).css({width:fh*(w/h),height:fh});
	}
}


//简易iscroll
function mIscroll(frame,child,prev,next,speen,fn){
	var idx=0,sw=1;
	if(!fn){fn=function(){};}
	$(frame).stop().animate({scrollLeft:0},100);
	$(prev).click(function(){
		if(idx>0){
			idx--;
			run(1);
		}
	});
	$(next).click(function(){
		if(idx<$(child).length-1){
			idx++;
			run(1);
		}
	});
	$(child).click(function(index){
			//if(sw==1){
				idx=$(this).index();
				run(2);
				
				if(idx==$(child).length-1){
					$(next).hide();
				}
				else{
					$(next).show();
				}
				if(idx==0){
					$(prev).hide();
				}
				else{
					$(prev).show();
				}
				if($(child).length==1){
					$(prev).hide();
					$(next).hide();
				}
			//}
	});
	function run(type){	
		var e=$(child).eq(idx);		
		var w1=0,w2=0,w3,w4;
		$(child).slice(0,idx+1).each(function(index, element) {
			w1+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
		});
		$(child).slice(0,idx).each(function(index, element) {
			w2+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
		});
		w3=$(child).eq(idx+1).outerWidth()+parseInt($(child).eq(idx+1).css("margin-left"))+parseInt($(child).eq(idx+1).css("margin-right"));
		w4=$(child).eq(idx-1).outerWidth()+parseInt($(child).eq(idx-1).css("margin-left"))+parseInt($(child).eq(idx-1).css("margin-right"));
		if(type==1){
			sw=0;
			if($(frame).scrollLeft()+$(frame).width()<w1){
				$(frame).stop().animate({scrollLeft:w1-$(frame).width()},speen,"jswing",function(){sw=1;});
			}
			if($(frame).scrollLeft()>w2){
				$(frame).stop().animate({scrollLeft:w2},speen,"jswing",function(){sw=1;});
			}
			fn(idx);
			sw=1;
		}
		if(type==2){
			if($(frame).scrollLeft()+$(frame).width()<w1+w3){
				sw=0;
				$(frame).stop().animate({scrollLeft:w1+w3-$(frame).width()},speen,"jswing",function(){sw=1;});
			}
			if($(frame).scrollLeft()>=w2-w4){
				sw=0;
				$(frame).stop().animate({scrollLeft:w2-w4},speen,"jswing",function(){sw=1;});
			}
		}
	}
}

//简易iscroll2
function mIscroll2(frame,child,prev,next,speen){
	var idx;
	var w=0,w1=0,w2;
	
	if($(frame).attr("idx")==undefined){$(frame).attr("idx",0);}
	idx=parseInt($(frame).attr("idx"));
	
	$(child).slice(0,idx).each(function(index, element) {
		w1+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
	});
	$(frame).stop().animate({scrollLeft:w1},0);	
	
	$(prev).click(function(){
		w=0,w1=0;
		idx=parseInt($(frame).attr("idx"));
		while(1){
			console.log(idx);
			if(idx<0){
				$(frame).stop().animate({scrollLeft:0},w);
				break;
			}
			w=w+$(child).eq(idx).outerWidth()+parseInt($(child).eq(idx).css("margin-left"))+parseInt($(child).eq(idx).css("margin-right"));
			if(w>$(frame).width()){
				$(child).slice(0,idx).each(function(index, element) {
					w1+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
				});
				if(w1>$(frame).width()){w2=$(frame).width();}
				else{w2=w;}
				
				$(frame).stop().animate({scrollLeft:w1},w2*2);
				$(frame).attr("idx",idx);
				break;
			}
			idx--;				
		}
	});
	$(next).click(function(){		
		w=0,w1=0;
		idx=parseInt($(frame).attr("idx"));		
		while(1){
			if(idx>$(child).length-1){
				break;
			}
			w=w+$(child).eq(idx).outerWidth()+parseInt($(child).eq(idx).css("margin-left"))+parseInt($(child).eq(idx).css("margin-right"));
			if(w>$(frame).width()){
				$(child).slice(0,idx).each(function(index, element) {
					w1+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
				});
				
				if($(frame).children().width()-($(frame).scrollLeft()+$(frame).width())<$(frame).width()){
					w2=$(frame).children().width()-($(frame).scrollLeft()+$(frame).width());
				}
				else if(w1>$(frame).width()){w3=$(frame).width();}
				else{w2=w*2;}
				
				$(frame).stop().animate({scrollLeft:w1},w2*2);
				$(frame).attr("idx",idx);
				break;
			}
			idx++;
		}
	});
}

//弹出层
function showlayer(e,fun,type){
	if(!fun){fun=function(){};}	
	if($(e).find(".sbar").length>0){
		$(e).find(".sbar").mCustomScrollbar();
	}
	$(e).addClass("showdiv");
	fun();	
}
function hidelayer(e,fun,type){
	if(!fun){fun=function(){};}
	$(e).removeClass("showdiv");
	if(typeof(player)!="undefined"){player.pause();}
	fun();	
	if($(e).find(".playing").length>0){
		var v=$(e).find(".playing")[0];
		v.pause();
		$(e).find(".playing").removeClass("playing");
	}
}

//自动调整底部,配合相应class
function autofoot(){
	/*var wh=$(window).height();
	var dh=$(document.body).height();
	if($(".footer").attr("class")=="footer_b"){
		dh=$(document.body).height()+$(".footer").height();;
	}
	setTimeout(function(){
		if(wh>dh){
			$(".footer").addClass("footer_b");
		}
		else{
			$(".footer").removeClass("footer_b");
		}
	},1000);*/
	$(".body").css("min-height",$(window).height()-$(".footer").outerHeight()-$(".header").outerHeight());
	$(".body.page").css("min-height",$(window).height()-$(".footer").outerHeight());
}

//建立下拉列表功能，待验证
function selector(e){
	$(e).hover(
		function(){
			$(this).find("ul").show();
		},
		function(){
			$(this).find("ul").hide();
		}
	);
	$(e).find("li").click(function(){
		$(this).parents(e).find("input").val($(this).text());
		$(this).parent().hide();
	});
}

//tab切换
function tabdiv(tab,div,event,type,speed,fn){
	if(!fn){fn=function(){};}
	speed=isNaN(speed)?0:speed;
	if(typeof(tab)!="object"){
		tab=$(tab);
	}
	if(typeof(div)!="object"){
		div=$(div);
	}
	div.each(function(index, element) {
    $(this).attr("idx",index);
  });
	tab.each(function(index, element) {
    $(this).bind(event,function(){
			tab.removeClass("now");
			$(this).addClass("now");
			if(type==1){
				div.filter("[idx!='"+index+"']").stop(true,true).hide();
			}
			if(type==2){
				div.filter("[idx!='"+index+"']").stop(true,true).fadeOut(speed);
			}
			if(type==3){
				div.filter("[idx!='"+index+"']").removeClass("act");
				div.filter("[idx='"+index+"']").addClass("act");
			}
			if(type!=3){
				div.filter("[idx='"+index+"']").stop(true,true).fadeIn(speed,function(){
					fn($(this));				
				});
			}
		});
  });
	if(tab.parent().find(".now").length==0){
		tab.eq(0).trigger(event);
	}
	else{
		tab.eq(tab.parent().find(".now")).trigger(event);
	}
}

//箭头切换
function arrowdiv(prev,next,div,type,speed,fn){
	var idx=0;
	if(!fn){fn=function(){};}
	speed=isNaN(speed)?0:speed;
	if(typeof(prev)!="object"){
		tab=$(prev);
	}
	if(typeof(next)!="object"){
		tab=$(next);
	}
	if(typeof(div)!="object"){
		div=$(div);
	}
	div.each(function(index, element) {
    $(this).attr("idx",index);
  });
  $(prev).bind("click",function(){
		idx--;
		if(idx<0){idx=div.length-1;}
		if(type==1){
			div.filter("[idx!='"+idx+"']").stop(true,true).hide();
		}
		if(type==2){
			div.filter("[idx!='"+idx+"']").stop(true,true).fadeOut(speed);
		}		
		div.filter("[idx='"+idx+"']").stop(true,true).fadeIn(speed,function(){
			fn($(this));
		});			
  });
	$(next).bind("click",function(){
		idx++;
		if(idx>=div.length){idx=0;}
		if(type==1){
			div.filter("[idx!='"+idx+"']").stop(true,true).hide();
		}
		if(type==2){
			div.filter("[idx!='"+idx+"']").stop(true,true).fadeOut(speed);
		}		
		div.filter("[idx='"+idx+"']").stop(true,true).fadeIn(speed,function(){
			fn($(this));
		});		
  });
	div.hide();
	div.eq(0).show();
}

//箭头切换
function arrowdiv1(prev,next,div1,div2,type,speed){
	var idx=0;
	if(typeof(prev)!="object"){
		tab=$(prev);
	}
	if(typeof(next)!="object"){
		tab=$(next);
	}
	if(typeof(div1)!="object"){
		div1=$(div1);
	}
	if(typeof(div2)!="object"){
		div2=$(div2);
	}
	div1.each(function(index, element) {
    $(this).attr("idx",index);
  });
  $(prev).bind("click",function(){		
		if(idx>0){
			idx--;
			div2.removeClass("now");
			div2.eq(idx).addClass("now");
			if(type==1){
				div1.filter("[idx!='"+idx+"']").stop(true,true).hide();
			}
			if(type==2){
				div1.filter("[idx!='"+idx+"']").stop(true,true).fadeOut(speed);
			}
			div1.filter("[idx='"+idx+"']").stop(true,true).fadeIn(speed);
		}
  });
	$(next).bind("click",function(){		
		if(idx+1<div2.length){
			idx++;
			div2.removeClass("now");
			div2.eq(idx).addClass("now");
			if(type==1){
				div1.filter("[idx!='"+idx+"']").stop(true,true).hide();
			}
			if(type==2){
				div1.filter("[idx!='"+idx+"']").stop(true,true).fadeOut(speed);
			}
			div1.filter("[idx='"+idx+"']").stop(true,true).fadeIn(speed);
		}
  });
	div1.hide();
	div1.eq(0).show();
	div2.removeClass("now");
	div2.eq(0).addClass("now");
}

//tab切换1
function tabdiv1(prev,next,div,speed,fn){
	var idx=0;
	if(!fn){fn=function(){};}
	speed=isNaN(speed)?0:speed;
	if(typeof(prev)!="object"){
		tab=$(prev);
	}
	if(typeof(next)!="object"){
		tab=$(next);
	}
	if(typeof(div)!="object"){
		div=$(div);
	}
	div.each(function(index, element) {
    $(this).attr("idx",index);
  });
  $(prev).bind("click",function(){
		idx--;
		if(idx<0){idx=div.length-1;}
		div.filter("[idx!='"+idx+"']").stop(true,true).hide();
		div.filter("[idx='"+idx+"']").fadeIn(speed,function(){
			fn($(this));
		});			
  });
	$(next).bind("click",function(){
		idx++;
		if(idx>=div.length){idx=0;}
		div.filter("[idx!='"+idx+"']").stop(true,true).hide();
		div.filter("[idx='"+idx+"']").fadeIn(speed,function(){
			fn($(this));
		});			
  });
	//if(tab.parent().find(".now").length==0){
	div.hide();
	div.eq(0).show();
	//}
	//else{
		//tab.eq(tab.parent().find(".now")).click();
	//}
}

//tab切换2，适用于滚动导航切换
function tabdiv2(prev,next,div,fn){
	var idx=0;
	if(!fn){fn=function(){};}
	if(typeof(prev)!="object"){
		tab=$(prev);
	}
	if(typeof(next)!="object"){
		tab=$(next);
	}
	if(typeof(div)!="object"){
		div=$(div);
	}
	div.each(function(index, element) {
    $(this).attr("idx",index);
  });
  $(prev).bind("click",function(){
		if(idx>0){
			idx--;
		}		
		div.filter("[idx!='"+idx+"']").removeClass("now");
		div.filter("[idx='"+idx+"']").addClass("now");
		fn(idx);
  });
	$(next).bind("click",function(){
		if(idx<div.length-1){
			idx++;			
		}
		div.filter("[idx!='"+idx+"']").removeClass("now");
		div.filter("[idx='"+idx+"']").addClass("now");
		fn(idx);
  });
	div.click(function(){
		idx=parseInt($(this).attr("idx"));
		div.filter("[idx!='"+idx+"']").removeClass("now");
		$(this).addClass("now");
		fn(idx);
		//run(0);
	});
	/*function run(type){	
		var e=div.eq(idx);
		if(type!=0){e.click();}
		var w1=0,w2=0;
		div.slice(0,idx+1).each(function(index, element) {
			w1+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
		});
		div.slice(0,idx).each(function(index, element) {
			w2+=$(this).outerWidth()+parseInt($(this).css("margin-left"))+parseInt($(this).css("margin-right"));
		});
		if(div.parent().scrollLeft()+$(frame).width()<w1){
			div.parent().stop().animate({scrollLeft:w1-$(frame).width()},500);
		}
		if(div.parent().scrollLeft()>w2){
			div.parent().stop().animate({scrollLeft:w2},500);
		}
	}*/
	div.eq(0).addClass("now");
	fn(0);
}
//数字初始化效果
function shownum(e,time){
	var stv_sn,t,x,z,y=0;
	if($(e).attr("num")==undefined){
		x=parseInt($(e).text());
		$(e).attr("num",$(e).text());
	}
	else{
		x=$(e).attr("num");
	}
	var x0=$(e).attr("num");
	
	if(x>time/15){
		t=15;
		z=x/(time/15);
	}
	else{
		t=time/x;
		z=1;
	}
	clearInterval(stv_sn);
	stv_sn=setInterval(function(){
		y=y+z;
		$(e).text(Math.ceil(y));
		if(Math.ceil(y+z)>=x){
			$(e).text(x0);
			clearInterval(stv_sn);
		}
	},t);	
}

//填满容器
function fullFill(e,w,h,ww,hh){	
	if(w/h>ww/hh){
		$(e).css({height:hh,width:hh/h*w,marginLeft:(hh/h*w-ww)*-0.5});
	}
	else{
		$(e).css({width:ww,height:ww/w*h,marginTop:(ww/w*h-hh)*-0.5});
	}
}

//时间比大小
function countDate(start,end){
	//创建Date变量：
	start = Date.parse(start.replace(/-/g,"/"));
	var date1 = new Date(start); //开始时间
	end = Date.parse(end.replace(/-/g,"/"));
	var date2=new Date(end);    //结束时间
	var date3=date2.getTime()-date1.getTime()  //时间差的毫秒数
	
	//计算出相差天数
	var days=Math.floor(date3/(24*3600*1000));
	//计算出小时数
	var leave1=date3%(24*3600*1000)    //计算天数后剩余的毫秒数
	var hours=Math.floor(leave1/(3600*1000));
	if(hours<10 && hours>=0){hours="0"+hours;}
	if(hours<0){hours="00";}
	//计算相差分钟数
	var leave2=leave1%(3600*1000)        //计算小时数后剩余的毫秒数
	var minutes=Math.floor(leave2/(60*1000));
	if(minutes<10 && minutes>=0){minutes="0"+minutes;}
	if(minutes<0){minutes="00";}
	//计算相差秒数
	var leave3=leave2%(60*1000)      //计算分钟数后剩余的毫秒数
	var seconds=Math.round(leave3/1000);
	if(seconds<10 && seconds>=0){seconds="0"+seconds;}
	if(seconds<0){seconds="00";}
	
	//var now=hours+":"+minutes+":"+seconds;
	if(days>0){
		return days+"天";
	}
	if(days==0){
		return "当天";
	}
	if(days<0){
		return "过期";
	}
	else if(hours>0){
		return hours+"小时";
	}
	else if(minutes>0){
		return minutes+"分";
	}
	else{
		return seconds+"秒";
	}
	//var now=+days+"天"+hours+"小时"+minutes+"分"+seconds+"秒";
}

//获取当前时间
function getNowDate(lite) {
	var date = new Date();
	var sign1 = "-";
	var sign2 = ":";
	var year = date.getFullYear() // 年
	var month = date.getMonth() + 1; // 月
	var day  = date.getDate(); // 日
	var hour = date.getHours(); // 时
	var minutes = date.getMinutes(); // 分
	var seconds = date.getSeconds() //秒
	var weekArr = ['星期一', '星期二', '星期三', '星期四', '星期五', '星期六', '星期天'];
	var week = weekArr[date.getDay()];
	// 给一位数数据前面加 “0”
	if (month >= 1 && month <= 9) {
	month = "0" + month;
	}
	if (day >= 0 && day <= 9) {
	day = "0" + day;
	}
	if (hour >= 0 && hour <= 9) {
	hour = "0" + hour;
	}
	if (minutes >= 0 && minutes <= 9) {
	minutes = "0" + minutes;
	}
	if (seconds >= 0 && seconds <= 9) {
	seconds = "0" + seconds;
	}
	var currentdate
	if(lite=="lite"){
		currentdate = year + sign1 + month + sign1 + day;// + " " + week;
	}
	else{
		currentdate = year + sign1 + month + sign1 + day + " " + hour + sign2 + minutes + sign2 + seconds;// + " " + week;
	}
	return currentdate;
}


//设置cookie
function setCookie(c_name,value,expiredays){
	var exdate=new Date()
	exdate.setDate(exdate.getDate()+expiredays)
	document.cookie=c_name+ "=" +escape(value)+((expiredays==null) ? "" : ";expires="+exdate.toGMTString());
}

function getCookie(c_name){
	if(document.cookie.length>0){
		c_start=document.cookie.indexOf(c_name + "=")
		if(c_start!=-1){ 
			c_start=c_start + c_name.length+1 
			c_end=document.cookie.indexOf(";",c_start)
			if(c_end==-1)c_end=document.cookie.length;
			return unescape(document.cookie.substring(c_start,c_end))
		}
	}
	return "";
}

//是否支持html5
function ishtml5(){
	if(typeof(Worker)!=="undefined"){
		return true;
	}
	else{
		return false;
	}	
}

//是否支持css3
function isCss3(style) {
	var prefix = ['webkit', 'Moz', 'ms', 'o'],
	i,
	humpString = [],
	htmlStyle = document.documentElement.style,
	_toHumb = function(string) {
		return string.replace(/-(\w)/g,
		function($0, $1) {
			return $1.toUpperCase();
		});
	};

	for (i in prefix) humpString.push(_toHumb(prefix[i] + '-' + style));

	humpString.push(_toHumb(style));

	for (i in humpString) if (humpString[i] in htmlStyle) return true;

	return false;
}


//获取随机数
function GetRandomNum(Min,Max){   
	var Range = Max - Min;   
	var Rand = Math.random();   
	return(Min + Math.round(Rand * Range));
}


//子导航定位
function navchildfix(nav,e){
	var x=$(nav).offset().left;
	var fix=$(e).parent().offset().left;
	//console.clear();
	//console.log(x0);
	if(x-fix+$(e).outerWidth()<=$(e).parent().width()){
		$(e).css({marginLeft:x-fix,float:"left",textAlign:"left"});
	}
	else{
		$(e).css({marginLeft:0,float:"right",textAlign:"right"});
	}
}

//div拖动
function movebox(e,c){
	var ww=$(window).width();
	var wh=$(window).height();
	var sw_m=0;
	var x_start,y_start,ol,ot;
	$(c).css("cursor","move");
	$(c).mousedown(function(event){
		sw_m=1;
		x_start=event.clientX;
		y_start=event.clientY;
		ol=$(e).offset().left;
		ot=$(e).offset().top;		
	});
	$("body").mousemove(function(event){
		if(sw_m==1){
			var x_move=event.clientX;
			var y_move=event.clientY;
			var ml=(x_move-x_start)+ol;
			var mt=(y_move-y_start)+ot;
			if(ml<0){ml=0;}
			if(ml>ww-$(e).outerWidth()){ml=ww-$(e).outerWidth();}
			if(mt<0){mt=0;}
			if(mt>wh-$(e).outerHeight()){mt=wh-$(e).outerHeight();}
			//$(e).css({left:ml,top:mt,margin:0});
			$(e).css({"transform":"translate("+ml+"px,"+mt+"px)"});
		}
	});
	$("body").mouseup(function(event){
		sw_m=0;
	});
}

//手机跳转
function mjump(url){
	var ua=navigator.userAgent.toLowerCase();
	if(ua.match(/iPad/i)=="ipad" || ua.match(/iphone/i)=="iphone" || ua.match(/android/i)=="android") { 
		location=url;
	}
}

function tapcopy(str,fun){
	var input = document.createElement("input");
	input.setAttribute("readonly","readonly");
	input.value = str;
	document.body.appendChild(input);
	input.select();
	input.setSelectionRange(0, input.value.length), document.execCommand('Copy');
	document.body.removeChild(input);
	if(typeof(fun)=="function"){
		fun();
	}
}

function auto_nav(){
	$('.nav_child .item').show();
	$(".nav_main a").each(function(index, element) {
        var w=0;
		var l=$(this).offset().left+$(this).outerWidth()*0.5-$(".nav_child").offset().left;
		
		var ci=$(".nav_child .item").eq(index);
		ci.each(function(index, element) {
            w+=$(this).outerWidth();
        });
		//$(".nav_child .child").eq(index).width(w);
		
		l=l+w*-0.5;
		
		if(l+w>$(".nav_child").width()){
			ci.css({left:"auto",right:0});
		}
		else if(w<0){
			ci.css({left:0});
		}
		else{
			ci.css({left:l});
		}
    });
	$('.nav_child .item').hide();
}

// JavaScript Document

(function($) {
	$.fn.setBlock = function(options) {
		var opts = $.extend({},$.fn.setBlock.defaults,options); 
		//初始化
		var sw=0,x=0,y=0,x1,y1,n;
		var f=$(this);
		//f.css({positon:"absolute",cursor:"Crosshair"});
		f.each(function(){
			$(this).mousedown(function(event){
				sw=1;
				x=event.clientX;
				y=event.clientY;
				x1=parseInt($(this).css("left"));
				y1=parseInt($(this).css("top"));
				n=$(this);
			});
			$(this).mouseup(function(){
				sw=0;
			});
		});
		$(window).mouseup(function(){
			sw=0;
		});
		$(window).mousemove(function(event){
			if(sw){
				//n.text((x1+event.clientX-x)+":"+(y1+event.clientY-y));
				n.css("left",x1+event.clientX-x);
				n.css("top",y1+event.clientY-y);
			}
		});
		
	};
	$.fn.setBlock.defaults = {
		
	}
})(jQuery);

function isIE(){
	if(window.navigator.userAgent.indexOf("MSIE")>=1 || window.navigator.userAgent.indexOf("Edge")>=1){
		return true; 
	}
	else{
		return false; 
	}
}

//判断移动端
function isMobile(){
	var system ={win:false,mac:false,xll:false};
	var p = navigator.platform;
	system.win = p.indexOf("Win") == 0;
	system.mac = p.indexOf("Mac") == 0;
	system.x11 = (p == "X11") || (p.indexOf("Linux") == 0); 
	if(system.win||system.mac||system.xll){return false;}else{return true;}
}