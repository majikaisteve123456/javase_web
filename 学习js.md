## javascript简介

脚本语言，不需要事先进行编译，只需适当的解释器就可以执行，可以嵌入html文件中，随着网页传送到客户端浏览器执行

* 可以制作网页特效
* 提供表单的前端验证
* 窗口动态操作
* 提高系统工作效率



**onmouseover**

<html>
<body>
<p onmouseover="alert('欢迎学习javascript')">鼠标移过来</p>
</body>
</html>



**在网页中进行打印**

<html>
<body>
<script>document.write("欢迎学习javascript");</script>
</body>
</html>

可以了将代码单独存储以.js为扩展名的文件中，利用src属性引入

<script src="welcome.js"></script>



为了避免某些浏览器不完全嵌入js代码，可以用注释语句括起来

<script>

<!-->

<-->

</script>



**在页面中将一些页面的文本进行替换** 

<html>
<head>
<script>
  function display()
  {

     document.getElementById("demo").innerHTML=Date();
  }

</script>
</head>
<body>
<p id="demo">这是一个段落</p>
<button type="button" onclick="display()">显示日期</button>
</body>
</html>



**点击图片实现图片的切换** 

<html>
<body>
<p id="demo">对点击按钮做出反应</p>
<script>
 function changeimage()
 {

    elem=document.getElementById("bulb");
    if(elem.src.match("bulbon"))//图像的名字
    {
       elem.src="images/pic_bulboff.gif";
    }
    else
    {
        elem.src="images/pic_bulbon.gif";
    }

 }
</script>

<img id="bulb" onclick="changeimage()" src="images/pic_bulboff.gif" width="100" height="80"/>
</body>
</html>



**输出到控制台**

浏览器使用F12启动控制台调试模式

使用console.log(xxx);输出到控制台上



**单行注释**

//



**多行注释**

/*

*/



**字符串赋值**

var a="a";



**数组定义**：

方式一：

var cars=new Array();

car[0]="c";

car[1]="a";

car[2]=“r”;

方式二：

var cars=new Array("c","a","r");

方式三：

var cars=["c","a","r"];



**对象的定义**：

var person=

{

firstname:"John",

lastname:"Doe",

id:5566

};

对对象的属性进行使用

person["lastname"]

person.lastname



对象还可以这样定义：

var person=new Object();



没有进行定义undefined 和null不是一回事





**自动数据类型转换：**

如果表达式用+运算符，且其中一个操作符为字符串，另一个操作符为数值，js自动将数值转成字符串

如果表达式中用了其他运算符，js自动将字符串转成数值



数据类型转换：

eval：将传入的字符参数内容，转换成相应的数值

y=eval("15")+8;  结果:y=23

parseInt("xxx"),将传入的字符串转化为整型

parseFloat("xxx") 将传入的字符串转化为浮点数



变量的作用域：全局变量和局部变量

* 在函数外声明的变量是全局变量，全局变量在任何脚本和函数内均可访问
* 如果变量没有声明，将自动变成全局变量
* 在HTML中所有的全局变量都会变成window对象的属性



typeof x  显示出变量的类型



javascript中程序控制流程可以使用

for(变量 in 对象)

{

}

来循环遍历对象的属性



异常处理

try{

}

catch（err）

{

}



抛出异常 throw



email地址格式验证：

<html>

	<head>
		<script>
			function validateForm(){
				var x=document.forms["myForm"]["email"].value;
				var atpos=x.indexOf("@");
				var dotpos=x.lastIndexOf(".");
				if (atpos<1 || dotpos<atpos+2 || dotpos+2>=x.length){
					alert("Not a valid e-mail address");
					return false;
				}
			}
		</script>
	</head>
	<body>
		<form name="myForm" action="demo-form.php" onsubmit="return validateForm();" method="post">
			Email: <input type="text" name="email">
			<input type="submit" value="Submit">
		</form>
	</body>
</html>



**form表单的onsubmit() return 问题**

验证表单中数据的合法性：

onsubmit=“validateForm();”中return false来阻止表单的提交

但是实际效果是return false 表单还是提交

使用onsubmit="return validateForm();" 就没有问题



onsubmit属性就是<form>这个html对象的一个方法名，其值就是一字符串，在方法体中可以写任意多个语句,包括内置函数和自定义函数



用上一种写法虽然返回了false，但是只是执行了函数，没有对结果进行任何处理

如果写成了第二种写法，则有利用返回值



**json字符串转化为对象**

<html>

	<body>
		<h2>为 JSON 字符串创建对象</h2>
	
		<p id="demo"></p>
		<script>
			var text = '{"employees":[' +
			'{"firstName":"John","lastName":"Doe" },' +
			'{"firstName":"Anna","lastName":"Smith" },' +
			'{"firstName":"Peter","lastName":"Jones" }]}';
	
			obj = JSON.parse(text);
			document.getElementById("demo").innerHTML =
			obj.employees[1].firstName + " " + obj.employees[1].lastName;
		</script>
	</body>
</html>



**引入javascript的方法**

<script type=="text/script"></script> 推荐

<script language="Javascript"></script>



**void的使用方法：**

**点击链接跳出弹窗**

<p>点击链接</p>

<a href="javascript:void(alert('warning'))">点击</a>



函数中的语句：

 a = void ( b = 5, c = 7 );

	document.write('a = ' + a + ' b = ' + b +' c = ' + c );
	返回的是undefined




死链接：(用void创建一个死链接)

<a href="javascript:void(0);">点我没反应</a>

锚点

<a href="#pos">点我定位到指定位置！</a>

<br><br><br><br><br>

<p id="pos">尾部定位点</p>





**DOM**

<div id="main">

   <p>DOM是非常有用的</p>

  <p> 该实例展示了

​               <b>getElementByTagName </b>方法

   </p>

</div>

<script>

​          var  x=document.getElementById("main");

​          var y= x.getElementsByTagName("p");

​          document.write('First paragraph inside "main" is'+y[0].innerHTML);

</script>



**DOM改变HTML元素内容**

改变HTML输出流： document.write(Date（）);

改变HTML元素内容：document.getElementById("p1").innerHTML="新文本";

改变HTML元素属性：document.getElementById("image").src="landscape.jpg";

改变HTML元素的样式：

document.getElementById("p1").style.color="blue";



鼠标点击触动

onmousedown="mDown(this)"

onmouseup="mUp(this)"



鼠标移到上方和鼠标移出

onmouseover="mOver(this)"

onmouseout="mOut(this)"



当鼠标离开输入框后，函数被触发

onchange="myfunction()"



**为元素添加事件**

<html>	

	<body>
		<p>点击按钮执行 <em>displayDate()</em> 函数.</p>
		<button id="myBtn">点这里</button>
		<script>
			document.getElementById("myBtn").onclick=function(){displayDate()};
			function displayDate(){
				document.getElementById("demo").innerHTML=Date();
			}
		</script>
		<p id="demo"></p>
	</body>
</html> 
​	

用onload事件来检查是否支持cookie，navigator.cookieEnabeld 返回的是一个布尔类型的值

<html>

	<body onload="checkCookies()">
		<script>
			function checkCookies(){
				if (navigator.cookieEnabled==true){
					alert("Cookies 可用")
				}
				else{
					alert("Cookies 不可用")
				}
			}
		</script>
		<p>弹窗-提示浏览器cookie是否可用。</p>
	</body>
</html>



## Bootstrap前端框架学习##









