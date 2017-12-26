---
layout: page
title: 留言板「MESSAGE」
comments: true 
---

<div width="360" height="250" alt="huanying">

	 &nbsp;&nbsp; *☆∵ ▁▂▄▂▁．★∵∴☆．★∵∴<br />
	　∴★◢█████◣* .☆<br />.★ * ☆
	　☆◢████☆██◣．☆<br />了,☆
	&nbsp;　◢■◤....█◥█◣．送你一件毛衣,* ★<br />
	&nbsp;　◥◤∴...██．◥◤∵小心別著涼了！<br />
</div>

<p><h4>hello,轻轻的你来了，你挥一挥衣袖不带走一片云彩，* ☆．∴★∵★ * ☆</h4>     
<P><h4>但是不带走可以，还是要留点啥吧 ︽⊙＿⊙︽ </h4>
<P><h4>这里是你畅所欲言的地方，可以咨询，\(￣︶￣)></h4>
<p><h4>可以交流，可以感叹，可以发飙，可以夸我，还可以打赏呦$$$$$但不可以订外卖 →_→ !</h4>   
<p><h4>要不我会突突你的  ▄︻┻┳═一  ☺ </h4>
<p>
<br/>
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
			title : "刚好遇见你",
			artist : "李玉刚",
			mp3 : "http://omjh2j5h3.bkt.clouddn.com/music/%E6%9D%8E%E7%8E%89%E5%88%9A%20-%20%E5%88%9A%E5%A5%BD%E9%81%87%E8%A7%81%E4%BD%A0.mp3",
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