# HTML5讲义

## 章节标签

* 标题 h1~h6
* 章节 section
* 文章 article
* 段落 p
* 头部 header
* 脚部 footer
* 主要内容 main
* 旁枝内容 aside
* 划分 div

## 全局属性

* class
* Contenteditable 表示可以编辑
* hidden
* id
* style
* tabindex 表示可以用tab进行选择，tab时会按照index递增顺序访问，0为最后一个（不是第一个），-1则为用tab永远无法访问
* title

## 内容标签

* ol + li
* ul + li
* dl + dt + dd
* pre
* hr
* br
* a
* em
* strong
* code
* quote
* blockquote

## HTML重点标签

* a标签
  * 属性
    * herf
      * 网址
        * http://www.google.com
        * Https://www.google.com
        * //www.google.com 无协议打开,建议使用此方式
      * 路径
        * a/b/c 开启服务器后注意此时根目录为开启文件夹
      * 伪协议
        * javascript:代码  现在使用的主要是javascripte:;
        * #id 跳转到指定id位置
        * mailto:邮箱
        * tel:手机号
    * target 
      * _blank
      * _self
      * _top 结合iframe理解
      * _parent 结合ifame理解
    * download 理论上下载
    * rel=noopener
  * 作用
    * 跳转外部页面
    * 跳转到内部锚点
    * 跳转到邮箱或者电话
* table标签
  * 样式
    * table-layout
    * border-collapse
    * boder-spacing
* img标签 **发出get请求，使用一张图片**
  * 属性
    * src
    * alt
    * height 只写数字就可以
    * width 只写数字就可以
  * 事件
    * onload
    * onerror
  * 响应式
    * max-width=100%
  * img是一个可替换元素，也就是说展现效果不由css控制，css可以影响替换元素的位置，但是不能影响可替换元素本身的内容 [可替换元素 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Replaced_element)

* form标签 **发出get或者post请求，然后刷新页面**
  * 属性
    * action
    * autocomplete 
    * method
    * target
  * 事件
    * onsubmit
  * Input:submit和button区别在于button可以包裹其他元素，而input：submit不能，另外一个form内必须有一个submit标签，只有一个button且该button没写type时那么这个button就会有submit的作用
* input标签
  * 验证器

## 其他问题

安装http-sever来打开文件，[http-server的安装和使用 - 简书 (jianshu.com)](https://www.jianshu.com/p/b9f043a2ba94) http-server -c-1(简写hs -c-1)无缓存打开
