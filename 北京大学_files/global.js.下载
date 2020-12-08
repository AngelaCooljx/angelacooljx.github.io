// JavaScript Document

function htmlsize(){
	var dw=750;
	var ww=$(window).width();
	var maxw=1920;
	var minw=320;
	if($(window).width()>maxw){ww=maxw;}
	else if($(window).width()<minw){ww=minw;}	
	$("html").css({fontSize:Math.floor((ww/dw)*100)});
}
htmlsize();
$(window).resize(htmlsize);

//header_home
function autoheader(){
	if($(".header").length>0 && $(".header2").length>0 && $(".home").length==0){
		if($(window).scrollTop()>$(".banner_frame").height()-$(".header").height()){
			//$(".header").removeClass("dark").addClass("light");
			$(".header").removeClass("showdiv");
			$(".header2").addClass("showdiv");
		}
		else{
			//$(".header").addClass("dark").removeClass("light");
			$(".header2").removeClass("showdiv");
			$(".header").addClass("showdiv");
		}
	}
}

//nav_page
$(window).on("load",function(){
	if(location.hash!="" && location.hash!=null){
		var h=0;
		if($(window).width()>850){
			h=$(".header").height()-1;
		}
		$(window).scrollTop($(location.hash).offset().top-h);
	}
});


