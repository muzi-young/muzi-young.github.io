# SVG 学习笔记

最近刚开始学习数据可视化的知识，以下是学习svg的记录：

## 1.svg坐标系：

svg坐标系：是以左上角开始 x =0，y= 0,坐标是向右向下移动

**svg元素可以相互嵌套**

## 2.svg元素：（所有元素除了g都有stroke和fill）

***g：用来将图形进行分组***

> g元素没有X和Y属性 <br />
>  样式由它子元素继承

***rect：矩形（边框和填充都在style样式中)***

> e-opacity: 边框的透明度 <br />
>  填充：
>
> > fill：填充的颜色（十六进制或者none）<br />
> >  fill-opacity：透明度

*circle：圆形（同rect一样有边框和填充）*

> 圆心在cx,cy处，半径为r

*ellipse：椭圆形（同rect一样有边框和填充）*

> 椭圆的圆心在cx，cy <br />
>  rx：椭圆在x轴上的半径 ry:椭圆在y轴上的半径 <br />
>  rx = ry 则为圆形

 *line：绘制直线*

> 起点坐标 x1,y1 <br />
>  终点坐标 x2,y2 <br />
>  可以设置stroke:颜色(十六进制);和粗细

*Polyline：折线*

> 每个点都是points属性中的x,y值 `polyline points = "10,0  60,0 75,50"/polyline` <br />
>  可以设置填充fill：颜色，不设置默认黑色

*polygon：绘制多边形*

> （至少三个点 两点就变成一条直线了）（同rect一样有边框和填充） <br />
>  两点之间绘制一条线 几个绘制几条线 `polygon points = "10,0  60,0 35,50"/polygon` 这就是一个三角形

*path：用于绘制组合线条、弧线、曲线等填充或非填充的高级形状*

> 所有绘图都在d属性中指定 <br />
>  M发出“移至”命令 <br />
>  A或a发出“弧”命令 
>
> > rx（x方向上的半径),第二个参数是ry（y轴的半径） <br />
> >  第三个参数是x-axis-rotation：相对于正常x轴有一定的旋转的角度 一般为0 <br />
> >  第四和第五个参数分别是large-arc-flag和sweep-flag <br />
>  A发出命令后跟的绝对点 
>
> > a发出命令后跟的是相对点 （m后跟的点+相对点的位置）
>
>  L或l发出“线段”命令 
>
> > L发出命令后跟的绝对点 <br />
> >  l发出命令后跟的是相对点 （m后跟的点+相对点的位置）<br />
> >  移动虚拟画笔绘图：路径形状始终会从虚拟画笔的最后一个点绘制到一个新点
>
>  Q或q:绘制二次贝塞尔曲线(和线段一样) 有一个控制点 <br />
>  C或者c:绘制三次贝塞尔曲线 有两个控制点 <br />
>  Z或者z可用于闭合路径的快捷命令（大小写命令无区别）代表闭合 <br />
>  填充路径fill 可以有标记

*marker：标记线段或路径的开始、中间和结束*

> `marker`元素必须嵌套在`defs`元素内 `defs`元素内通常保存一组可重用的SVG图片定义。 <br />
>  两个`marker`元素定义了之前图片中展示的开始和结束标记 <br />
>  使用CSS属性`marker-start`和`marker-end`引用这两个`marker`元素 <br />

```
marker id="markerCircle" markerWidth="8" markerHeight="8" refX="5" refY="5"/marker
```
> 宽度`markerWidth`和高度`markerHeightid`属性是用来在`path`元素中对其引用 <br />
>  `refX`和`refY`坐标集被用作参考点 此标记的路径的开始位置 <br />
>  在中css样式中引用 `marker-start:url(#标记id)` <br />
>  `line`、`polyline`和`polygon`元素也可以使用标记 <br />
>  标记单位 `makerUnits`设置为`strokeWidth`

*text:绘制文本*

