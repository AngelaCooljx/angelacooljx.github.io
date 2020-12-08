// JavaScript Document
var sw=1,ww,wh,step=0;
var dst=-1,dst1=-1;


function autowindow(){
	ww=$(window).width();
	wh=$(window).height();
	//$("body").height(wh);
	if($(window).width()>=850){		
		$(".screen").height("100%");
		$(".screen").width(ww);
		$(".body_scroll").width(ww*$(".screen").length);
		$(".body_r").scrollTop(0);
		$(".body_scroll").css({left:step*ww*-1});
	}
	else{
		$(".screen").height("auto");
		$(".screen").width("auto");
		$(".body_scroll").width("auto");
		$(".body_scroll").css({left:0});
	}
	
	
	$(".screen").eq(step).addClass("showdiv");
	$(".nav_b .item").eq(step).addClass("now");
	
	if(sw && $(".screen").length>0 && $(window).width()>=1000){
		$(".body_scroll").stop().animate({left:step*ww*-1},1300,"easeInOutQuart",function(){
			sw=1;
		});
	}
	/*$(".autodiv").each(function(){
		autodiv($(this));
	});*/
}

/*
$(".gotop").click(function(){
	sw=0;
	$(".body_scroll").stop().animate({left:0},1000,"easeInOutQuart",function(){
		sw=1;
	});
	step=0;
	$(".nav_b .item").removeClass("now");
	$(".nav_b .item").eq(step).addClass("now");
});
*/

$(window).scroll(function(){
	$(".screen,.special").each(function(index, element) {
  	if($(window).scrollLeft()>=$(this).offset().left){
			step=index;
			$(".nav_b .item").removeClass("now");
			$(".nav_b .item").eq(step).addClass("now");
			}
  });
});

/*function autodiv(e){
	$(e).css({width:ww/$(e).attr("h")*$(e).attr("w"),height:"100%"});
}*/

$(function(){
	autowindow();
	$(window).resize();
	
	$(".home2 .list").mousewheel(function(event, delta, deltaX, deltaY){
		event.stopPropagation();
	});
	
	$(".body_r").mousewheel(function(event, delta, deltaX, deltaY){
		if($(window).width()>=1000){
			gowheel(delta);
		}
		//event.stopPropagation();
		//event.preventDefault();
	});
	
	$(".nav_b .item").click(function(){
		sw=0;
		step=$(this).index();		
		$(".body_scroll").stop().animate({left:ww*step*-1},1300,"easeInOutQuart",function(){
			showscreen(step);
			sw=1;
		});
		$(".nav_b .item").removeClass("now");
		$(".nav_b .item").eq(step).addClass("now");
		if(step==2){
			$(".nav_b").addClass("w");
			$(".ll").addClass("w");
		}
		else{
			$(".nav_b").removeClass("w");
			$(".ll").removeClass("w");
		}
		if((step+1)==$(".screen").length){
			$(".body_r .arr").addClass("h");
		}
		else{
			$(".body_r .arr").removeClass("h");
		}
		
	});
	$(".body_r .arr").click(function(){
		$(".nav_b .list .item.now").next().click();
	});
});

$(window).resize(function(){
	autowindow();
});

function gowheel(delta){
	if(sw && $(".screen").length>0){
		var sch=0;
		var isgo=0;
		/*$(".screen").eq(step).children().each(function(){
			if($(this).css("position")!="absolute"){
				sch+=$(this).outerWidth();
			}
		});
		if(sch>$(".screen").eq(step).outerWidth()){
			$(".screen").eq(step).attr("unlock",0);
			if(dst<0){
				dst=$(".screen").eq(step).scrollLeft();
			}			
			if(delta<0){
				dst=dst+delta*80*-1;
			}
			else{
				dst=dst+delta*90*-1;
			}
			
			if(sch==$(".screen").eq(step).outerWidth()+$(".screen").eq(step).scrollLeft() && delta<0){
				$(".screen").eq(step).attr("unlock",1);
			}
			if($(".screen").eq(step).scrollLeft()==0 && delta>0){
				$(".screen").eq(step).attr("unlock",1);
			}
			if(dst!==$(".screen").eq(step).scrollLeft()){
				$(".screen").eq(step).stop().animate({scrollLeft:dst},500,"easeOutQuad",function(){dst=$(".screen").eq(step).scrollLeft();});
			}
		}*/
		
		if($(".screen").eq(step).attr("unlock")!="0"){
			dst=-1;
			if(delta<0){
				if($(".screen").eq(step+1).length>0){
					sw=0;
					step++;
					isgo=1;					
				}
				else{					
					//sw=0;
					//$(".ll").click();
					/*if($(".body_b").hasClass("showdiv")){
						$(".body_r").removeClass("showdiv");						
					}
					else{
						$(".ll").click();
						//$(".body_b").css("z-index",2);
						//$(".body_r").css("z-index",1);
					}*/
					//setTimeout(function(){
						//$(".bb").click();
						//$(".ll").click();
						//sw=1;
					//},1400);
				}
			}
			else{
				if($(".screen").eq(step-1).length>0 && step>0){
					sw=0;
					step--;
					isgo=1;
				}
				else{
					//sw=0;
					//$(".body_r").removeClass("showdiv");
					//$(".rr").addClass("showdiv");
					//$(".ll").click();
					//setTimeout(function(){
						//$(".home").addClass("showdiv");
						//sw=1;
					//},1400);
				}
			}
			
			if(isgo==1){
				$(".body_scroll").stop().animate({left:ww*step*-1},1300,"easeInOutQuart",function(){
					showscreen(step);
					sw=1;
				});
				$(".nav_b .item").removeClass("now");
				$(".nav_b .item").eq(step).addClass("now");
				if(step==2){
					$(".nav_b").addClass("w");
					$(".ll").addClass("w");
				}
				else{
					$(".nav_b").removeClass("w");
					$(".ll").removeClass("w");
				}
				
				if(step+1==$(".screen").length){
					$(".body_r .arr").hide();
				}
				else{
					$(".body_r .arr").show();
				}
			}
		}
	}
}
function showscreen(i){
	$(".screen").removeClass("showdiv");
	$(".screen").eq(i).addClass("showdiv");
	
	if(i==0){
		//$(".home1 .td strong").each(function(index, element) {
			//shownum($(this),3000);
		//});
	}
	
	//$(".nav_b .item").removeClass("now");
	//$(".nav_b .item").eq(i-1).addClass("now");
	
	
}