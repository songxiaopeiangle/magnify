<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>放大镜</title>
	<style type="text/css">
		*{
			margin: 0;
			padding: 0;
		}
		#smallImg{
			width: 300px;
			height: 300px;
			position: relative;
			float: left;
		}
		#smallImg img{
			width: 300px;
			height: 300px;

		}
		#lay{
			
			background: #fff;
			position: absolute;
			left: 0;
			top: 0;
			opacity: 0.6;
			filter: alpha(opacity=60);
			display: none;
		}
		#bigImg{
			float: left;
			width: 300px;
			height: 300px;
			overflow: hidden;
			display: none;
		}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var scale = 2;
			var smallBox = $("smallImg");
			var layBox = $("lay");
			var bigBox = $("bigImg");
			var bigImg = bigBox.children[0];
			layBox.style.width = parseInt(smallBox.offsetWidth / scale) + "px";//在小图层css里不设置宽度和高度的时候，相对大图进行缩小4倍
			//console.log(layBox.style.width);
			layBox.style.height = parseInt(smallBox.offsetHeight /scale) + "px";
			bigImg.style.width = smallBox.offsetWidth * scale + "px";//不是laybox的偏移
			bigImg.style.height = smallBox.offsetHeight * scale + "px";
			console.log(bigImg);

			smallBox.onmouseover = function(){
				bigBox.style.display = "block";
				layBox.style.display = "block";
				

			}
			smallBox.onmouseout = function(){
				bigBox.style.display = "none";
				layBox.style.display = "none";
				

			}
			smallBox.onmousemove = function(e){
				e = e || event;
				
				
				var x = e.clientX - layBox.offsetWidth / 2;//不能加px
				var y = e.clientY - layBox.offsetHeight /2;
				
				layBox.style.width = parseInt(smallBox.offsetWidth / scale) + "px";//在小图层css里不设置宽度和高度的时候，相对大图进行缩小4倍
				//console.log(layBox.style.width);
				layBox.style.height = parseInt(smallBox.offsetHeight /scale) + "px";
				//console.log(layBox.style.height);
				//layBox.style.left = x + "px";
				//layBox.style.top = y + "px";
				//如何移中心点
				layBox.style.left = x + "px";
				layBox.style.top = y + "px";
				//中心点确定后，检测边界
				if(layBox.offsetLeft <= 0){
					x = 0;
				}
				if(layBox.offsetTop <= 0){
					y = 0;
				}
				if(layBox.offsetLeft >= smallBox.offsetWidth - layBox.offsetWidth){
					x = smallBox.offsetWidth - layBox.offsetWidth;
				}
				if(layBox.offsetTop >= smallBox.offsetHeight - layBox.offsetHeight){
					y = smallBox.offsetHeight - layBox.offsetHeight;
				}
				layBox.style.left = x + "px";
				layBox.style.top = y + "px";

				var Left = layBox.offsetLeft * scale;
				var Top = layBox.offsetTop * scale;
				bigImg.style.marginLeft = -1 * Left + "px";
				bigImg.style.marginTop = -1 * Top + "px";

			}
			function $(id){
				return document.getElementById(id);
			}
		}
	</script>
</head>
<body>
	<div id="smallImg">
		<img src="1.jpg" />
		<div id="lay"></div>
	</div>
	<div id="bigImg">
		<img src="1.jpg" />
	</div>
</body>
</html>
