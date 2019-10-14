# canvas的基本使用

## 1.使用步骤 

>在html中写canvas标签

```javascript
<canvas id="myCanvas" width="306" height="166" style="border:1px solid #000000"></canvas>
```

>使用js对画布进行操作

```javascript
var c=document.getElementById("myCanvas");
//创建 context 对象
var ctx=c.getContext("2d");
//绘制一个红色的矩形
ctx.fillStyle="#FF0000";
//fillRect(x,y,width,height) 方法定义了矩形当前的填充方式。
ctx.fillRect(0,0,150,75);
```

>绘制线条

```javascript
//定义线条开始坐标
ctx.moveTo(0,0);
 //定义线条结束坐标
ctx.lineTo(200,100);
ctx.stroke();
```

> 绘制圆

```javascript
//单纯的画圆
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);
ctx.stroke();
//画有颜色的圆
cv.beginPath();
cv.arc(110,80,5,0,2*Math.PI);
// 改变线条的颜色
//cv.strokeStyle='#9af300';
cv.closePath()
cv.fillStyle = '#9af300';
cv.strokeStyle = '#9af300';
cv.lineWidth = 2;
cv.fill();
cv.stroke();

```

>绘制文本

```javascript
// 设置字体
context.font = "Bold 50px Arial";
// 设置对齐方式
context.textAlign = "left";
// 设置填充颜色
context.fillStyle = "#005600";
// 设置字体内容，以及在画布上的位置
 context.fillText("老马!", 10, 50);
// 绘制空心字
context.strokeText("blog.itjeek.com!", 10, 100);
```

> 画三角形

```javascript
//通过id获得当前的Canvas对象
var canvasDom=document.getElementById("demoCanvas");
//通过Canvas Dom对象获取Context的对象
var context = canvasDom.getContext("2d");
context.beginPath(); // 开始路径绘制
context.moveTo(20, 20); // 设置路径起点，坐标为(20,20)
context.lineTo(200, 200); // 绘制一条到(200,20)的直线
context.lineTo(400, 20);
context.closePath();
context.lineWidth = 2.0; // 设置线宽
context.strokeStyle = "#CC0000"; // 设置线的颜色
context.stroke(); // 进行线的着色，这时整条线才变得可见
```

> 线性渐变

```javascript
// 创建渐变
var grd=ctx.createLinearGradient(0,0,200,0);
grd.addColorStop(0,"red");
grd.addColorStop(1,"white");
 
// 填充渐变
ctx.fillStyle=grd;
ctx.fillRect(10,10,150,80);
```

> 给填充颜色的实心圆设置透明度

```javascript
ctx.strokeStyle = 'rgba(102, 112, 147, 0.7)';
```

## canvas的基本使用

### 1.创建一个画布（canvas）

```javascript
//创建一个canvas，给一个id方便js操作
<canvas id="myCanvas" width="300" height="300"></canvas>
```

### 2.获取画布节点

```javascript
let myCanvas = document.getElementById("myCanvas");
```

### 3.通过画布节点区获取画笔

```javascript
let pen = myCanvas.getContext("2d");
```

## 实心矩形

默认背景为黑色

```javascript
// pen.fillRect(x, y, widtd, height);//左上角坐标（x,y） 宽高
pen.fillRect(0, 0, 100, 100);
```

### 清除

```javascript
//清除一个矩形(起点坐标为50，50，清楚宽高为50的一个矩形)
pen.clearRect(50, 50, 100, 100);
//清空画布（起点坐标为0，0，清楚宽高为画布的宽高的一个矩形）
pen.clearRect(0, 0, myCanvas.width, myCanvas.height);
```

> 通常一个画布中不止一个图形，这就需要很多样式，不同的图形之间的样式，包括背景颜色、宽度等等都会相互受影响，就用到save、beginPath、restore，这三个方法。
> 1.关于 save() ：Canvas状态存储在栈中，每当save()方法被调用后，当前的状态就被推送到栈中保存。
> 2.关于beginPath():清空之前所有的容器路径。
>
> 3.关于restore()：每一次调用 restore 方法，上一个保存的状态就从栈中弹出，所有设定都恢复(类似数组的 pop())。

```javascript
// 1、获取画布节点
let myCanvas = document.getElementById("myCanvas");
 // 2、通过画布节点区获取画笔
let pen = myCanvas.getContext("2d");
        
// 共有的样式写在开头，能作用到每一个图形
pen.save();
//样式
pen.beginPath();
//图形的绘制
pen.restore(); 
```

### 动画的基本效果

> 1. 移动
>    pen.translate(x,y) 横向移动距离，纵向移动距离 实际上是移动画布的0，0点，连续使用有叠加的效果
> 2. 旋转
>    // pen.rotate(50 * Maih.PI / 180); 弧度 也是以画布0，0点旋转
> 3. 缩放
>
> ​        pen.scale(0.5,0.5) 以画布0，0点缩放

```javascript
// 示例：
let i = 0;
setInterval(function () {//不停的去绘制一个图案
	pen.clearRect(0, 0, myCanvas.width, myCanvas.height);//每绘制一次就清空一次画布
	i++;
	pen.save();
	pen.translate(250, 250);
	//样式
	pen.rotate(i * Math.PI / 180);
	pen.beginPath();
	//图形的绘制
	pen.fillRect(-50, -50, 100, 100)
	pen.restore();
}, 10);
```

