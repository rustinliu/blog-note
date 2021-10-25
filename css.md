## 版本问题

* 最广泛的版本 CSS2.1，最新版本CSS3（分块升级）
* 判断浏览器支持CSS情况，[CAN I use](http://www.caniuse.com)
* 标准的制定者是W3C，搜索 CSS3 spec可以找到并查看最新标准，目前CSS2.1有人工翻译的版本可供查阅参考

## 语法

* 选择器 {

  属性名：属性值;

  /* 注释 */

  }

* at 语法

  @charset "UTF-8";

  @import url(2.css);  这个是CSS语法

  @media(min-width:100px) and (max-width:200px) {

  语法一

  }

  * @charset必须放在第一行
  * 前两个at语法必须以;结束
  * charset是字符集，但UTF-8是字符编码encoding，这是历史遗留问题，这里确定的是 **文件编码**

## 文档流

* 流动方向
  * inline元素从左往右，到最右边换行
  * block元素从上往下，每一个都另起一行
  * inline-block也是从左往右
* 宽度
  * inline宽度为内部inline元素的和，不能用width指定
  * block默认自动计算宽度(**这里需要说明一点就是自动就算宽度不代表就是100%，指的是填充满，比如有边框的情况，任何尽量不要让宽度设置为100%**)，可与width指定
  * inline- block结合前两者特点，可用width
* 高度
  * **inline高度由line- height间接确定**，和height无关
  * block高度由内部文档流元素决定，可以是设height
  * Inline-block和block类似，可以设置height
* 脱离文档流
  * 浮动 定位

## 盒模型

* 两个模型
  * 分别是什么
    * content-box 内容盒 width只包含content的宽度
    * border-box 边框盒 width包含border、padding、border的宽度
  * 公式
    * content-box width = 内容宽度
    * border-box width = 内容宽度+padding * 2+border * 2

* margin合并（**只发生在上下 margin**）
  * 那些情况会合并，
    * 兄弟margin合并
    * 父子margin合并
  * 如何阻止合并
    * 兄弟合并是符合预期的
    * 兄弟合并可以用inline- block消除
    * 父子合并解决
      * 父元素设置border/padding
      * 父元素设置overflow:hidden
      * display:flex

## 单位

* 长度单位
  * px
  * em 相对于自身font-size的倍数
  * 百分数
  * 整数
  * rem
  * vw,vh
* 颜色
  * 十六进制
  * RGBA
  * HSL颜色

