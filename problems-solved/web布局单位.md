**rpx单位是微信小程序中css的尺寸单位** ，`rpx可以根据屏幕宽度进行自适应`。官方推荐微信小程序可以用iPhone6 作为视觉稿的标准。规定屏幕宽为750rpx。如在 iPhone6 上，屏幕宽度为750 px，则共有个750 物理像素，则750 rpx = 375px  = 750 物理像素 例如 : 1rpx = 0.5px = 1物理像素

但是不同iOS设备上，px和rpx换算有些区别：

iphone5 上： 1rpx = 0.42px     1px = 2.34rpx

iphone6 上： 1rpx = 0.5px     1px = 2rpx

iphone6S 上： 1rpx = 0.552px     1px = 1.81rpx

`在不同设备上rpx与px的转换是不相同的，但是宽度的rpx却是固定的，所以可以使用rpx作为单位，来设置布局的宽高，不是所有的单位都适合rpx，字体不适合rpx,会导致不同设备看不清。`

设计稿恰巧是750px,量出宽度是多少，那么你就定义多少rpx，假设设计稿640px宽度则就需要转换一下，你需要转换一下 1px = 750/640 rpx

**微信小程序也支持rem尺寸单位** ，**rem：** 相对单位，可理解为”root em”, 相对根节点html的字体大小来计算，CSS3新加属性，chrome/firefox/IE9+支持。

rem和rpx的换算关系：rem: 规定屏幕宽度为20rem；1rem = (750/20)rpx

在开发中,

1). 需要导入js

```
    (function (doc, win) {  
          var docEl = doc.documentElement,  
            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',  
            recalc = function () {  
              var clientWidth = docEl.clientWidth;  
              if (!clientWidth) return;  
              docEl.style.fontSize = 20 * (clientWidth / 320) + 'px';  
            };  
    
          if (!doc.addEventListener) return;  
          win.addEventListener(resizeEvt, recalc, false);  
          doc.addEventListener('DOMContentLoaded', recalc, false);  
    })(document, window);  
```

2).  根据设计稿宽度算出rem和px直接的转换公式

例如：640px的设计稿，转换公式就是按照上面js中这句而来【docEl.style.fontSize = 20 * (clientWidth / 320) + 'px'】，最终 1rem = 20 x 640/320 + 'px' = 40px;

3).   根据设计稿按照1rem = 40px 对着各个元素进行单位转换

**px：** 绝对单位，页面按精确像素展示

**em：** 相对单位，基准点为父节点字体的大小，如果自身定义了font-size按自身来计算（浏览器默认字体是16px），整个页面内1em不是一个固定的值。

`什么是视口（视窗）在桌面端，视口在桌面端，指的是浏览器的可视区域；而在移动端，它涉及3个视口：Layout Viewport（布局视口），Visual Viewport（视觉视口），Ideal Viewport（理想视口）。视口单位中的“视口”，桌面端指的是浏览器的可视区域；移动端指的就是Viewport中的Layout Viewport。`

**vw：** viewpoint width，视口宽度，1vw等于视窗宽度的1%。

**vh：** viewpoint height，视口高度，1vh等于视窗高度的1%。

vw和vh是css3中的新单位，是一种视窗单位，在小程序中也同样适用。

* 小程序中，窗口宽度固定为100vw，将窗口宽度平均分成100份，1份是1vw
* 小程序中，窗口高度固定为100vh ，将窗口高度平均分成100份，1份是1vh

![](https://ask.qcloudimg.com/draft/2305175/ayirldc3sx.png?imageView2/2/w/1620)图片.png

**vmin：** vw和vh中较小的那个。

**vmax：** vw和vh中较大的那个。

vw, vh, vmin, vmax：IE9+局部支持，chrome/firefox/safari/opera支持，ios safari 8+支持，android browser4.4+支持，chrome for android39支持

其它的单位还有：

%:百分比

in:寸

cm:厘米

mm:毫米

pt:point，大约1/72寸

pc:pica，大约6pt，1/6寸
