---
layout: page
title: 留言板「MESSAGE」
comments: true 
---
<div width="360" height="250" alt="huanying">

  *☆∵ ▁▂▄▂▁．★∵∴☆．★∵∴<br />
∴★◢█████◣* ☆．∴★∵★ * ☆<br />
 ☆◢████☆██◣．∴天氣冷了,☆<br />
◢■◤█████◥█◣．送你一件毛衣,* ★<br />
◥◤∴█████．◥◤∵小心別著涼了！<br />
</div>

<p><h4>hello,轻轻的你来了，你挥一挥衣袖不带走一片云彩，* ☆．∴★∵★ * ☆</h4>     
<P><h4>但是不带走可以，还是要留点啥吧 ︽⊙＿⊙︽ </h4>
<P><h4>这里是你畅所欲言的地方，可以咨询，\(￣︶￣)></h4>
<p><h4>可以交流，可以感叹，可以发飙，可以夸我，还可以打赏呦$$$$$但不可以订外卖 →_→ !</h4>   
<p><h4>要不我会突突你的  ▄︻┻┳═一  ☺ </h4>
<p>
<br /> 
{% include dashang.html %}
	<div id="QPlayer" class="QPlayer">
		<div id="pContent">
			<div id="player">
				<span class="cover"></span>
				<div class="ctrl">
					<div class="musicTag marquee">
						<strong>Title</strong> <span> - </span> <span class="artist">Artist</span>
					</div>
					<div class="progress">
						<div class="timer left">0:00</div>
						<div class="contr">
							<div class="rewind icon"></div>
							<div class="playback icon"></div>
							<div class="fastforward icon"></div>
						</div>
						<div class="right">
							<div class="liebiao icon"></div>
						</div>
					</div>
				</div>
			</div>
			<div class="ssBtn">
				<div class="adf"></div>
			</div>
		</div>
		<ol id="playlist"></ol>
</div>
<script src="/js/jquery.min.js"></script>
<script src="/js/jquery.marquee.min.js"></script>

<script>
	var playlist = [
			{
			title : "19岁",
			artist : "赵雷",
			mp3 : "http://p22h841lq.bkt.clouddn.com/%E5%89%8D%E5%86%B2%20-%2019%E5%B2%81%EF%BC%88Cover%20%E8%B5%B5%E9%9B%B7%EF%BC%89.mp3",
			cover : "http://p4.music.126.net/Nn8kTtc14uWJw_UWbEc5mg==/7909886650478099.jpg?param=106x106",
			},
			{
			title : "成都",
			artist : "赵雷",
			mp3 : "http://p22h841lq.bkt.clouddn.com/%E8%B5%B5%E9%9B%B7%20-%20%E6%88%90%E9%83%BD.mp3",
			cover : "http://p4.music.126.net/Nn8kTtc14uWJw_UWbEc5mg==/7909886650478099.jpg?param=106x106",
			},
			{
			title : "山丘",
			artist : "李宗盛",
			mp3 : "http://p22h841lq.bkt.clouddn.com/%E6%9D%8E%E5%AE%97%E7%9B%9B%20-%20%E5%B1%B1%E4%B8%98%20%28Live%29.mp3",
			cover : "http://p4.music.126.net/Nn8kTtc14uWJw_UWbEc5mg==/7909886650478099.jpg?param=106x106",
			},
			{
			title : "花旦",
			artist : "周华健",
			mp3 : "http://p22h841lq.bkt.clouddn.com/%E5%91%A8%E5%8D%8E%E5%81%A5-%E8%8A%B1%E6%97%A6.mp3",
			cover : "http://p4.music.126.net/Nn8kTtc14uWJw_UWbEc5mg==/7909886650478099.jpg?param=106x106",
			}
			];
	var isRotate = true;
	var autoplay = true;

</script>
<script src="/js/player.js"></script>
<script>
	function bgChange() {
		var lis = $('.lib');
		for ( var i = 0; i < lis.length; i += 2)
			lis[i].style.background = 'rgba(246, 246, 246, 0.5)';
		}
	window.onload = bgChange;
</script>

<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title></title>
<link rel="stylesheet" href="/css/player.css">	
<script>
	myVid = document.getElementById("audio1");
	function setHalfVolume() {
		myVid.volume = 0.2;
	}
</script>