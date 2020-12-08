$(function(){
    $.ajax({
        url : '/dat/recentList.xml',
        error : function(dat) {
        },
        success : function(dat) {
            var recentList = $(dat).find('Notice');
            if(recentList.size() > 0){
                var _recentListHtml = [];
                var _tr = '<div class="item"><a target="_blank" href="__HREF__">\
                            <div class="h">__TITLE__</div>\
                            <div class="date"><span>__DATE__</span></div>\
                            </a> \
                        </div>';
                recentList.each(function(index){
                    if(index > 2){
                        return false;
                    }
                    var _this = $(this);
                    _recentListHtml.push(_tr.replace(/(__HREF__|__TITLE__|__DATE__)/gi, function ($a, $b) {
                        return {
                            "__HREF__": '/notice/detail.html?aid=' + _this.find('ID').text(),
                            "__TITLE__": _this.find('Title').text(),
                            "__DATE__": _this.find('PubDate').text(),
                        }[$b];
                    }));
                })
                $('#tzggList').html(_recentListHtml.join(''));
            }else{
                // $('.notice .list').html("<div class='empty-data' style='text-align:center;font-size:18px;'><b>暂无数据</b></div>");
            }
        }
    });
    $.ajax({
        url : '/dat/recentStatement.xml',
        error : function(dat) {
        },
        success : function(dat) {
            var recentStatementList = $(dat).find('Notice');
            if(recentStatementList.size() > 0){
                var _recentStatementListHtml = [];
                var _tr = '<div class="item"><a target="_blank" href="__HREF__">\
                            <div class="h">__TITLE__</div>\
                            <div class="date"><span>__DATE__</span></div>\
                            </a> \
                        </div>';
                recentStatementList.each(function(index){
                    if(index > 2){
                        return false;
                    }
                    var _this = $(this);
                    _recentStatementListHtml.push(_tr.replace(/(__HREF__|__TITLE__|__DATE__)/gi, function ($a, $b) {
                        return {
                            "__HREF__": '/notice/detail.html?aid=' + _this.find('ID').text(),
                            "__TITLE__": _this.find('Title').text(),
                            "__DATE__": _this.find('PubDate').text(),
                        }[$b];
                    }));
                })
                $('#bdsmList').html(_recentStatementListHtml.join(''));
            }else{
                // $('.notice .list').html("<div class='empty-data' style='text-align:center;font-size:18px;'><b>暂无数据</b></div>");
            }
        }
    });
    $.ajax({
        url : '/dat/topNews.json',
        error : function(dat) {
        },
        success : function(dat) {
            var _htmlA = [];
            var _htmlB = [];
            var _tpl = '<div class="item"><a target="_blank" href="__href__">\
                    <div class="text">\
                        <div class="h">__title__</div>\
                        <div class="date" style="display:none;"></div>\
                    </div></a>\
                </div>';
            if(dat.success){
                $.each(dat.data, function(index){
                    if(index < 4){
                        _htmlA.push(_tpl.replace(/(__href__|__title__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__title__": dat.data[index].title
                            }[$b];
                        }));
                    }else{
                        _htmlB.push(_tpl.replace(/(__href__|__title__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__title__": dat.data[index].title
                            }[$b];
                        }));
                    }
                })
                $('.home5 .content .list:eq(0) .box').html(_htmlA.join(''));
                $('.home5 .content .list:eq(1) .box').html(_htmlB.join(''));
            }
        }
    });
    $.ajax({
        url : '/dat/imgNews.json',
        error : function(dat) {
        },
        success : function(dat) {
            var _htmlA = [];
            var _htmlB = [];
            var _tplA = '<div class="pic">\
                            <div class="img" style="background-image:url(__img__);"><a target="_blank" href="__href__"></a></div>\
                            <div class="video">\
                                <video controls preload="auto" poster="__img__" webkit-playsinline="" playsinline="" x5-playsinline="" x-webkit-airplay="allow">\
                                    <source src="__video__" type="video/mp4" />\
                                </video>\
                                <span class="close">关闭</span>\
                            </div>\
                        </div>\
                        <div class="text">\
                            <a target="_blank" href="__href__">\
                                <div class="h">__title__</div>\
                                <div class="date" style="display:none;"></div>\
                            </a>\
                            <span class="v">&#xe67c;</span>\
                        </div>';
            var _tplB = '<div class="pic"><div class="img" style="background-image:url(__img__);"><a target="_blank" href="__href__"></a></div></div>\
                        <div class="text">\
                            <a target="_blank" href="__href__">\
                                <div class="h">__title__</div>\
                                <div class="date" style="display:none;"></div>\
                            </a>\
                        </div>';
            if(dat.success){
                $.each(dat.data, function(index){
                    var _tpl = dat.data[index].video ? _tplA : _tplB;
                    if(index == 0){
                        $('.home5 .content .list:eq(0) .ptbox .inner').html(_tpl.replace(/(__href__|__img__|__title__|__video__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__img__": '/' + dat.data[index].pic,
                                "__title__": dat.data[index].title,
                                "__video__":dat.data[index].video
                            }[$b];
                        }));
                    }else{
                        $('.home5 .content .list:eq(1) .ptbox .inner').html(_tpl.replace(/(__href__|__img__|__title__|__video__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__img__": '/' + dat.data[index].pic,
                                "__title__": dat.data[index].title,
                                "__video__":dat.data[index].video
                            }[$b];
                        }));
                    }
                })
                $(".home5 .ptbox").each(function(index, element) {
                    var t=$(this);
                    $(this).find(".v").click(function(){
                        t.addClass("act");
                        var v=t.find("video")[0];
                        v.play();
                    });
                    $(this).find(".close").click(function(){
                        t.removeClass("act");
                        var v=t.find("video")[0];
                        v.pause();
                    });
                });
            }
        }
    });
    $.ajax({
        url : '/dat/teachResearchNews.json',
        error : function(dat) {

        },
        success : function(dat) {
            if(dat.success){
                $.each(dat.data, function(index){
                    // $('.home6 .part1 .pic a,.home6 .part1 .text a').attr('href', dat.data[index].url);
                    $('.home6 .part1 .text a').attr('href', dat.data[index].url);
                    $('.home6 .part1 .text .inner .h a').html(dat.data[index].title);
                    $('.home6 .part1 .text .inner .p').html(dat.data[index].summary);
                    $('.home6 .part1 .text .l img').attr('src', '/' + dat.data[index].pic);
                })
                
            }
        }
    });
    /*$.ajax({
        url : '/dat/teachResearchImg.json',
        error : function(dat) {
        },
        success : function(dat) {
            if(dat.success){
                $('.home6 .part1 .text .l img').attr('src', '/' + dat.data);
            }
        }
    });*/
    $.ajax({
        url : '/dat/mediaPKU.json',
        error : function(dat) {
        },
        success : function(dat) {
            var _htmlA = [];
            var _tpl = '<div class="item">\
                            <a target="_blank" href="__href__">\
                                <div class="pic"><span>__source__</span></div>\
                                <div class="h">__title__</div>\
                            </a>\
                        </div>';
            if(dat.success){
                $.each(dat.data, function(index){
                    _htmlA.push(_tpl.replace(/(__href__|__source__|__title__)/gi, function ($a, $b) {
                        return {
                            "__href__": dat.data[index].url,
                            "__source__": dat.data[index].source,
                            "__title__": dat.data[index].title
                        }[$b];
                    }));
                })
                $('.home8 .r .list').html(_htmlA.join(''));
            }
        }
    });
    $.ajax({
        url : '/dat/pkuPeople.json',
        error : function(dat) {
        },
        success : function(dat) {
            var _htmlA = [];
            var _htmlB = [];
            var _tpl = '<a href="__href__" target="_blank"><img src="__img__"></a>\
                        <div class="mask"><a href="__href__" target="_blank">__title__</a></div>';
            if(dat.success){
                $.each(dat.data, function(index){
                    if(index == 0){
                        $('.home6 .part2 .d').eq(1).find('.pic').html(_tpl.replace(/(__href__|__img__|__title__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__img__": '/' + dat.data[index].pic,
                                "__title__": dat.data[index].title
                            }[$b];
                        }));
                    }else{
                        $('.home6 .part2 .d').eq(0).find('.pic').html(_tpl.replace(/(__href__|__img__|__title__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__img__": '/' + dat.data[index].pic,
                                "__title__": dat.data[index].title
                            }[$b];
                        }));
                    }
                })
            }
            var _htmlA = [];
            var _htmlB = [];
            var _tplA = '<div class="pic">\
                            <div class="img"><a target="_blank" href="__href__"><img src="__img__"></a></div>\
                            <div class="video">\
                                <video controls preload="auto" poster="__img__" webkit-playsinline="" playsinline="" x5-playsinline="" x-webkit-airplay="allow">\
                                    <source src="__video__" type="video/mp4" />\
                                </video>\
                                <span class="close">关闭</span>\
                            </div>\
                        </div>\
                        <div class="text">\
                            <a target="_blank" href="__href__">\
                                <div class="h">__title__</div>\
                            </a>\
                            <span class="v">&#xe67c;</span>\
                        </div>';
            var _tplB = '<div class="pic"><div class="img"><a target="_blank" href="__href__"><img src="__img__" alt=""></a></div></div>\
                        <div class="text">\
                            <a target="_blank" href="__href__">\
                                <div class="h">__title__</div>\
                            </a>\
                        </div>';
            if(dat.success){
                $.each(dat.data, function(index){
                    // var _tpl = dat.data[index].video ? _tplA : _tplB;
                    var _tpl = _tplB;
                    if(index == 0){
                        $('.home6 .part2 .d:eq(1) .ptbox .inner').html(_tpl.replace(/(__href__|__img__|__title__|__video__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__img__": '/' + dat.data[index].pic,
                                "__title__": dat.data[index].title,
                                "__video__":dat.data[index].video
                            }[$b];
                        }));
                    }else{
                        $('.home6 .part2 .d:eq(0) .ptbox .inner').html(_tpl.replace(/(__href__|__img__|__title__|__video__)/gi, function ($a, $b) {
                            return {
                                "__href__": dat.data[index].url,
                                "__img__": '/' + dat.data[index].pic,
                                "__title__": dat.data[index].title,
                                "__video__":dat.data[index].video
                            }[$b];
                        }));
                    }
                })
                $(".home6 .ptbox").each(function(index, element) {
                    var t=$(this);
                    $(this).find(".v").click(function(){
                        t.addClass("act");
                        var v=t.find("video")[0];
                        v.play();
                    });
                    $(this).find(".close").click(function(){
                        t.removeClass("act");
                        var v=t.find("video")[0];
                        v.pause();
                    });
                });
            }
        }
    });
    $.ajax({
        url : '/dat/hotTopics.json',
        error : function(dat) {
        },
        success : function(dat) {
            var _htmlA = [];
            var _tpl = '<div class="item">\
                            <div class="pic" style="background-image:url(__img__);"></div>\
                            <div class="tit">\
                                <div class="h">__title__</div>\
                            </div>\
                            <span class="more1">查看更多</span>\
                            <a href="__href__" target="_blank"></a>\
                        </div>';
            if(dat.success){
                $.each(dat.data.reverse(), function(index){
                    _htmlA.push(_tpl.replace(/(__href__|__img__|__title__)/gi, function ($a, $b) {
                        return {
                            "__href__": dat.data[index].url,
                            "__img__": '/' + dat.data[index].pic,
                            "__title__": dat.data[index].title
                        }[$b];
                    }));
                })
                $('.home9 .list').html(_htmlA.join(''));
            }
        }
    });

})