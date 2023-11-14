这次的开发需求是给列表做个搜索框，输入对应的编号，页面自动滚到所在位置。这里用到了querySelector()和scrollIntoView()两个方法。

## querySelector()

返回文档中匹配指定CSS选择器的一个元素，例如要返回class="item"的元素：`document.querySelector(".item")`

## scrollIntoView()

该方法让当前的元素滚动到浏览器窗口的可视区域内。

### 语法

```javascript
element.scrollIntoView(); // 等同于element.scrollIntoView(true) 
element.scrollIntoView(alignToTop); // Boolean型参数 
element.scrollIntoView(scrollIntoViewOptions); // Object型参数
```

### 参数

#### alignToTop

该参数是一个Boolean值，默认为true。

- true：等同于`scrollIntoViewOptions: {block: "start", inline: "nearest"}`，元素的顶端将和其所在滚动区的可视区域的顶端对齐。
- fales：等同于`scrollIntoViewOptions: {block: "end", inline: "nearest"}`，元素的底端将和其所在滚动区的可视区域的底端对齐

#### scrollIntoViewOptions

- behavior：定义动画过渡效果，"auto"或"smooth"。默认为"auto"。
- block：定义垂直方向的对齐，"start","center","end","nearest"。默认为"start"。
- inline：定义水平方向的对齐，"start","center","end","nearest"。默认为 "nearest"。

## Demo

```javascript
document.querySelector(`.item:nth-child(${index+1})`).scrollIntoView()
```

这样写效果达到了，但是总感觉有点生硬，那就用它的behavior参数试试吧。behavior设置为smooth之后会有个滚动的动画，看着舒服多了。

```javascript
document.querySelector(`.item:nth-child(${index+1})`).scrollIntoView({behavior:"smooth"})
```