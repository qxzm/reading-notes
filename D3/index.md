## D3



### 一、SVG基础

##### svg预定于了7种形状元素，分别是

| 图形          | 标签               | 参数                                                         |
| ------------- | ------------------ | ------------------------------------------------------------ |
| 矩形          | rect               | **x**: 左上角x坐标<br />**y**: 作案上交y坐标<br />**width**：矩形的宽度<br />**height**： 矩形的高度<br />**rx**： 对于圆角矩形，指定椭圆在x方向的半径<br />**ry**： 对于圆角矩形，指定椭圆在y方向的半径 |
| 圆形          | circle             | **cx**：圆心的x坐标<br />**cy**：圆心的y坐标<br />**r**：圆的半径 |
| 椭圆          | ellipse            | **cx**：圆心的x坐标<br />**cy**：圆心的y坐标<br />**rx**：椭圆的水平半径<br />**ry**：椭圆的垂直半径 |
| 线段          | line               | **x1**: 起点的x坐标<br />**y1**: 起点的y坐标<br />**x2**: 终点的x坐标<br />**y2**: 终点的y坐标 |
| 多边形 / 折线 | polygon / polyline | **position**：一系列的点坐标                                 |
| 路径          | path               | **d**： 添加路径，如下<br /><br />**移动类**<br />    **M** = moveto: 将画笔移动到指定坐标<br />**直线类**<br />    **L** = lineto：画直线到指定坐标<br />    **H** = horizontal lineto：画水平直线到指定坐标<br />    **V** = vertical lineto：画垂直直线到指定坐标<br />**曲线类**<br />    **C** = curveto：画三次贝塞尔曲线 经 两个指定控制点到达终点坐标<br />    **S** = shorthand / smooth curveto：与前一条三次贝塞尔曲线相连，第一个控制点为前一条曲线第二个控制点的对称点，只需要输入第二个控制点和终点，即可以绘制一个三次贝塞尔曲线<br />    **Q** = quadiratic Bezier curveto：画二次贝塞尔曲线 经一个指定控制点到终点坐标<br />    **T** = shorthand / smooth quadratic Bezier curveto：与前一条二次贝塞尔曲线相连，控制点为前一条二次贝塞尔曲线控制点的对称点，只需要输入终点，即可绘制一个二次贝塞尔曲线<br />**弧线类**<br />    **A** = elliptical arc：画椭圆曲线到指定坐标<br />        **rx**： 椭圆x方向的半轴大小<br />        **ry**： 椭圆y方向的半轴大小<br />        **x-axis-rotation**：椭圆的x轴与水平轴顺时针方向的夹角<br />        **large-arc-flag**：有两个值（1：大角度弧线、0：小角度弧线）<br />        **sweep-flag**：有两个值（1：顺时针到终0：逆时针到终点）<br />        **x**：终点x坐标<br />        **y**：终点y坐标<br />**闭合类**<br />    **Z** = closepath: 绘制一条直线连接终点和起点，用来封闭图形<br /><br />**PS**（上述命令用大写英文字母表示坐标中的绝对坐标，用小写英文字母则表示相对 *当前画笔* 坐标） |
| 文字          | text               | **x**：文字位置的x坐标<br />**y**：文字位置的y坐标<br />**dx**：相对于当前位置在x方向上的平移的距离（正右负左）<br />**dy**：相对于当前位置在y方向上的平移的距离（正下负上）<br />**textLength**：文字的显示长度（不足则拉长，足则压缩）<br />**rotate**：旋转角度（正顺时针， 负逆时针） |



##### 样式

样式可以使用以下属性，也可以指定css 或者 style

| 参数             | 说明                                          |
| ---------------- | --------------------------------------------- |
| fill             | 填充色，改变文字的text的颜色也用这个          |
| stroke           | 轮廓线的颜色                                  |
| stroke-width     | 轮廓线的宽度                                  |
| stroke-linecap   | 轮廓线头断电的样式，圆角、直角等              |
| stroke-dasharray | 虚线的样式                                    |
| opacity          | 透明度0-1                                     |
| font-family      | 字体                                          |
| font-size        | 字体大小                                      |
| font-width       | 字体粗细，有normal，bold，bolder，lighter可选 |
| font-style       | 字体的样式，斜体等                            |
| text-decoration  | 上划线，下划线等                              |