> 第一个字在x，y处绘制 x确定了左侧的边缘 y是文本的底部 <br />
>  文本瞄点text-anchor  <br />
>  `start、middle、end` <br />
>  描边`stroke` 填充`fill` <br />
>  字母之前间距`letter-spacing`  字距`kerning`单词的间距;(文本的词距)`word-spacing` <br />
>  无自动换行 <br />
>  垂直文本`writing-mode` 但如果不想让其旋转 `glyph-orientation-vertical：0` （不设置默认旋转90°） <br />
>  文本方向direction：`ltr`：从左到右；`rtl`：从右到左 <br />
>  添加样式： <br />
>  ![img](https://cdn.nlark.com/yuque/0/2021/png/2861422/1638603277648-e5c532d0-90f8-4725-887e-5acf7a5a2494.png)						
>  textLength:设置文本的长度 <br />
>  可以搭配使用的元素`tspantreftextpath`

*tsapn:用来绘制多行文本*

> 垂直定位：dy <br />
>  水平定位：dx <br />
>  带基线偏移`baseline-shift`的上标super和下标sub <br />

*tref:用来引用`defs`的文本*

 `tref xlink:href="#id名"/`

*textpath:用于沿着路径布局文本*

> 在`defs`元素内的path中定义id 在textpath用xlink:href引用 `textpath xlink:href="#id名"/`

*switch:在SVG图片上绘制文本*

> 展示`switch`元素中相应的`g`元素中用systemLanguage属性定义语言的种类

*image:SVG图片中嵌套图片*

 xlink:href="图片的路径"

*a:SVG图片中创建链接*

> `a`元素上的xlink:show属性 <br />
>  new 新窗口中打开链接 <br />
>  replace  替换当前窗口 <br />
>  使用图形作为链接 写在`a/a`之间

*defs:嵌套了在SVG图片中可重用的定义*

> 在`def`元素内定义的图形不会展示在SVG图片上。必须通过`use`元素来引用 <br />
>  引用`g`元素前，必须设置其id属性

*use:元素通过xlink:href属性引用`g`元素*

> `use`元素通过x和y属性指定显示可重用图形的位置  g元素中的图形位于0,0处 <br />
>  可以嵌套任何形状元素（rect，line等）和g、symbol

*symbol:元素用来定义可重用的标记*

> 嵌套在`symbol`中的形状不会显示，除非其被`use`元素引用 <br />
>  `symbol`元素需要一个id属性供后面的`use`元素引用 <br />
>  preserveAspectRatio <br />
>  viewBox <br />
>  `g`元素不能包含这两个属性 <br />
>  `use`：在SVG文档的任何位置复用图形 <br />
>  包括`g`元素和`symbol`元素 <br />
>  复用的图形可以被定义在`defs`元素内或者外面（`symbol`内)
>  位置x="" y=""

## 3.CSS-级联样式表
- 利用具体的样式属性
- 使用style属性
- 使用内联样式表 写在`svg/svg`中
- 使用外联样式表 
```javascript
<?xml-stylesheet type="text/css" href="svg-stylesheet.css" ?>
```
-  在HTML页面使用样式表


## 4.svg的效果
*1.轮廓stroke*

> `stroke-width`:宽度 <br />
>  `stroke-linecap`：渲染方式 <br />
>  `butt` 结尾处截断的线头 <br />
>  `square` 超过线段结尾一点 <br />
>  `round` 圆弧线头 <br />
>  `stroke-linejoin` 两条线之间的连接 <br />
>  `miter` <br />
>  `round` <br />
>  `bevel` <br />
>  `stroke-miterlimit` 限制两条线相交的点之间的距离 <br />
>  `stroke-dasharray`:虚线轮廓 <br />
>  `stroke-dashoffset` 开始点 <br />
>  `stroke-opacity `轮廓透明度 

*2.填充fill*

> `fill-opacity` 填充透明度 <br />
>  `fill-rule `填充复杂图形 <br />
>  `nonzero` 内部 <br />
>  `evenodd` 外部 

*3.视口和视图框*

> 视口：可见区域 <br />
>  视图框：`viewBox`属性 参数 x y width height 

*4.动画  嵌套到元素内*

