【DOM】

- [DOM简介](#dom简介)
- [获取元素](#获取元素)
	- [ID获取元素](#id获取元素)
	- [Tag获取元素](#tag获取元素)
	- [H5新增方法获取元素](#h5新增方法获取元素)
	- [获取特殊元素（body和html）](#获取特殊元素body和html)
- [事件基础](#事件基础)
	- [事件三要素](#事件三要素)
	- [执行事件的步骤](#执行事件的步骤)
- [操作元素](#操作元素)
	- [改变元素内容](#改变元素内容)
	- [innerText和innerHTML的区别](#innertext和innerhtml的区别)
	- [修改元素属性](#修改元素属性)
	- [案例：分时显示不同图片，不同问候语](#案例分时显示不同图片不同问候语)
	- [修改表单属性](#修改表单属性)
	- [案例：模仿京东登陆页面显示明文密码](#案例模仿京东登陆页面显示明文密码)
	- [修改元素的样式属性](#修改元素的样式属性)
	- [案例：淘宝点击关闭二维码](#案例淘宝点击关闭二维码)
	- [案例：循环精灵图背景](#案例循环精灵图背景)
	- [案例：显示隐藏文本框](#案例显示隐藏文本框)
	- [使用ClassName修改样式属性](#使用classname修改样式属性)
	- [案例：密码框格式提示错误信息](#案例密码框格式提示错误信息)
	- [操作元素总结](#操作元素总结)
	- [排他思想（算法）](#排他思想算法)
	- [案例：百度换肤效果](#案例百度换肤效果)
	- [案例：表格悬浮经过变色](#案例表格悬浮经过变色)
	- [案例：表单全选取消](#案例表单全选取消)
	- [自定义属性的操作](#自定义属性的操作)
	- [案例：tab栏切换（重点★）](#案例tab栏切换重点)
	- [H5自定义属性](#h5自定义属性)
- [节点操作](#节点操作)
	- [获取元素方式](#获取元素方式)
	- [节点概述](#节点概述)
	- [节点层级](#节点层级)
	- [获取first/last子元素](#获取firstlast子元素)
	- [案例：新浪下拉菜单](#案例新浪下拉菜单)
	- [节点操作：兄弟节点](#节点操作兄弟节点)
	- [节点操作：创建/添加节点](#节点操作创建添加节点)
		- [创建节点](#创建节点)
		- [添加节点](#添加节点)
	- [案例：简单版发布留言](#案例简单版发布留言)
	- [节点操作：删除节点](#节点操作删除节点)
	- [案例：删除留言案例](#案例删除留言案例)
	- [节点操作：复制节点](#节点操作复制节点)
	- [案例：动态生成表格](#案例动态生成表格)
	- [三种动态创建元素的区别](#三种动态创建元素的区别)
	- [DOM重点核心](#dom重点核心)

# DOM简介

文档对象模型 Document Object Model
- 是W3C组织推荐的处理可扩展标记语言（HTML/XML）的标准编程接口
- 提供了一系列的DOM接口，可改变网页的内容、结构和样式

DOM树
- 文档 > 根元素 > 元素 > ... > 元素 > 属性
- 文档 document 一个页面就是一个文档
- 元素 element 页面中所有标签都是元素
- 节点 node 网页中的所有内容（标签、属性、文本、注释等）都是节点
> DOM把以上内容都看作**对象**


# 获取元素

DOM在实际开发中主要用来操作元素，获取页面元素的方法：
- ID获取
- TAG获取
- H5新增方法获取
- 特殊元素获取

## ID获取元素

getElementById(ID) 可以获取带有ID的元素对象

```html
<div id="time">2019-9-9</div>
<script>
	// 因为文档页面从上往下加载，所以先有标签，再有JS
	// getElementById() 注意是驼峰命名法
	// 参数 id 是字符串，大小写敏感
	// 返回的是一个元素对象

	var time = document.getElementById('time');
	console.log(time); //<div id="time">2019-9-9</div>
	console.log(typeof time); //object

	// console.dir 打印返回的元素对象,更好的查看里面的属性和方法
	console.dir(time);

	// 输出结果为:
	// div#time
	// accessKey: ""
	// align: ""
	// ariaAtomic: null
	// ariaAutoComplete: null
	// ariaBusy: null
	// ariaChecked: null
	// ariaColCount: null
	// ariaColIndex: null
	// ariaColSpan: null
	// ariaCurrent: null
	// ariaDescription: null
	// ariaDisabled: null
	// ariaExpanded: null
	// ariaHasPopup: null
	// ...反正很长很多
</script>
```



## Tag获取元素

getElementsByTagName() 返回带有指定标签名的对象集合

注意:
1. 因为得到的是一个对象的集合,所以想要操作就要遍历
2. 得到的元素对象是动态的

```html
<ul>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
</ul>

<script>

	// 返回的是：获取过来的元素对象的集合,以伪数组的形式存储
	var lis = document.getElementsByTagName('li');
	console.log(lis);

	// HTMLCollection(5)
	// 0: li
	// 1: li
	// 2: li
	// 3: li
	// 4: li
	// length: 5
	// __proto__: HTMLCollection

	console.log(lis[0]); //<li>text</li>

	// 想要依次打印里面的元素可以采取遍历的方式
	for (var i = 0; i < lis.length; i++) {
		console.log(lis[i]);
	}

	// 如果页面中只有一个li,返回的还是伪数组
	// 如果页面中没有这个元素,返回的是空的伪数组

</script>
```

还可以获取某个元素(父元素)内部的所有指定标签名的子元素

```element.getElementsByTagName('tagName')```

父元素必须是指定的单个对象,获取的时候不包括父元素自己

```html
<ul>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
</ul>
<ol id="ol">
	<li>another</li>
	<li>another</li>
	<li>another</li>
	<li>another</li>
	<li>another</li>
</ol>

<script>
	var ol = document.getElementsByTagName('ol');
	console.log(ol[0].getElementsByTagName('li'));
	//父元素必须是指定的单个对象
	//这里用的是ol[0],而不是[ol]


	//换一种思路，用ID获取ol，用TAG获取li
	var ol = document.getElementById('ol');
	console.log(ol.getElementsByTagName('li'));

</script>
```


## H5新增方法获取元素

`document.getElementsByClassName('class')`
// 根据类名返回元素对象集合

`document.querySelector('selector')`
// 根据指定选择器返回第一个元素对象

`document.querySelectorAll('selector')`
// 根据指定选择器返回所有元素


```html
<div class="box">盒子</div>
<div class="box">盒子</div>
<div id="nav">
	<ul>
		<li>首页</li>
		<li>产品</li>
	</ul>
</div>

<script>
	// 根据类名获取某些元素集合
	var boxes = document.getElementsByClassName('box');
	console.log(boxes);

	// HTMLCollection(2)
	// 0: div.box
	// 1: div.box
	// length: 2
	// __proto__: HTMLCollection



	// querySelector() 返回指定选择器的第一个元素对象，切记里面的选择器需要添加符号 .box #nav

	var firstBox = document.querySelector('.box');
	console.log(firstBox); //<div class="box">盒子</div>

	var nav = document.querySelector('#nav');
	console.log(nav);

	var li = document.querySelector('li');
	console.log(li);


	// querySelectorAll() 返回指定选择器的所有元素对象集合

	var allBox = document.querySelectorAll('.box');
	console.log(allBox);

</script>
```

## 获取特殊元素（body和html）


```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>

<body>
	<script>
		// 获取body元素
		var bodyEle = document.body;
		console.log(bodyEle);
		console.dir(bodyEle);

		// 获取html元素
		var htmlEle = document.html;
		console.log(htmlEle);  //undefined

		var htmlEle = document.documentElement;   //正确写法
		console.log(htmlEle);

	</script>
</body>
</html>
```

# 事件基础

- JS可以创建动态页面
- 事件是可以被JS侦测到的行为

> 简单理解：‘触发-响应’ 机制
> 网页中的每个元素都可以触发JS事件

## 事件三要素

事件由三部分组成：事件源、事件类型、事件处理程序，称为事件三要素

- 事件源：事件被触发的对象，谁
- 事件类型：如何触发，什么事件，比如鼠标点击onclick、鼠标经过、键盘按下
- 事件处理程序：通过函数赋值的方式完成

```html
<body>
	<button id="btn">唐伯虎</button>
	<script>

		// 事件源
		var btn = document.getElementById('btn');
		// 事件类型
		btn.onclick = function () {
			// 事件处理程序
			alert('点秋香');
		}
	</script>
</body>
```

## 执行事件的步骤

- 获取事件源
- 注册事件（绑定事件）
- 添加事件处理程序（采取函数赋值的形式）

```html
<div>123</div>
<script>
	// 执行事件步骤
	// 点击div 控制台输出 我被选中了
	// 1. 获取事件源
	var div = document.querySelector('div');
	// 2.绑定事件 注册事件
	// div.onclick 
	// 3.添加事件处理程序 
	div.onclick = function () {
		console.log('我被选中了');

	}
</script>
```

常见的鼠标事件

- onclick 鼠标点击左键触发
- onmouseover 鼠标经过触发
- onmouseout 鼠标离开触发
- onfocus 获得鼠标焦点触发
- onblur 失去鼠标焦点触发
- onmousemove 鼠标移动触发
- onmouseup 鼠标弹起触发
- onmousedown 鼠标按下触发

分析事件三要素



# 操作元素

JS的DOM操作可以改变网页内容、结构和样式，我们可以利用DOM操作元素来改变元素里面的内容、属性等


## 改变元素内容

`element.innerText()`
// 从起始位置到终止位置的内容，去除html标签，去除空格和换行

`element.innerHTML()`
// 从起始位置到终止位置的全部内容，包括html标签，保留空格和换行


```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<style>
		div,
		p {
			width: 300px;
			height: 30px;
			line-height: 30px;
			color: #fff;
			background-color: pink;
		}
	</style>
</head>

<body>
	<button>显示当前系统时间</button>
	<div>某个时间</div>
	<p>1123</p>
	<script>
		// 点击按钮，让div里面的文字发生变化
		// 1. 获取元素 
		var btn = document.querySelector('button');
		var div = document.querySelector('div');
		// 2.注册事件
		btn.onclick = function () {
			// div.innerText = '2019-6-6';
			div.innerHTML = getDate(); // 添加事件处理程序
		}

		function getDate() {
			var date = new Date();
			// 我们写一个 2019年 5月 1日 星期三
			var year = date.getFullYear();
			var month = date.getMonth() + 1;
			var dates = date.getDate();
			var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
			var day = date.getDay();
			return '今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day];
		}
		// 我们元素可以不用添加事件
		var p = document.querySelector('p');
		p.innerHTML = getDate();
	</script>
</body>
</html>
```

## innerText和innerHTML的区别

```html
<div>今天是：2019</div>
<p>
	我是文字
	<span>1231534</span>
</p>
<script>
	var div = document.querySelector('div');
	div.innerText = '<strong>今天是：</strong>2019';
	// 输出为：<strong>今天是：</strong>2019
	// HTML标签未被识别
	// innerText 非标准，会去除空格和换行

	div.innerHTML = '<strong>今天是：</strong>2019';
	// 输出为：今天是：2019
	// 其中‘今天是：’加粗了，HTML标签可以被识别
	// innerHTML W3C标准，会保留空格和换行

	// 以上操作均对div内的文本进行了‘写’操作
	// 注意：innerText和innerHTML均可以进行‘读’和‘写’操作

	// 用以上两种方式读一下p标签
	var p = document.querySelector('p');
	console.log(p.innerText);
	// 输出为：我是文字 1231534
	// 未保留HTML标签，去除了空格换行

	console.log(p.innerHTML);
	// 输出为：
	// 		我是文字
	// 		<span>1231534</span>
	// 保留了HTML标签，保留了空格换行

 	// innerHTML更为常用
</script>
```


## 修改元素属性

- innerText, innerHTML
- src, href
- id, alt, title


```html
<body>
	<button id="ldh">ldh</button>
	<button id="zxy">zxy</button>
	<img src="images/ldh.jpg" alt="" title="ldh">


	<script>
		// 修改元素属性 src
		// 1.获取元素
		var ldh = document.getElementById('ldh');
		var zxy = document.getElementById('zxy');
		var img = document.querySelector('img');
		// 2.注册事件 3.处理程序
		zxy.onclick = function () {
			img.src = 'images/zxy.jpg';  //对元素属性重新赋值即可
			img.title = 'zxy';
		}

		ldh.onclick = function () {
			img.src = 'images/ldh.jpg';
			img.title = 'ldh';
		}
	</script>
</body>
```

## 案例：分时显示不同图片，不同问候语

- 如果上午打开页面，显示“上午好”，显示上午图片
- 如果下午打开页面，显示“下午好”，显示下午图片
- 如果晚上打开页面，显示“晚上好”，显示晚上图片


```html
<body>
	<img src="images/s.gif" alt="">
	<div>上午好</div>

	<script>
		//获取元素
		var img = document.querySelector('img');
		var div = document.querySelector('div');

		//得到小时数
		var date = new Date();  //日期内置对象
		var h = date.getHours();

		//判断小时数改变图文信息
		if (h < 12) {
			img.src = 'images/s.gif';
			div.innerHTML = '上午好';
		} else if (h < 18) {
			img.src = 'images/x.gif';
			div.innerHTML = '下午好';
		} else {
			img.src = 'images/w.gif';
			div.innerHTML = '晚上好';
		}

	</script>
</body>
```

## 修改表单属性

利用DOM可以操作如下表单元素的属性
`type, value, checked, selected, disabled`

```html
<button>按钮</button>
<input type="text" value="content">
<script>
	// 获取元素
	var btn = document.querySelector('button');
	var input = document.querySelector('input');

	//注册事件 处理程序
	btn.onclick = function () {

		// 表单里的值 文字内容通过value来修改，innerHTML不行
		input.value = '被点击了';

		// 禁用表单disabled 让按钮button禁用
		// btn.disabled = true;

		// 此处的btn也可以换成this来做，this指向的是事件函数的调用者btn
		this.disabled = this;


	}
</script>
```

## 案例：模仿京东登陆页面显示明文密码

思路：
- 点击眼睛按钮，把密码框类型改为文本框
- 一个按钮两个状态，点击一次，切换为文本框，再点击一次切换为密码框

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<style>
		.box {
			position: relative;
			width: 400px;
			border-bottom: 1px solid #ccc;
			margin: 100px auto;
		}

		.box input {
			width: 370px;
			height: 30px;
			border: 0;
			outline: none;
		}

		.box img {
			position: absolute;
			top: 2px;
			right: 2px;
			width: 24px;
		}
	</style>
</head>

<body>
	<div class="box">
		<label for="">
			<img src="images/close.png" alt="" id="eye">
		</label>
		<input type="password" name="" id="pwd">
	</div>


	<script>
		var eye = document.getElementById('eye');
		var pwd = document.getElementById('pwd');

		var flag = 0;
		eye.onclick = function () {
			if (flag == 0) {
				pwd.type = 'text';
				eye.src = 'images/open.png';
				flag = 1;
			}
			else {
				pwd.type = 'password';
				eye.src = 'images/close.png';
				flag = 0;
			}
		}
	</script>

</body>

</html>

```

## 修改元素的样式属性

可以修改元素的大小、颜色、位置等样式

`element.style` 行内样式操作

`element.className` 类名样式操作

注意：

- JS里面的样式采用驼峰命名法，如fontSize, backgroundColor
- JS修改样式操作，产生的是行内样式，权重更高

```html
<style>
	div {
		width: 200px;
		height: 200px;
		background-color: pink;
	}
</style>

<div></div>

<script>
	var div = document.querySelector('div');

	div.onclick = function () {
		// div.style里面的属性采用驼峰命名法
		this.style.backgroundColor = 'purple';
		this.style.width = '250px';
	}
</script>
```


## 案例：淘宝点击关闭二维码

当鼠标点击二维码关闭按钮时，关闭整个二维码

思路：
- 利用样式的显示和隐藏完成
-> display:none 隐藏元素
-> display:block 显示元素
- 点击按钮，让这个二维码盒子隐藏起来

```html
<!-- 这里省了CSS样式 -->
<div class="box">
	淘宝二维码
	<img src="images/tao.png" alt="">
	<i class="close-btn">x</i>
</div>

<script>
	var btn = document.querySelector('.close-btn');
	var box = document.querySelector('.box');

	btn.onclick = function () {
		box.style.display = 'none';
	}
</script>
```

## 案例：循环精灵图背景

```html
<style>
	* {
		margin: 0;
		padding: 0;
	}

	li {
		list-style-type: none;
	}

	.box {
		width: 250px;
		margin: 100px auto;
	}

	.box li {
		float: left;
		width: 24px;
		height: 24px;
		background-color: pink;
		margin: 15px;
		background: url(images/sprite.png) no-repeat;
	}
</style>

<div>
	<ul>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
	</ul>
</div>

<script>
	// 获取元素
	var lis = document.querySelectorAll('li');

	// 循环修改图片的坐标
	for (var i = 0; i < lis.length; i++) {
		// 索引号乘44就是每个精灵图的y坐标
		var y = i * 44;
		lis[i].style.backgroundPosition = '0 -' + y + 'px';
	}
</script>
```


## 案例：显示隐藏文本框

鼠标点击文本框时，默认文字隐藏，鼠标离开文本框时，默认文字显示

两个新事件：

- onfocus 获得焦点
- onblur 失去焦点

```html
<style>
	input {
		color: #999;
	}
</style>

<form action="">
	<input type="text" value="手机">
</form>

<script>
	var text = document.querySelector('input');

	text.onfocus = function () {
		console.log('得到了焦点');

		// 获得焦点，判断表单里面内容是否是默认文字
		// 如果是默认文字，就清空表单内容
		if (this.value === '手机') {
			this.value = '';
		}

		// 获得焦点后，文本框颜色变黑
		this.style.color = '#333';
	}

	text.onblur = function () {
		console.log('失去了焦点');

		// 失去焦点，判断表单内容是否为空，如果为空，修改为默认文字
		if (this.value === '') {
			this.value = '手机';
		}
		// 失去焦点后，文本框颜色变浅
		this.style.color = '#999';
	}

</script>
```

## 使用ClassName修改样式属性

如果需要修改的样式比较多，一个一个用style写太慢

```html
<style>
	div {
		width: 100px;
		height: 100px;
		background-color: pink;
	}

	.change {
		background-color: purple;
		color: #fff;
		font-size: 25px;
		margin-top: 100px;
	}
</style>

<div>文本</div>

<script>
	var test = document.querySelector('div');
	tets.onclick = function () {

		// 可以修改元素的className更改元素的样式，适用于样式修改较多功能复杂的情况

		// 让当前元素的类名改为了CSS中的change类
		this.className = 'change';

		// className会覆盖掉原先的类名
		// 如果想保留原有类名，可用多类名选择器
		this.className = 'first change';
	}
</script>
```

## 案例：密码框格式提示错误信息

如果用户离开密码框，里面输入个数不是6-16个，则提示错误信息，否则提示正确信息

思路：
- 表单失去焦点用onblur
- 输入正确则提示正确的信息，颜色为绿色，小图标变化
- 如果输入的不是6-16位，则提示错误信息，颜色为红色，小图标变化
- 因为样式变化较多，采用className修改样式

```html
<style>
	div {
		width: 600px;
		margin: 100px auto;
	}

	.message {
		display: inline-block;
		font-size: 12px;
		color: #999;
		background: url(images/mess.png) no-repeat left center;
		padding-left: 20px;
	}

	.wrong {
		color: red;
		background-image: url(images/wrong.png);
	}

	.right {
		color: green;
		background-image: url(images/right.png);
	}
</style>

<div class="register">
	<input type="password" class='ipt'>
	<p class='message'>请输入6-16位密码</p>
</div>

<script>
	var ipt = document.querySelector('.ipt');
	var message = document.querySelector('.message');

	ipt.onblur = function () {
		if (this.value.length < 6 || this.value.length > 16) {
			console.log('error');
			message.className = 'message wrong';
			message.innerHTML = '不符合6-16位的要求';
		} else {
			message.className = 'message right';
			message.innerHTML = '符合6-16位的要求';
		}
	}
</script>
```


## 操作元素总结

操作元素

- 操作元素内容 innerText, innerHTML
- 操作常见元素属性 src, href, alt, etc.
- 操作表单元素属性 type, value, disabled, etc.
- 操作元素样式属性 element.style, className

作业：

- 1.世纪佳缘 用户名 显示隐藏内容
- 2.京东关闭广告（直接隐藏即可）
- 3.新浪下拉菜单（新浪微博即可）
- 4.开关灯案例，页面背景色黑白切换


## 排他思想（算法）

排他思想算法：
1. 所有元素全部清除样式（干掉其他人）
2. 给当前元素设置样式（留下我自己）

注意：顺序不能颠倒，首先干掉其他人，再设置自己

```html
<body>
	<button>按钮1</button>
	<button>按钮2</button>
	<button>按钮3</button>
	<button>按钮4</button>
	<button>按钮5</button>

	<script>
		var btns = document.getElementsByTagName('button');

		//btns得到的是伪数组
		for (var i = 0; i < btns.length; i++) {
			btns[i].onclick = function () {
				// 先把所有的背景颜色去掉
				for (var i = 0; i < btns.length; i++) {
					this.style.backgroundColor = '';
				}
				// 然后让当前元素的背景颜色变色
				this.style.backgroundColor = 'pink';
			}
		}
	</script>

</body>
```

## 案例：百度换肤效果

思路：
- 给4个小图片注册点击事件（利用循环）
- 点击小图片，让页面背景修改为当前图片
- 核心算法：把当前图片的src路径取过来，给body作为背景


```html
<style>

</style>

<body>
	<ul class="baidu">
		<li><img src="images/1.jpg" alt=""></li>
		<li><img src="images/2.jpg" alt=""></li>
		<li><img src="images/3.jpg" alt=""></li>
		<li><img src="images/4.jpg" alt=""></li>
	</ul>
</body>

<script>
	// 获取图片元素
	var imgs = document.querySelector('.baidu').querySelectorAll('img');

	// 循环注册事件
	for (var i = 0; i < imgs.length; i++) {
		imgs[i].onclick = function () {

			// this.src是点击的图片的路径
			// 把该路径给body即可
			document.body.style.backgroundImage = 'url(' + this.src + ')';
		}
	}

</script>
```

## 案例：表格悬浮经过变色


```html
<style>
	table {
		width: 800px;
		margin: 100px auto;
		text-align: center;
		border-collapse: collapse;
		font-size: 14px;
	}

	thead tr {
		height: 30px;
		background-color: skyblue;
	}

	tbody tr {
		height: 30px;
	}

	tbody td {
		border-bottom: 1px solid #d7d7d7;
		font-size: 12px;
		color: blue;
	}

	.bg {
		background-color: pink;
	}
</style>

<body>
	<table>
		<thead>
			<tr>
				<th>代码</th>
				<th>名称</th>
				<th>最新公布净值</th>
				<th>累计净值</th>
				<th>前单位净值</th>
				<th>净值增长率</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>003526</td>
				<td>农银金穗3个月定期开放债券</td>
				<td>1.075</td>
				<td>1.079</td>
				<td>1.074</td>
				<td>+0.047%</td>
			</tr>
			<tr>
				<td>003526</td>
				<td>农银金穗3个月定期开放债券</td>
				<td>1.075</td>
				<td>1.079</td>
				<td>1.074</td>
				<td>+0.047%</td>
			</tr>
			<tr>
				<td>003526</td>
				<td>农银金穗3个月定期开放债券</td>
				<td>1.075</td>
				<td>1.079</td>
				<td>1.074</td>
				<td>+0.047%</td>
			</tr>
			<tr>
				<td>003526</td>
				<td>农银金穗3个月定期开放债券</td>
				<td>1.075</td>
				<td>1.079</td>
				<td>1.074</td>
				<td>+0.047%</td>
			</tr>
			<tr>
				<td>003526</td>
				<td>农银金穗3个月定期开放债券</td>
				<td>1.075</td>
				<td>1.079</td>
				<td>1.074</td>
				<td>+0.047%</td>
			</tr>
			<tr>
				<td>003526</td>
				<td>农银金穗3个月定期开放债券</td>
				<td>1.075</td>
				<td>1.079</td>
				<td>1.074</td>
				<td>+0.047%</td>
			</tr>
		</tbody>
	</table>

	<script>
		// 思路：
		// - 用到鼠标事件，鼠标经过onmouseover，鼠标离开onmouseout
		// - 核心思路：鼠标经过tr行，当前行变背景颜色，鼠标离开去掉当前背景色
		// - 注意：第一行表头不需要变色，因此我们获取的是tbody里面的行


		// 获取元素
		var trs = document.querySelector('tbody').querySelectorAll('tr');

		// 循环注册事件
		for (var i = 0; i < trs.length; i++) {

			// 鼠标经过变色
			trs[i].onmouseover = function () {
				this.className = 'bg';
			}

			//鼠标离开去色
			trs[i].onmouseout = function () {
				this.className = '';
			}
		}
	</script>

</body>
```

## 案例：表单全选取消

```html
<style>
	* {
		padding: 0;
		margin: 0;
	}

	.wrap {
		width: 300px;
		margin: 100px auto 0;
	}

	table {
		border-collapse: collapse;
		border-spacing: 0;
		border: 1px solid #c0c0c0;
		width: 300px;
	}

	th,
	td {
		border: 1px solid #d0d0d0;
		color: #404060;
		padding: 10px;
	}

	th {
		background-color: #09c;
		font: bold 16px "微软雅黑";
		color: #fff;
	}

	td {
		font: 14px "微软雅黑";
	}

	tbody tr {
		background-color: #f0f0f0;
	}

	tbody tr:hover {
		cursor: pointer;
		background-color: #fafafa;
	}
</style>

</head>

<body>
	<div class="wrap">
		<table>
			<thead>
				<tr>
					<th>
						<input type="checkbox" id="j_cbAll" />
					</th>
					<th>商品</th>
					<th>价钱</th>
				</tr>
			</thead>
			<tbody id="j_tb">
				<tr>
					<td>
						<input type="checkbox" />
					</td>
					<td>iPhone8</td>
					<td>8000</td>
				</tr>
				<tr>
					<td>
						<input type="checkbox" />
					</td>
					<td>iPad Pro</td>
					<td>5000</td>
				</tr>
				<tr>
					<td>
						<input type="checkbox" />
					</td>
					<td>iPad Air</td>
					<td>2000</td>
				</tr>
				<tr>
					<td>
						<input type="checkbox" />
					</td>
					<td>Apple Watch</td>
					<td>2000</td>
				</tr>

			</tbody>
		</table>
	</div>

	<script>


		// Step1:全选和取消全选：让下方所有复选框的checked属性跟随全选变化

		// 获取元素
		var j_cbAll = document.getElementById('j_cbAll');
		var j_tbs = document.getElementById('j_tb').getElementsByTagName('input');

		// 注册事件
		j_cbAll.onclick = function () {
			for (var i = 0; i < j_tbs.length; i++) {
				//this.checked 可以得到当前复选框的选中状态，true/false
				j_tbs[i].checked = this.checked;
			}
		}

		// Step2: 下面复选框需要全部选中，上面全选才能选中：给下面所有复选框绑定点击事件，每次点击，都要循环查看下面所有的复选框是否有没选中的，如果有一个没选中的，上面全选就不选中

		for (var i = 0; i < j_tbs.length; i++) {
			j_tbs[i].onclick = function () {
				// 每次点击下面的复选框都要循环检查是否被选中

				// flag控制全选按钮是否选中
				var flag = true;

				for (i = 0; i < j_tbs.length; i++) {
					if (!j_tbs[i].checked) {
						flag = false;
						break; //退出for循环，提高执行效率，只要有一个是false就不是全选
					}
				}
				j_cbAll.checked = flag;
			}
		}
	</script>

</body>

```

## 自定义属性的操作

获取元素的属性值

```html
<body>
	<div id="demo" index="1" class="nav"></div>
</body>

<script>
	// 获取元素的属性：element.attribute
	var div = document.querySelector('demo');
	console.log(div.id);

	// 获取元素的属性：element.getAttribute()
	console.log(div.getAttribute('id'));

	// 二者的区别：
	// element.attribute一般获取内置属性
	// element.getAttribute()一般获取自定义属性
	console.log(div.getAttribute('index'));  //1

</script>
```


设置属性值

```html
<script>
	// 设置属性值：element.attribute = 'value'; 
	// 设置内置属性值

	div.id = 'test';
	// <div id="test" index="1"></div>
	div.className = 'navs';


	// 设置属性值：element.setAttribute('attibute','value') 
	// 设置自定义属性
	div.setAttribute('index', 2);
	//<div id="test" index="2"></div>

	div.setAttribute('class', 'footer');  //class特殊，不是className

</script>
```

移除属性

```html
<script>
	// 移除属性：element.removeAttribute('attibute');
	div.removeAttribute('index');

</script>
```


## 案例：tab栏切换（重点★）

当鼠标点击上面相应的选项卡，下面的内容跟随变化

分析：
- Tab栏有两个大的模块
- 上部分模块为选项卡，点击一个，当前底色为红色，其余不变（排他思想），修改类名
- 下部分模块内容，会跟随上部分选项卡变化，所以下部分模块的变化写到上部分的点击事件里

```html
<style>
	* {
		margin: 0;
		padding: 0;
	}

	li {
		list-style-type: none;
	}

	.tab {
		width: 978px;
		margin: 100px auto;
	}

	.tab_list {
		height: 39px;
		border: 1px solid #ccc;
		background-color: #f1f1f1;
	}

	.tab_list li {
		float: left;
		height: 39px;
		line-height: 39px;
		padding: 0 20px;
		text-align: center;
		cursor: pointer;
	}

	.tab_list .current {
		background-color: #c81623;
		color: #fff;
	}

	.item_info {
		padding: 20px 0 0 20px;
	}

	.item {
		display: none;
	}
</style>
</head>

<body>
	<div class="tab">
		<div class="tab_list">
			<ul>
				<li class="current">商品介绍</li>
				<li>规格与包装</li>
				<li>售后保障</li>
				<li>商品评价（50000）</li>
				<li>手机社区</li>
			</ul>
		</div>
		<div class="tab_con">
			<div class="item" style="display: block;">
				商品介绍模块内容
			</div>
			<div class="item">
				规格与包装模块内容
			</div>
			<div class="item">
				售后保障模块内容
			</div>
			<div class="item">
				商品评价（50000）模块内容
			</div>
			<div class="item">
				手机社区模块内容
			</div>

		</div>
	</div>

	<script>

		// 获取元素
		var tab_list = document.querySelector('.tab_list');
		var lis = tab_list.querySelectorAll('li');
		var items = document.querySelectorAll('.tab_con');

		// 绑定事件
		for (var i = 0; i < lis.length; i++) {

			// Step1:处理上部分模块的切换变色功能
			lis[i].onclick = function () {

				// 先排他，去掉所有li的类名
				for (var i = 0; i < lis.length; i++) {
					lis[i].className = '';
				}

				// 再单独给当前的li赋新类
				this.className = 'current';

				// Step2:切换下面的内容模块

				// 核心思路：给上面的tab_list里所有的li添加自定义属性，属性值从0开始

				// 给5个li设置索引号
				lis[i].setAttribute('index', i);

				var index = this.getAttribute('index');

				// 当我们点击tab_list里面某个li，让tab_con里面对应序号的内容显示，其余隐藏（排他思想）

				for (var i = 0; i < items.length; i++) {
					items[i].style.display = 'none';
				}
				items[index].style.display = 'block';

			}
		}

	</script>

</body>>
```

## H5自定义属性

目的：为了保存并使用数据，有些数据可以保存到页面中，而不用保存到数据库中

通过 `getAttribute()` 获取自定义属性

H5规定自定义属性以data-开头作为属性名，并赋值

例如 `<div data-index="1"></div>`

或者通过JS设置

```html
<div getTime="20" data-index="2"></div>
<script>
	var div = document.querySelector('div');
	console.log(div.getTime); //undefined,获取不到自定义属性
	console.log(div.getAttribute('getTime')); //20

	div.setAttribute('data-time', 20);
</script>
```

获取H5自定义属性

兼容性获取 *更好用*
- element.getAttribute('data-index');

H5新增获取 (IE11+才支持)
- element.dataset.index
- element.dataset['index']

```html
<div getTime="20" data-index="2" data-list-name="andy"></div>
<script>
	// dataset是一个集合，里面存放了所有以data-开头的自定义属性
	console.log(div.dataset);

	// 短的属性名
	console.log(div.dataset.index);
	console.log(div.dataset[index]);

	// 长的属性名
	console.log(div.dataset.listName); //注意这里改成了驼峰命名法
	console.log(div.dataset['listName']);
</script>
```


# 节点操作


## 获取元素方式

1. 利用DOM提供的方法获取元素
   - getElementById
   - getElementsByTagName
   - querySelector
   - 逻辑性不强，繁琐


2. 利用节点层级关系获取元素
   - 利用父子兄节点关系获取元素
   - 逻辑性强，但是兼容性差


这两种方式都可以获取节点元素，都会使用，但是节点操作更简单


## 节点概述

- 网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM中，节点使用node表示
- HTML DOM树中的所有节点均可通过JS访问呢，所有HTML元素均可修改，也可以创建或删除
- 一般的，节点至少拥有三个基本属性：nodeType/nodeName/nodeValue


节点类型
- 元素节点：nodeType = 1
- 属性节点：nodeType = 2
- 文本节点：nodeType = 3 (文本节点包含文字、空格、换行等)

> 实际开发中，主要操作的是元素节点

```html
<div>iamdiv</div>
<span>iamspan</span>
<ul>
	<li>iamli</li>
	<li>iamli</li>
	<li>iamli</li>
	<li>iamli</li>
	<li>iamli</li>
</ul>
<div class="box">
	<span class="qrcode"></span>
</div>

<script>
	var box = document.querySelector('.box');
	console.dir(box);

	// nodeName: "DIV"
	// nodeType: 1
	// nodeValue: null

</script>
```

## 节点层级

父子兄层级关系

```mermaid
graph TD
	html-->head
	html-->body
	head-->title-->text1
	body-->a-->href
	body-->h1-->text2
```


1. 父级节点 parentNode

```html
<div class="demo">
	<div class="box">
		<span class="qrcode"></span>
	</div>
</div>

<script>
	var qrcode = document.querySelector('.qrcode');
	// var box = document.querySelector('.box');
	// 父节点 parentNode 得到是*最近*的父节点，找不到返回为null
	qrcode.parentNode; 
</script>
```

2. 子节点 childNode
parentNode.childNodes - 标准 - 获取所有子节点 - 不好用
parentNode.children - 非标准 - 获取所有子元素节点 - 好用!!!

```html
<ul>
	<li>iamli</li>
	<li>iamli</li>
	<li>iamli</li>
	<li>iamli</li>
</ul>

<script>
	// DOM 方法获取ul和li
	var ul = document.querySelector('ul');
	var lis = ul.querySelectorAll('li');

	// 子节点获取 parentNode.childNodes 标准!!!
	// 所有的子节点，包含元素/文本等节点
	console.log(ul.childNodes); //这里有9个子节点
	console.log(ul.childNodes[0].nodeType); //3 文本节点
	console.log(ul.childNodes[1].nodeType); //1 元素节点

	// 遍历比较输出
	for (var i = 0; i < ul.childNodes.length; i++) {
		if (ul / childNodes[i].nodeType == 1) {
			console.log(ul.childNodes[i]);
		}
	}

	// 所以一般不提倡使用子节点childNodes
	// 而是用子节点另一种获取方式 parentNode.children  非标准!!!

	// parentNode.children是一个只读属性，返回所有的子元素节点，注意，只返回子*元素*节点，其余节点不返回

	// 虽然children非标准，但是得到了各个浏览器的支持，可以放心使用

	console.log(ul.children);  // 4个li节点

</script>
```

## 获取first/last子元素

```html
<ol>
	<li>iamli1</li>
	<li>iamli2</li>
	<li>iamli3</li>
	<li>iamli4</li>
</ol>

<script>
	var ol = document.querySelector('ol');
	// 第一个/最后一个节点
	console.log(ol.firstChild);
	console.log(ol.lastChild);

	// 第一个/最后一个元素节点
	console.log(ol.firstElementChild);
	console.log(ol.lastElementChild);

	// 注意，firstElementChild 和 lastElementChild 有兼容性问题，IE9+才支持

	// 实际开发的写法，既没有兼容性问题，又返回元素节点
	console.log(ol.children[0]);
	console.log(ol.children[ol.children.length - 1]);

</script>
```

## 案例：新浪下拉菜单

```html
<style>
	* {
		margin: 0;
		padding: 0;
	}

	li {
		list-style-type: none;
	}

	a {
		text-decoration: none;
		font-size: 14px;
	}

	.nav {
		margin: 100px;
	}

	.nav>li {
		position: relative;
		float: left;
		width: 80px;
		height: 41px;
		text-align: center;
	}

	.nav li a {
		display: block;
		width: 100%;
		height: 100%;
		line-height: 41px;
		color: #333;
	}

	.nav>li>a:hover {
		background-color: #eee;
	}

	.nav ul {
		display: none;
		position: absolute;
		top: 41px;
		left: 0;
		width: 100%;
		border-left: 1px solid #FECC5B;
		border-right: 1px solid #FECC5B;
	}

	.nav ul li {
		border-bottom: 1px solid #FECC5B;
	}

	.nav ul li a:hover {
		background-color: #FFF5DA;
	}
</style>

<ul class="nav">
	<li>
		<a href="#">微博</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
	<li>
		<a href="#">微博</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
	<li>
		<a href="#">微博</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
	<li>
		<a href="#">微博</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
</ul>

<script>
	// 导航栏里面的li都有鼠标经过效果，需要循环注册鼠标事件
	// 当鼠标经过li中的第二个孩子ul时显示，当鼠标离开，ul隐藏

	var nav = document.querySelector('.nav');
	var lis = nav.children;

	for (var i = 0; i < lis.length; i++) {
		lis[i].onmouseover = function () {
			this.children[1].style.display = 'block';
		}

		lis[i].onmouseout = function () {
			this.children[1].style.display = 'none';
		}
	}
</script>
```

## 节点操作：兄弟节点


包含元素或文本节点
- `node.nextSibling` 下一个兄弟节点(包含元素或者文本节点等)
- `node.previousSibling` 上一个兄弟节点(包含元素或者文本节点等)


只包含元素节点
- `node.nextElementSibling` 下一个兄弟元素节点
- `node.previousElementSibling` 上一个兄弟元素节点
> 只包含元素节点的这两个方法有兼容性问题，IE9+才支持

```html
<div>iamdiv</div>
<span>iamspan</span>
<script>
	var div = document.querySelector('div');
	console.log(div.nextSibling); //#text
	console.log(div.previousSibling); //#text

	console.log(div.nextElementSibling); //<span>iamspan</span>
	console.log(div.previousElementSibling); //<span>iamspan</span>


	//如何解决兼容性问题？封装一个兼容性的函数
	function getNextElementSibling(element) {
		var el = element;
		while (el = el.nextSibling) {
			if (el.nodeType == 1) {
				return el;
			}
			return null;
		}
	}

</script>
```

## 节点操作：创建/添加节点

> 例如网页新增留言，新增元素

### 创建节点

`document.createElement()`
该方法创建由tagName指定的HTML元素，因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为“动态创建元素节点”

### 添加节点

`node.appendChild(child)`
该方法将一个节点添加到指定父节点的子节点列表*末尾*，类似CSS中的after伪元素

`insertBefore(child, selectedElement)`
该方法将一个节点添加到指定父节点的指定子节点的*前面*，类似CSS中的before伪元素

```html
<body>
	<ul>
		<li>123</li>
	</ul>
</body>

<script>
	// 创建元素节点
	var li = document.createElement('li');

	// 添加节点
	var ul = document.querySelector('ul');
	ul.appendChild(li);  //后面追加元素，类似数组的push()

	var lili = document.createElement('li');
	ul.insertBefore(lili, ul.children[0]); //前面添加元素

	// 页面添加新元素分两步：1.创建元素，2.添加元素

</script>
```

## 案例：简单版发布留言

```html
<textarea name="" id="">123</textarea>
<button>发布</button>
<ul>

</ul>

<script>
	// 获取元素
	var btn = document.querySelector('button');
	var text = document.querySelector('textarea');
	var ul = document.querySelector('ul');

	// 绑定元素 注册事件
	btn.onclick = function () {

		//加一个判断，如果输入的内容为空，弹提示框
		if (text.value == '') {
			alert('no content');
			return false;
		} else {
			//创建元素
			var li = document.createElement('li');

			//给元素赋值
			li.innerHTML = text.value;

			//在后面添加
			ul.appendChild(li);

			//在前面添加
			ul.insertBefore(li, ul.children[0]);
		}
	}
</script>
```

## 节点操作：删除节点

`node.removeChild(child)` 删除一个子节点

```html
<button>删除</button>
<ul>
	<li>熊大</li>
	<li>熊二</li>
	<li>光头强</li>
</ul>

<script>
	//获取元素
	var ul = document.querySelector('ul');
	var btn = document.querySelector('button');

	//删除元素
	btn.onclick = function () {
		// 判断是否还有内容可以删
		if (ul.children.length == 0) {
			alert('已经删完了还删什么删！');
			this.disabled = true; //禁用该按钮

		} else {
			ul.removeChild(ul.children[0]);
		}

	}
</script>
```

## 案例：删除留言案例

```html
<textarea name="" id="">123</textarea>
<button>发布</button>
<ul>

</ul>

<script>
	// 获取元素
	var btn = document.querySelector('button');
	var text = document.querySelector('textarea');
	var ul = document.querySelector('ul');

	// 绑定元素 注册事件
	btn.onclick = function () {

		//加一个判断，如果输入的内容为空，弹提示框
		if (text.value == '') {
			alert('no content');
			return false;
		} else {
			//创建元素
			var li = document.createElement('li');

			//给元素赋值
			li.innerHTML = text.value + "<a href='javascript:;'>删除</a>";

			//防止链接跳转，地址栏不加#号
			//可以用href="javascript:;" 或者href="javascript:void(0);"

			//在前面添加
			ul.insertBefore(li, ul.children[0]);

			//删除当前链接的元素
			var as = document.querySelectorAll('a');
			for (var i = 0; i < as.length; i++) {
				as[i].onlclick = function () {
					// 删除的是a所在的li 而li在ul里，等于是我是a，我叫我爷爷ul删除了我爸爸li
					ul.removeChild(this.parentNode);

				}
			}
		}
	}
</script>
```

## 节点操作：复制节点

`node.cloneNode()`

```html
<ul>
	<li>1</li>
	<li>2</li>
	<li>3</li>
</ul>

<script>
	var ul = document.querySelector('ul');

	// 先克隆
	var lili = ul.children[0].cloneNode();

	//如果node.cloneNode()括号里的参数为空或者false,则是*浅拷贝*,只克隆复制接电ul.children脑本身，不克隆里面的子节点

	//如果node.cloneNode(true)则是*深拷贝*，复制标签且复制内容

	// 再添加
	ul.appendChild(lili);

</script>
```

## 案例：动态生成表格

```html
<style>
	table {
		width: 500px;
		margin: 100px auto;
		border-collapse: collapse;
		text-align: center;
	}

	td,
	th {
		border: 1px solid #333;
	}

	thead tr {
		height: 40px;
		background-color: #ccc;
	}
</style>

<table cellspacing="0">
	<thead>
		<tr>
			<th>姓名</th>
			<th>科目</th>
			<th>成绩</th>
			<th>操作</th>
		</tr>
	</thead>
	<tbody>

	</tbody>
</table>

<script>
	// 准备学生数据
	var datas = [{
		name: 'wei',
		subject: 'js',
		score: 100
	}, {
		name: 'hong',
		subject: 'js',
		score: 98
	}, {
		name: 'fu',
		subject: 'js',
		score: 100
	}, {
		name: 'ming',
		subject: 'js',
		score: 100
	},
	];

	//在tbody中创建行
	var tbody = document.querySelector('tbody');
	for (var i = 0; i < datas.length; i++) {
		// create tr
		var tr = document.createElement('tr');
		tbody.appendChild(tr);

		//行里面创建的单元格
		//单元格的数量等于对象的属性个数
		for (var k in datas[i]) {
			var td = document.createElement('td');
			//单元格填充数据：把对象里的属性值datas[i][k]赋值给单元格元素
			td.innerHTML = datas[i][k];
			tr.appendChild(td);
		}

		//创建删除单元格
		var td = document.createElement('td');
		td.innerHTML = '<a href="javascript:;">delete</a>';
		tr.appendChild(td);
	}

	//删除操作
	var as = document.querySelectorAll('a');

	for (var i = 0; i < as.length; i++) {
		as[i].onclick = function () {
			tbody.removeChild(this.parentNode.parentNode);
		}
	}
</script>
```

## 三种动态创建元素的区别

- `document.write()`
- `element.innerHTML`
- `document.createElement()`

```html
<button>点击</button>
<p>abc</p>
<div class="inner"></div>
<div class="create"></div>

<script>
	//document.write() 创建元素
	//直接将内容写入页面的内容流，文档流执行完毕，会导致页面重绘，原有内容都会没有
	var btn = document.querySelector('button');
	btn.onclick = function () {
		document.write('<div>123</div>')
	}

	//element.innerHTML创建元素
	//innerHTML是将内容写入某个DOM节点，不会导致页面全部重绘
	//innerHTML创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂
	var inner = document.querySelector('.inner');
	inner.innerHTML = '<a href="#">baidu</a>';

	//document.createElement()创建元素
	//createElement()创建多个元素效率稍微低一点点，但是结构更清晰
	var create = document.querySelector('.create');
	var a = document.createElement('a');
	create.appendChild(a);

	//★总之，不管什么浏览器，innerHTML的效率都要比createElement高
</script>
```

## DOM重点核心

DOM - 文档对象模型 - W3C标准 - 可扩展标记语言的接口

改变网页的内容、结构和样式

1. 对于JS，为了能够使JS操作HTML，JS有一套自己的DOM编程接口
2. 对于HTML，DOM使得HTML形成一颗DOM树，包含文档、元素、节点

获取的DOM元素是一个‘对象’

关于DOM操作，我们主要是对元素操作，主要有创建、增删改查、属性操作、事件操作

```
创建：document.write() / innerHTML / createElement()

增加：appendChild() / insertChild()

删除：removeChild()

修改：修改DOM元素的内容、属性、表单值等
- 属性：src, href, title
- 内容：innerHTML, innerText
- 表单：value, type, disabled
- 样式：style, className

查询：
- DOM API: getElementById / getElementsByTagName 古老用法，不推荐
- H5: querySelector / querySelectorAll 推荐
- Node: (父子兄弟) parentNode, children, previousElementSibling, nextElementSibling 推荐

属性操作：
- setAttribute
- getAttribute
- removeAttribute

事件操作：
- onclick 鼠标点击左键触发
- onmouseover 鼠标经过触发
- onmouseout 鼠标离开触发
- onfocus 获得鼠标焦点触发
- onblur 失去鼠标焦点触发
- onmousemove 鼠标移动触发
- onmouseup 鼠标弹起触发
- onmousedown 鼠标按下触发
```