```html
<svg width=500 height=500 version=1.1 xmlns="http://www.w3.org/2000/svg">
  <path d="M30, 100 L270, 300 M30, 100 H270 M30, 100 V300"
        style="stroke:black;stroke-width:3"></path>
</svg>
<svg>
  <path d="M30, 100 C100, 320 190, 20 270, 100"></path>
</svg>
<svg>
  <path d="M100, 200 a200, 150 0 1, 0 150, -150 Z"></path>
</svg>
<svg>
  <text x=200 y=150 dx=-5 dy=5 textLength=90>
    D3 first <tspan fill="red">SVG</tspan> test
  </text>
  <text x=200 y=250 dx=-5 dy=5 textLength=190>
    D3 first <tspan fill="red">SVG</tspan> test
  </text>
</svg>
```



##### 标记

> 标记 marker 是一个重要的概念，能依附于path, line, polyline, polygen元素上，标记marker卸载defs中，defs用于定义可重复使用的图形元素

| 属性                       | 说明                                                         |
| -------------------------- | ------------------------------------------------------------ |
| viewBox                    | 坐标系的区域                                                 |
| refX / refY                | 在viewBox内的基准点， 绘制时此点在直线端点上                 |
| markerUnits                | 标记大小的基准， 有两个值（strokeWidth 线的宽度，userSpaceOnUser 线前端的大小） |
| markerWidth / markerHeight | 标识的大小                                                   |
| orient                     | 绘制方向，可设定为 auto 和 角度值                            |
| id                         | 标识的id号                                                   |

![marker的参数](img/d3-marker参数.png)

```html
<svg>
  <defs>
    <marker id=arrow
            markerUnits=strokeWidth
            markerWidth=12
            markerHeight=12
            viewBox="0 0 12 12"
            refX=6
            refY=6
            orient=auto
            >
      <path d="M2,2 L10,6 L2,10 L6,6 L2,2" style="fill:black"></path>
    </marker>
  </defs>
  <line x1=0 y1=0 x2=200 y2=50
        stroke=red
        stroke-width=2
        marker-end="url(#arrow)"></line>
  <path d="M20,70 T80,100 T160,80 T200,90"
        fill="white"
        stroke=red
        stroke-width=2
        marker-start="url(#arrow)"
        marker-mid="url(#arrow)"
        marker-end="url(#arrow)"></path>
</svg>
```



##### 滤镜

> 滤镜 filter 和marker一样也是定义于defs。种类很多，都以fe开头，如feMorphology, feGaussianBlur, feFlood

```html
<svg>
  <defs>
    <filter id="GaussianBlur">
      <feGaussianBlur in="SourceGraphic" stdDeviation=2></feGaussianBlur>
    </filter>
  </defs>

  <rect x=100 y=100 width=150 height=100 fill=blue></rect>
  <rect x=300 y=100 width=150 height=100 fill=blue
        filter="url(#GaussianBlur)"></rect>
</svg>
```



##### 渐变

> svg中有linearGradient 线性渐变和 radialGradient 放射性渐变，定义在defs

```html
<svg>
  <defs>
    <linearGradient id="myGradient" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#f00"></stop>
      <stop offset="100%" stop-color="#0ff"></stop>
    </linearGradient>

    <linearGradient id="myGradient2" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" stop-color="#f00"></stop>
      <stop offset="100%" stop-color="#0ff"></stop>
    </linearGradient>

    <linearGradient id="myGradient3" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#f00"></stop>
      <stop offset="100%" stop-color="#0ff"></stop>
    </linearGradient>
  </defs>

  <rect x=100 y=100 width=150 height=100 fill="url(#myGradient)"></rect>
  <rect x=250 y=100 width=150 height=100 fill="url(#myGradient2)"></rect>
  <rect x=100 y=200 width=150 height=100 fill="url(#myGradient3)"></rect>
</svg>
```



