# jquery-pull-refresh
this is a simple demo for pull-refresh
html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no,minimal-ui" />
		
		<title></title>
		<script src="js/jquery-1.11.2.min.js" type="text/javascript" charset="utf-8"></script>
		<script src="js/pullRefresh.js" type="text/javascript" charset="utf-8"></script>
		<style type="text/css">
			 body {
            font-family: 'Helvetica Neue', 'Helvetica Neue', Helvetica, Arial, 'Hiragino Sans GB', 'Microsoft Yahei', sans-serif;
            color: #4C4747;
        }

        body, div, p,ul {
            padding: 0px;
            margin: 0px;
        }

        .pull_drawing {
            position: absolute;
            top: -58px;
            width: 100%;
            padding-top: 22px;        
            background-size: 172px 22px;
            height: 35px;
            line-height: 35px;
            text-align: center;
        }

        .loading_icon {
            position: absolute;
            margin-left: -25px;
            margin-top: 8px;
            width: 14px;
            height: 14px;
            border: 2px solid #54a5d4;
            border-radius: 50%;
            -webkit-animation: roll 1s linear infinite;
            animation: roll 1s linear infinite;
            clip: rect(0,15px,18px,0);
            line-height: 35px;
            text-align: center;
        }

        @-webkit-keyframes roll {
            0% {
                -webkit-transform: rotate(0deg);
            }

            100% {
                -webkit-transform: rotate(360deg);
            }
        }

        @keyframes roll {
            0% {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }
        .main {
            width: 100%;
            /*border: solid 1px #0094ff;*/
        }
        .textbg {
            width: 100%;
            line-height: 30px;
            background-color: #F2F2F2;
            font-size: 17px;
            font-family: 'Adobe Garamond Pro';
        }
        .textbg p{
            text-indent: 30px;
        }
        .nav{
        	background-color: #fff;
        	position: relative;
            z-index: 10;
            padding: 6px 10px;
            text-align: center
        }
        #data-list li{
        	padding: 4px 10px;
        	border-bottom: 1px solid #ddd;
        }
		</style>
	</head>
	<body style="background-color: #f5f5f5">
	    <div class="nav">
	    	我是导航栏
	    </div>
    <div id="main" class="main">
        <p class="pull_drawing">
            <i class="loading_icon"></i>
            <span class="loading_text">下拉刷新中</span>
        </p>
        <div class="textbg">
          <ul id="data-list">
          	<li>列表item</li>
            <li>列表item</li>
            <li>列表item</li>
            <li>列表item</li>
            <li>列表item</li>
            <li>列表item</li>
            <li>列表item</li>
            <li>列表item</li>
          </ul>       
        </div>
    </div>
    <script type="text/javascript">
    	$('#main').refresh({
    		pullFunction:function(ms,callback){
    			setTimeout(function(){
    				for(var i=0;i<5;i++){
    					$('#data-list').append('<li>我是新增的item</li>')
    				}
 				callback();
    				
    			},ms)
    		},
    	})
    </script>
</body>
</html>
