URL（Uniform Resource Locator）即**统一资源定位符**，它是WWW的统一资源定位标志，就是指网络地址。这里需要和另外一个概念URI（Uniform Resource Identifier）即**统一资源标识符**区分开，URI是一个用于标识某一互联网资源名称的字符串，URL是URI的子集。

url的组成包括以下内容：

* 协议（必须）：常见的有HTTP（Hyper Text Transfer Protocol）、HTTPS、FTP等，

* 域名/IP（必须）：域名通过DNS被解析成IP

  * 域名（Domain Name）
    * 域名分类：.xxx如.com、.net、.cn等是**顶级域名**，xxx.xxx是**二级域名**（俗称一级域名），www.xxx.xxx是**三级域名**（俗称二级域名），所以xxx.xxx与www.xxx.xxx可能不是同一个网站
  * IP即IP地址（Internet Protocol Address），
    * mac查询内网IP `ifconfig en0`,查询外网IP`curl ifconfig.me`
    * ping用于确定本地主机是否能与另一台主机成功交换(发送与接收)数据包，再根据返回的信息，就可以推断TCP/IP参数是否设置正确，以及运行是否正常、网络是否通畅等。用法`ping xxx`
    * 几个特殊的IP
      * 127.0.0.1表示自己
      * localhost通过hosts指定为自己（mac的hosts位于`/etc/hosts`，可通过修改该文件自定义localhost名称）
  * DNS （Domain Name System域名系统），实现域名到IP的解析服务
    * 使用`nslookup 域名`可以手动进行DNS查询
  * 一个域名可以对应不同IP（实现负载均衡）；一个IP也可以对应不同域名（共享主机）

* 端口（必须，如省略会使用默认端口）

  * 一共有65535个端口，0到1023（2的十次方减1）号端口是留给系统使用的，只有在有管理员权限的情况下才可以使用，其他端口普通用户能使用，比如http-server就默认使用8080端口，详见：[TCP/UDP端口列表 - 维基百科](https://zh.wikipedia.org/wiki/TCP/UDP端口列表#0.E5.88.B01023.E5.8F.B7.E7.AB.AF.E5.8F.A3)
  * **HTTP最好使用80端口**
  * **HTTPS最好使用443端口**
  * **FTP最好使用21端口**

* 路径（非必需）

  实现请求不同的页面

* 查询参数（非必需）

  * 从“？”开始到“#”（或至结束）为止之间的部分为参数部分，又称搜索部分、查询部分。参数间用“&”作为分隔符。

* 锚点（非必需）

  实现打开页面时滚动到该锚点位置。

  * 锚点看起来有中文，但是实际上不支持中文，
  * 锚点无法在network面板看到，因为**锚点不会传给服务器也就是说HTTP请求中不包含锚部分**

## 使用curl命令进行HTTP请求

* curl -v http://baidu.com
* curl -s -v https://www.baidu.com
* curl会重写url，先请求DNS获取IP
* 过程：进行TCP连接，TCP连接成功后，开始发HTTP请求，相应结束后，关闭TCP连接