### 二、选择集与数据

##### 选择元素

选择器是css选择器或者DOM API所选择的元素

* **select**：匹配选择器的第一个元素
* **selectAll**：匹配选择器的所有元素



##### 选择集

上述返回为选择集（selection），其操作如下

* selection.**empty**()：判断选择集是否为空
* selection.**node**()：返回第一个非空元素，空返回null
* selection.**size**()：返回选择集中的元素个数
* selection.**attr**(name [, value])：设置 或 获取 属性
* selection.**property**(name [, value])：设置 或 获取 属性（attr不生效的， 如文本框的value，复选框的value）
* selection.**classed**(name [, value])：设置 或 获取 选择集的CSS类（value是布尔）
* selection.**style**(name [, value [, priority]])：设置 或 获取 选择集的样式
* selection.**text**([value])：设置 或 获取 选择集的文本内容，不包括内部标签，等同innerText
* selection.**html**([value])：设置 或 获取 选择集的内部html内容，相当于innerHTML

```html
<p>Paragraph 1</p>
<p>Paragraph 2</p>
<p>Paragraph 3</p>
<script>
	var paragraphs = d3.selectAll('p')
  console.log(paragraphs.empty()) // false
  console.log(paragraphs.node()) // <p>Paragraph 1</p>
  console.log(paragraphs.size()) // 3
  
  // classed
  d3.select('p')
    .classed('red', true)
    .classed({red: true, bigSize: true})
    .classed('red bigSize', true)
</script>
```



##### 选择集数据

可添加，插入，删除元素

* selection.**append**(name)：在选择集的末尾添加一个元素，name为元素名称
* selection.**insert**(name [, before])：在选择集中置顶元素前插入一个元素，before是选择器
* selection.**remove**()：删除选择集中的元素



##### 数据绑定

将数据绑定到DOM上

* selection.**datum**([value])：选择集中的每一个元素都绑定相同的数据value
* selection.**data**([values [, key]])：选择集中的每一个元素分别绑定数组values的每一项。key是一个键函数，用于指定绑定数组时的对应规则
  * update：数组长度 = 元素数量
  * enter：数组长度 > 元素数量
  * exit：数组长度 < 元素数量

```javascript
var dataset = [3, 6, 9, 12, 15]
var p = d3.selelct('body').selectAll('p')
var update = p.data(dataset)

console.log(update)
console.log(update.enter())
console.log(update.exit())

// data key调整绑定顺序
var persons = [
  {id: 6, name: 'a'},
  {id: 9, name: 'b'},
  {id: 3, name: 'c'}
]
p.data(persons, function (d) {
  return d.id
}).text(function (d) {
  return d.id + ' : ' + d.name
})

// 输出
// <p> 3: c </p>
// <p> 6: a </p>
// <p> 9: b </p>
```



##### 选择集的处理

* **update**部分直接使用
* **enter**部分可以 selection.enter().append() 的形式添加足够的元素
* **exit**部分是删除 selection.exit().remove()



##### 选择集的处理 二

* **filter **过滤器

  ```javascript
  selection.filer(function (d, i) {
  	return d > 20
  })
  ```

* **sort** 改变顺序

  ```js
  selection.sort(function (a, b) {
    return b - a // 递减排序
  })
  ```

* **each** 对各元素分别处理

  ```js
  var persons = [
    {id: 1, name: 'zhang san'},
    {id: 2, name: 'li si'}
  ]
  
  var p = d3.select('body').selectAll('p')
  p.data(persons).each(function (d, i) {
    d.age = 20
  }).text(function (d, i) {
    return d.id + ' ' + d.name + ' ' + d.age
  })
  ```

* **call** 允许将选择集自身作为参数， 传递给某一个函数

  ```js
  function myfun (selection) {
    selection.attr('name', 'value')
  }
  
  d3.selectAll('div').call(myfun)
  // 等同
  myfun(d3.selectAll('div'))
  ```



##### 数组的处理