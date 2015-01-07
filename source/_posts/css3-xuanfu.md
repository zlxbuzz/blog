title: CSS3鼠标悬停图片动画 多种文字动画效果
date: 2014-12-11 17:41:41
categories: css
tags: [css,css3]
---
##HTML代码

	<div&nbsp;class="grid">

	<figure&nbsp;class="effect-lily">

	<img&nbsp;src="img/12.jpg"&nbsp;alt="img12"/>

	<figcaption>

	<div>

	<h2>Nice&nbsp;<span>Lily</span></h2>

	<p>Lily&nbsp;likes&nbsp;to&nbsp;play&nbsp;with&nbsp;crayons&nbsp;and&nbsp;pencils</p>

	</div>

	<a&nbsp;href="#">View&nbsp;more</a>

	</figcaption>

	</figure>

	<figure&nbsp;class="effect-lily">

	<img&nbsp;src="img/1.jpg"&nbsp;alt="img1"/>

	<figcaption>

	<div>

	<h2>Nice&nbsp;<span>Lily</span></h2>

	<p>Lily&nbsp;likes&nbsp;to&nbsp;play&nbsp;with&nbsp;crayons&nbsp;and&nbsp;pencils</p>

	</div>

	<a&nbsp;href="#">View&nbsp;more</a>

	</figcaption>

	</figure>

	</div>


##CSS代码

	figure.effect-lily img {

	max-width: none;

	width: -webkit-calc(100% + 50px);

	width: calc(100% + 50px);

	opacity: 0.7;

	-webkit-transition: opacity 0.35s, -webkit-transform 0.35s;

	transition: opacity 0.35s, transform 0.35s;

	-webkit-transform: translate3d(-40px,0, 0);

	transform: translate3d(-40px,0,0);

	}

	 

	figure.effect-lily figcaption {

	text-align: left;

	}

	 

	figure.effect-lily figcaption > div {

	position: absolute;

	bottom: 0;

	left: 0;

	padding: 2em;

	width: 100%;

	height: 50%;

	}

	 

	figure.effect-lily h2,

	figure.effect-lily p {

	-webkit-transform: translate3d(0,40px,0);

	transform: translate3d(0,40px,0);

	}

	 

	figure.effect-lily h2 {

	-webkit-transition: -webkit-transform 0.35s;

	transition: transform 0.35s;

	}

	 

	figure.effect-lily p {

	color: rgba(255,255,255,0.8);

	opacity: 0;

	-webkit-transition: opacity 0.2s, -webkit-transform 0.35s;

	transition: opacity 0.2s, transform 0.35s;

	}

	 

	figure.effect-lily:hover img,

	figure.effect-lily:hover p {

	opacity: 1;

	}

	 

	figure.effect-lily:hover img,

	figure.effect-lily:hover h2,

	figure.effect-lily:hover p {

	-webkit-transform: translate3d(0,0,0);

	transform: translate3d(0,0,0);

	}

	 

	figure.effect-lily:hover p {

	-webkit-transition-delay: 0.05s;

	transition-delay: 0.05s;

	-webkit-transition-duration: 0.35s;

	transition-duration: 0.35s;

	}

