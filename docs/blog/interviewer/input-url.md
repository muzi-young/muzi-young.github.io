# 从浏览器输入url的过程？

- 1.dns解析，解析IP地址，客户端和服务器建立tcp连接（三次握手），发送http请求；

- 2.server端接收HTTP请求，处理并返回；

- 3.客户端接收返回数据，处理数据并渲染页面执行js。

- 443是https的默认端口  80是http的默认端口


三次握手：

- 客户端询问服务器是否可用

- 服务器告诉客户端可用

- 客户端告诉服务器开始用了
