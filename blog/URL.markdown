# IP
## IP的全称是Internet Protocol,中文叫网际协议，是用于分组交换数据网络的一种协议，IP地址，是用于标识发送或者接收数据的设备的一串数字。所以只要我们的设备连接上了互联网，就会拥有至少一个独特的IP地址。
# 端口
## 我们的机器就像麦当劳一样，有很多的窗口去分别提供不同的服务，这些机器的窗口叫做端口(port)，一台机器有65535个端口，提供HTTP服务最好使用80端口，提供HTTPS服务最好使用443端口，提供FTP服务最好使用21端口。
## 其中0到1023端口是留给系统使用的，必须拥有管理员权限后，才能使用这1024个端口。http-server默认使用8080端口。
# 域名
## 域名是对IP地址的别称，我们可以在命令行窗口使用ping命令，查看不同域名对应的IP地址，一个域名可以对应不同的IP地址，叫做负载均衡。一个IP地址可以对应不同域名，这个叫做共享主机。
# DNS
## DNS的全称是Domain Name System，域名系统，是一个将域名和IP地址互相映射的分布式数据库。当在浏览器输入域名之后，浏览器回向通信服务商提供的DNS服务器询问域名所对应的IP地址，当DNS返回IP地址之后，浏览器会对这个地址的80/443端口发送请求。
# URL
## URL的全称是Uniform Resource Locator(统一资源定位符)，是互联网上标准的资源地址。通常的组成形式是：协议+域名或IP地址+端口号+路径+查询字符串+锚点