> set元素 定时间间隔过去后将属性设置为某个值 <br />
>  特定时间设置属性的值， <br />
>  属性的名称`attributeName`属性。 <br />
>  在to属性中指定将为其设置的值， <br />
>  设置属性值的时间在begin属性中指定。 <br />
>  要设置`attributeType = "XML"` <br />
>  animate 用来为SVG形状的属性添加动画 <br />
>  `fill="remove"` 当动画结束时，动画属性被设置为原始值 <br />
>  `fill = "freeze"` 当动画结束时，动画属性保持最终的值不变 <br />
>  `repeatCount="indefinite"` 动画无限重复 <br />
>  `animateTransform` 形状的transform属性设置动画 <br />
>  type属性 动画的类型 scale 缩放 rotate 旋转transform平移 <br />
>  `animateMotion` 使形状沿着路径的线路移动 <br />
>  path属性 路径指令 和path操作一样 <br />
>  同步一个动画的开头到另一个动画的结尾 写两个`animate  /` <br />
>  设置第一个animate 的id <br />
>  设置begin="第一个动画的id名.end" <br />
>  重复动画：有两个属性可以用来实现重复效果的动画 <br />
>  repeatCount <br />
>  设置一个数值，动画会重复固定数值的次数 <br />
>  indefinite 无限执行动画 <br />
>  repeatDur 其指定动画重复的持续事件。 <br />
>  设置为indefinite 无限执行动画 

*5. 脚本 使用JavaScript为SVG添加脚本*

> 操作svg和操作HTML元素一样 <br />
>  获取svg ：`document.getElementById()` <br />
>  改变属性值 `setAttribute()` 包括`style属性` <br />
>  获取属性值 `getAttribute()` <br />
>  通过元素的`style属性`引用给定的CSS属性来更改SVG元素的CSS属性 

*6.变换*

- `translate()` 平移:x和y作为参数传递给`translate()`函数

- `rotate()` 旋转 :函数默认绕点0,0旋转形状、如果不想绕0,0旋转 就把x,y传入`rotate()` 函数中 `transform：rotate(度数,x,y)`度数为代表逆时针旋转

- `scale()` 缩放:两个参数 大于1为放大 小于1为缩小(x ：x轴上缩放;y ：y轴上缩放)

- `skew() `某个指定的角度偏斜给定的轴。
  - `skewX()`函数使x轴倾斜
  -  `skewY()`函数y轴倾斜

- `matrix()` 矩阵 **只能指定前6个值**

- `cos(a)`和`sin(a)`的值必须在被插入矩阵之前被预先计算。参数a是旋转的角度

*7. 渐变*

> 线性渐变`linearGradient`  <br />
>  嵌套在`defs`元素内 <br />
>  在其他元素内使用style属性里的CSS属性fill（`fill: url(#myLinearGradient1)`）引用线性渐变。 <br />
>  嵌套了两个`stop`元素 <br />
>  `offset` 开始和结束的位置 <br />
>  `stop-color` 停止点的颜色 开始改变或者改变到这个颜色 <br />
>  `stop-opacity` 停止点的透明度 <br />
>  放射渐变`radialGradient` 以圆形方式改变 

*8. 填充图案*

> 在`defs`元素内部定义了一个`pattern`元素 <br />
>  要在`pattern`元素上写`id`和`patternUnits="userSpaceOnUse"` <br />
>  从x,y处开始填充  填充大小由`width`，`height`属性确定 <br />
>  在`pattern`中定义填充图形的元素 <br />
>  填充的图形要变换就要在`pattern`上定义`patternTransform`属性 可以写变换函数(旋转、缩放、平移) <br />
>  在其他元素上的css样式中引入id `style:"fill:url(#id名)"`

*9. 剪裁路径 用于根据特定剪裁路径SVG形状*

 在defs中定义`clipPath`

- 矩形剪裁:在`clipPath`中定义(像矩形形状的图案)rect,最后定义的圆通过CSS属性`clip-path`引用`clipPath`的id属性

- 高级剪裁：在`clipPath`中定义`path`（高级剪裁，圆、椭圆、多边形或者自定义路径);
  - 应用于`rect`元素的CSS属性`clip-path`引用`clipPath`的id属性

- 分组剪裁：应用于`g`的的CSS属性`clip-path`引用`clipPath`的id属性，这个分组里面的所有元素都剪裁

- 文本剪裁：除了矩形剪裁，高级路径剪裁还可以文字剪裁，在`clipPath`定义`text`	元素

*10. 遮罩*

> 在defs中定义`mask`元素，`mask`元素中定义遮罩层的形状 <br />
>  在`mask`上定义遮罩元素的id <br />
>  在`rect`上css的mask引用id属性 `style="mask:url(#id名)"` <br />
>  可以在遮罩层使用渐变 <br />
>  先定义渐变 在遮罩中引用渐变 `style="fill:url(#渐变id名)"`