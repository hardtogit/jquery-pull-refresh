$.fn.extend({
    refresh: function(option) {
        var el = $(this);
        var defaults = {
        	height:60,//设置触发下拉刷新的距离；
        	loading_text:$('.loading_text'),//设置文字容器；
        	loading_icon:$('.loading_icon'),//设置加载icon的容器；
        	coefficient:0.6,//阻尼系数；注，阻尼系数越小，越难触发。
        	pullFunction:function(){},//下拉刷新请求数据函数；
        }
        var settings = $.extend(defaults, option || {}); //init
        console.log(settings)
            var _hasPhone = navigator.userAgent.match(/(iPhone|iPod|Android|ios)/i);
            var height=settings.height;
            var className="loading_icon";          
            var _hasTouch = 'ontouchstart' in window;
            var _pulldownConfig = { normalStatus: "下拉即可刷新", maxStatus: "松开立即刷新", releaseStatus: "正在加载…" };
            var _start = 0,_end = 0;          
            var _TransitionObj = {
                translate: function (height) {
                    el.css({ "-webkit-transform": "translate(0," + height + "px)", "transform": "translate(0," + height + "px)" });
                },
                translitionTime: function (time) {
                    el.css({ "-webkit-transition": "all " + time + "s", "transition": "all " + time + "s" });
                },
                goDefault: function () {
                    _TransitionObj.translitionTime(0.5);
                    _TransitionObj.translate(0);
                }
            };
            var _bindTouchEvents = function () {
                el.bind("touchstart", _touchstartHandler);
                el.bind("touchmove", _touchmoveHandler);
                el.bind("touchend", _touchendHandler);
            };
            var _touchstartHandler = function (e) {            	
                settings.loading_icon.removeClass(className);
                var even = typeof event == "undefined" ? e : event;
                //保存当前鼠标Y坐标
                _start = _hasTouch ? even.touches[0].pageY : even.pageY;
                if (el.scrollTop() > 0) {
                    console.log(el.scrollTop());
                    //消除滑块动画时间
                    _TransitionObj.translitionTime(0);
                }
            };
            var changeHeight;
            var _touchmoveHandler = function (e) {  
             	if($(document).scrollTop()>=10){
             		return
             	}
             	changeHeight=_end - _start;
                var even = typeof event == "undefined" ? e : event;
                //保存当前鼠标Y坐标
                _end = _hasTouch ? even.touches[0].pageY : even.pageY;
                if (changeHeight<0||changeHeight>200){
                	return
                }
                if (changeHeight*settings.coefficient > height) {
                    settings.loading_text.html(_pulldownConfig.maxStatus);
                } else {
                    settings.loading_text.html(_pulldownConfig.normalStatus);
                }
                even.preventDefault();
                //消除滑块动画时间
                _TransitionObj.translitionTime(0); 
                _TransitionObj.translate(changeHeight*settings.coefficient);
            };
            var back=function(){
            	_TransitionObj.translate(0)
            }
            var _touchendHandler = function (e) {
            	if($(document).scrollTop()>0){
             		return
             	}
                //判断滑动距离是否大于等于指定值
                if (changeHeight*settings.coefficient>= height) {
                    settings.loading_icon.addClass(className);
                    //设置滑块回弹时间
                    _TransitionObj.translitionTime(1);
                    
                    //设置刷新时的文字
                    settings.loading_text.html(_pulldownConfig.releaseStatus);
                    //保留提示部分
                  	_TransitionObj.translate(40);
                    //执行回调函数
                   settings.pullFunction(3000,function(){ _TransitionObj.translate(0)})
                    
                 
                } else {
                    //返回初始状态
                    _TransitionObj.goDefault();
                }
            }
            _bindTouchEvents();
       }
  })