//全局js
$(function(){
htmlsize();
//start


var sto_nav;
$(".nav_main a").hover(
	function(){
		clearTimeout(sto_nav);
		$(".nav_child .item").removeClass("s");
		$(".nav_main a").removeClass("hover");
		var ol=$(this).parents(".block").offset().left;
		var al=$(this).offset().left+$(this).outerWidth()*0.5;
		var fl=al-ol;
		var c=$(this).parents(".block").find(".nav_child").find(".item").eq($(this).index());
		var cl=fl-c.outerWidth()*0.5;
		if(c.find("a").size()==0){c.hide();}
		if(cl<0){
			c.css("left",0);
		}
		else if(cl+c.outerWidth()>$(this).parents(".block").outerWidth()){
			c.css("right",0);
		}
		else{
			c.css("left",cl);
		}
		$(this).addClass("hover");
		c.addClass("s");
	},
	function(){
		sto_nav=setTimeout(function(){
			$(".nav_child .item").removeClass("s");
			$(".nav_main a").removeClass("hover");
		},100);
	}
);
$(".nav_child .item").hover(
	function(){
		clearTimeout(sto_nav);
	},
	function(){
		$(".nav_child .item").removeClass("s");
		$(".nav_main a").removeClass("hover");
	}
);

$(".banner_page1 .text a").click(function(){
	var e=$(this).attr("href").split("#")[1];
	$(window).scrollTop($("#"+e).offset().top-$(".header").height()-1);
	return false;
});

$(".nav_child .item .r a").click(function(){
	var e=$(this).attr("href").split("#")[1];
	$(window).scrollTop($("#"+e).offset().top-$(".header").height()-1);
	return false;
});

if($(".banner_page1 .text .p").length>0){
	var myScroll4 = new IScroll($(".banner_page1 .text .p")[0], {
			scrollX: !false,
			scrollY: false,
			click: true,
			tap: true
	});
	if($(".banner_page1 .text .p .now").length>0){
		myScroll4.scrollToElement($(".banner_page1 .text .p .now")[0]);
	}
}

$(window).scroll(function(){
	autoheader();	
})
autoheader();

//search
$(".header .sc,.header2 .sc,.body_r .navg .sc,.nav_mobile .sc").click(function(){
	showlayer("#search");
	setTimeout(function(){
		$(".search_box .kw").focus();
	},100);
});

//img
var imgdis=[
	".person_detail .content .pic",
	".body_home .banner .child",
	".cas .item .pic",
	".photos .list .item .pic",
	".layer .picbox"
	];
	
	imgdis.forEach(function(item){
		//console.log(item);
		$(item).bind("contextmenu",function(e){
			return false;
		});
})

/*$(document).on('dragstart','img',function(e){
	return false;
})*/

$("img").bind("dragstart",function(){
	return false;
});

//gotop
$(".gotop").click(function(){
	$(".body_b").animate({scrollTop:0},400+$(".body_b").scrollTop()*0.3);
});

autofoot();
$(window).resize(function(){
	autofoot();
})

//header
$("body").mousewheel(function(event, delta, deltaX, deltaY){
	if(deltaY>0){
		
		$(".header").removeClass("lit");
	}
	if(deltaY<0 && $(".body_home").length==0 && ($(".body").outerHeight()+$(".footer").outerHeight()>$(window).height())){
		$(".header").addClass("lit");
	}
});

//header_r
$(".body_r .menu").bind("click",function(event){
	if(!$(this).hasClass("act")){
		$(this).addClass("act");
		$(".body_r .navg").addClass("showdiv");	
	}
	else{
		$(this).removeClass("act");
		$(".body_r .navg").removeClass("showdiv");	
	}
});

//nav_mobile
$(".header .menu").bind("click",function(event){
	$(".nav_mobile").addClass("showdiv");
	event.stopPropagation();
});
$(".nav_mobile").bind("touchmove",function(event){
	event.stopPropagation();
});
$(".nav_mobile .close").bind("click",function(event){
	$(".nav_mobile").removeClass("showdiv");
});
$(".nav_mobile").bind("click",function(event){
	$(".nav_mobile").removeClass("showdiv");
});
$(".nav_mobile .nav_main").bind("click",function(event){
	event.stopPropagation();
});


//select
$(".select").each(function(index, element) {
	var t=$(this);
	if(t.find(".txt").attr("placeholder")){
		t.find(".txt").text(t.find("span").attr("placeholder")).addClass("pldr");
	}
	t.click(function(){
		$(this).find("ul").show();
		t.css("z-index",1);
	});
	/*if(!t.find("ul").hasClass("mCustomScrollbar")){
		t.find("ul").mCustomScrollbar({scrollInertia:250});
	}*/
	t.mouseleave(function(){
		$(this).find("ul").hide();
		t.css("z-index",0);
	});
	t.find("li").click(function(event){
		event.stopPropagation();
		t.find("span").text($(this).text()).removeClass("pldr");
		t.find("input").val($(this).attr("value"));
		t.find("ul").hide();
		t.css("z-index",0);
	});
});




if((navigator.userAgent.indexOf("MSIE 8.0")>-1 || navigator.userAgent.indexOf("MSIE 9.0")>-1) && getCookie("browser_tip")!="1"){
	$("body").append("<div class='browser_tip' style='position:fixed;left:0;bottom:-100px;right:0;height:100px;line-height:100px;color:#fff;font-size:16px;text-align:center;background:#94070a;box-shadow:0 0 15px rgba(0,0,0,0.3)'><b style='font-weight:bold;margin:0 5px;font-size:20px;'>您的浏览器版本过低！</b>可能无法完整浏览所有内容，建议您使用<b style='font-weight:bold;margin:0 8px;font-size:20px;'>主流浏览器的最新版本</b>以获得最佳浏览体验！<a class='a1' style='text-decoration:underline;margin-left:20px;font-style:italic;'>知道了</a><a href='https://www.baidu.com/s?wd=浏览器' target='_blank' style='text-decoration:underline;margin-left:20px;font-style:italic;'>获取浏览器</a><a class='a2' style='text-decoration:underline;margin-left:20px;font-style:italic;'>不再提示</a></div>");
	$(".browser_tip").animate({bottom:0},1000);
	$(".browser_tip .a1").click(function(){
		$(".browser_tip").animate({bottom:-100},1000,function(){$(".browser_tip").remove();});
	});
	$(".browser_tip .a2").click(function(){
		setCookie("browser_tip","1");
		$(".browser_tip").animate({bottom:-100},1000,function(){$(".browser_tip").remove();});
	});
}


$("video").each(function(index, element) {
	$(this).bind("play",function(){			
		if($(".playing").length>0 && !$(this).hasClass("playing")){
			var v=$(".playing")[0];
			v.pause();
			$(".playing").removeClass("playing");
		}
		$(this).addClass("playing");
	});
});

//end
});