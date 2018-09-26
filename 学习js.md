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





