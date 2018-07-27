# 什么是node.js#

运行服务端的javascript





# 安装node.js##

下载二进制文件（.exe）

命令行进入安装的目录 

node --version



# 创建第一个应用#

不仅在实现一个应用，同时还实现整个HTTP服务器

Node.js 应用是由那几部分组成的

1. 引入required模块，可以使用require指令来再如Node.js模块
2. 创建服务器：服务求器可以监听客户端的请求
3. 接收请求和响应请求 服务端很容易创建，客户端可以使用浏览器或终端发送HTTP请求，服务器接收请求后返回响应数据



## 步骤一、引入required模块##

使用require指令来载入http模块，并将实例化的HTTP赋值给变量http

var http=required ("http");

