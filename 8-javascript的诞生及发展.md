## 起源

JavaScript因为互联网而生，紧随着浏览器的出现而问世。回顾它的历史，就要从浏览器的历史讲起。

此处我们使用时间线的形式，简单回顾这段辉煌的历史：

* 1990年底，欧洲核能研究组织，发明了万维网（World Wide Web）。

* 1992年底，美国国家超级电脑应用中心（NCSA），开发了第一个浏览器，Mosaic。

* 1994年10月，Mosaic通信公司成立，不久后改名为Netscape。开始开发面向普通用户的新一代的浏览器 Netscape Navigator。

* 1994年12月，Navigator发布了1.0版，市场份额一举超过90%。

  > Netscape公司很快发现，Navigator浏览器需要一种可以嵌入网页的脚本语言，用来控制浏览器行为（表单验证）。管理层对这种浏览器脚本语言的设想是：功能不需要太强，语法较为简单，容易学习和部署。
  >  那一年，正逢Sun公司的Java语言问世，市场推广活动非常成功。Netscape公司决定与Sun公司合作，浏览器支持嵌入Java小程序（后来称为Java applet）。
  >  但是，浏览器脚本语言是否就选用Java，则存在争论。后来，还是决定不使用Java，因为网页小程序不需要Java这么“重”的语法。但是，同时也决定脚本语言的语法要接近Java，并且可以支持Java程序。这些设想直接排除了使用现存语言，比如Perl、Python和TCL。

* 1995年，Netscape公司雇佣了程序员**Brendan Eich**开发这种网页脚本语言。

  > 但是，他对Java一点兴趣也没有。为了应付公司安排的任务，他只用10天时间就把Javascript设计出来了。
  >
  > 
  >
  > 由于设计时间太短，语言的一些细节考虑得不够严谨，导致后来很长一段时间，Javascript写出来的程序混乱不堪。如果Brendan Eich预见到，未来这种语言会成为互联网第一大语言，全世界有几百万学习者，他会不会多花一点时间呢？
  >
  > 总的来说，他的设计思路是这样的：
  >
  > （1）借鉴C语言的基本语法；
  >
  > （2）借鉴Java语言的数据类型和内存管理；
  >
  > （3）借鉴Scheme语言，将函数提升到"第一等公民"（first class）的地位；
  >
  > （4）借鉴[self语言](https://en.wikipedia.org/wiki/Self_(programming_language))，使用基于原型（prototype）的继承机制。
  >
  > 在名称方面，JavaScript一开始被命名为Mocha（摩卡），然后经历了Mocha=>LiveScriot>JavaScript的过程。

* 1996年8月互联网巨头微软公司进入浏览器领域，推出JScript，和NetScript公司开始争夺博主地位。同年11月，Netscape公司决定将JavaScript提交给国际标准化组织ECMA（European Computer Manufacturers Association）

  > 希望JavaScript能够成为国际标准，以此抵抗微软。

* 1997年7月，ECMA组织发布262号标准文件（ECMA-262）的第一版，规定了浏览器脚本语言的标准，并将这种语言称为ECMAScript。这个版本就是ECMAScript 1.0版。

  > 之所以不叫JavaScript，一方面是由于商标的关系，Java是Sun公司的商标，根据一份授权协议，只有Netscape公司可以合法地使用JavaScript这个名字，且JavaScript已经被Netscape公司注册为商标，另一方面也是想体现这门语言的制定者是ECMA，不是Netscape，这样有利于保证这门语言的开放性和中立性。因此，ECMAScript和JavaScript的关系是，前者是后者的规格，后者是前者的一种实现。在日常场合，这两个词是可以互换的。

## JavaScript的兴起

* 2004年愚人节时，杀手级应用Gmail出现，之前人们认为网页只能看新闻和图片，Gmail的出现让用户和开发者眼前一亮
* 2005年，Jesse将谷歌用到的技术命名为AJAX，从此前端技术正式出现。在此之前网页开发是后端设计师完成。
* 2006年，JQuery发布，目前最长寿的JS库，后十年JQuery大放异彩，直到IE不行了，JQuery才稍微降温。（JQuery能让代码在IE、Firefox、谷歌等都不报错）

##  JavaScript的爆发

* V8引擎
  * Chrome的JS引擎是V8
  * 2009年，Ryan基于V8创建了Node.js
  * 2010年，Isaac基于Node.js写了npm
  * 至此，js可以脱离浏览器运行了
  * 2010年，TJ受到Sinatra启发，发布了Express.js。用它可以代替java等做一个后端完整的服务器
  * 爆发：React、VUE等出现

## ECMAScript版本发展

* 时间线：
  * 1997年6月，第一版ECMAScript发布
  * 1999年12月，第三版发布，该版使用最广泛
  * 第四版，流产
  * 2009年12月，第五版发布，增加了一些功能
  * 2015年6月，第六版发布，新浏览器都支持这一版本，之后每年发布一版，版本号以年份命名
    * JS与ECMAScript关系：
      ECMAScript写在纸上的标准，JS是浏览器实现
      纸上标准落后于浏览器，先实现再写进标准