## 一、jQuery使用：

### 1.本地引入

~~~html
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
~~~

### 2.CDN远程引入

~~~html
<script src="http://code.jquery.com/jquery-migrate-1.2.1.min.js"></script>
~~~

### 3.使用jQuery

**方式一：**

~~~
<head>
  <meta charset="UTF-8">
  <title>jQuery</title>
  <script src="../JS/jquery-3.5.1.js"></script>
  <script type="text/javascript">
      $(function () {
        
      });
  </script>
</head>
~~~

**方式二：**

~~~
<body>
  <script src="../JS/jquery-3.5.1.js"></script>
  <script type="text/javascript">
  	
  </script>
</body>
~~~

## 二、jQuery 对象和 dom 对象区分

### 1.jQuery 对象与dom对象

① **DOM对象：**

1. 通过getElementById()查询出来的标签对象时Dom对象
2. 通过getElementName()查询出来的标签对象时Dom对象
3. 通过getElementByTagName()查询出来的标签对象是Dom对象
4. 通过createElemnet()方法创建的对象,是Dom对象

**DOM对象Alert出来的效果是:[object HTML 标签名Element]**

②  **jQuery对象：**

1. 通过jQuery提供的API创建的对象，是jQuery对象
2. 通过jquery包装的Dom对象,也是jQuery对象
3. 通过jquery提供的API查询到的对象,是jQuery对象

### 2.jQuery 对象的本质

​	JQuery 对象时dom对象的数组 + JQuery提供的一系列功能函数。

### 3.jQuery 对象和 Dom 对象使用的区别

1. JQuery对象不能使用DOM对象的属性和方法
2. DOM 对象也不能使用JQuery 对象的属性和方法

### 4.DOM 对象 和 jQuery对象互转

* dom 对象转为JQuery对象
  * 先有Dom对象
  *  $(DOM 对象) 就可以转换为jQuery对象
* jQuery 对象转为 dom 对象
  * 先有jQuery对象
  * jQuery 对象(下标)取出相对应的DOM对象

![image-20200719165711650](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200719165719.png)

## 三、jQuery的2把利器

### 1.jQuery函数; $/jQuery

* jQuery向外暴露的就是jQuery函数，可以直接使用
* 当成一般函数使用：$(param)
  * param 是function: 相当于windown.onload = function(文档加载完成的监听)
  * param 是选择器字符串：查找所有的匹配Dom元素，返回包含所有的DOM元素的jQuery对象
  * param 是DOM元素：将DOM元素对象包装成jQuery对象返回$(this)
  * param 是标签字符串： 创建标签DOM元素对象并包装为jQuery对象返回
* 当成对象使用：$.xxx
  * each(obj/arr, function(key, value){})
  * trim(str)

### 2.jQuery对象

* 包含所有匹配的n个DOM元素的伪数组对象
* 执行$()返回的就是jQuery对象
* 基本行为：
  * length/size(): 得到dom元素的个数
  * [index] : 得到指定下标对应的dom元素
  * each(function(index, domEle){}): 遍历所有的dom元素
  * index(): 得到当前dom元素在所在兄弟中的下标

## 四、jQuery 选择器

* 有特定语法规则（CSS选择器）的字符串
* 用来查找某个/些DOM元素：$(selector)

### 1.基本选择器

| 方法                          | 描述                                         |
| ----------------------------- | -------------------------------------------- |
| #id                           | 根据给定的ID匹配一个元素。                   |
| tagName/*                     | 根据匹配标签元素/所有元素。                  |
| .class                        | 根据给定的类匹配元素。                       |
| selector1,selector2,selector3 | 将每一个选择器匹配到的元素合并后一起返回。   |
| selector1selector2selector3   | 将每一个选择器匹配到的元素交集部分一起返回。 |

### 2.层次选择器

​	**找子孙后代，兄弟元素**

| 方法                | 描述     |
| ------------------- | -------- |
| selector1>selector2 | 子元素   |
| selector1 selector2 | 后代元素 |

### 3.过滤选择器

| 方法             | 描述                                       |
| ---------------- | ------------------------------------------ |
| :first           | 获取第一个元素                             |
| :last            | 获取最后个元素                             |
| :eq(index)       | 匹配一个给定索引值的元素                   |
| :lt              | 匹配所有小于给定索引值的元素               |
| :gt              | 匹配所有大于给定索引值的元素               |
| :odd             | 匹配所有索引值为奇数的元素，从 0 开始计数  |
| :even            | 匹配所有索引值为偶数的元素，从 0 开始计数  |
| :not(selector)   | 去除所有与给定选择器匹配的元素             |
| :hidden          | 匹配所有不可见元素，或者type为hidden的元素 |
| :visible         | 匹配所有的可见元素                         |
| [attrName]       | 匹配包含给定属性的元素。                   |
| [attrName=value] | 匹配给定的属性是某个特定值的元素           |

**代码示例 [attrName]：**

~~~html
<div>
  <p>Hello!</p>
</div>
<div id="test2"></div>
~~~

jQuery代码：

~~~
$("div[id]")
~~~

运行结果：

~~~
<div id="test2"></div>
~~~

**代码示例 [attrName=value]：**

~~~html
<input type="checkbox" name="newsletter" value="Hot Fuzz" />
<input type="checkbox" name="newsletter" value="Cold Fusion" />
<input type="checkbox" name="accept" value="Evil Plans" />
~~~

jQuery 代码：

~~~
$("input[name='newsletter']").attr("checked", true);
~~~

运行结果：

~~~
<input type="checkbox" name="newsletter" value="Hot Fuzz" checked="true" />
<input type="checkbox" name="newsletter" value="Cold Fusion" checked="true" />
~~~

### 4.表单选择器

| 方法      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| :input    | 匹配所有 input, textarea, select 和 button 元素              |
| :text     | 匹配所有的单行文本框                                         |
| :checkbox | 匹配所有复选框                                               |
| :radio    | 匹配所有单选按钮                                             |
| :checked  | 匹配所有选中的被选中元素(复选框、单选框等，不包括select中的option) |

**代码示例 【:input】：**

~~~html
<form>
    <input type="button" value="Input Button"/>
    <input type="checkbox" />

    <input type="file" />
    <input type="hidden" />
    <input type="image" />

    <input type="password" />
    <input type="radio" />
    <input type="reset" />

    <input type="submit" />
    <input type="text" />
    <select><option>Option</option></select>

    <textarea></textarea>
    <button>Button</button>

</form>
~~~

jQuery 代码：

~~~
$(":input")
~~~

运行结果：

~~~html
  	<input type="button" value="Input Button"/>
  	<input type="checkbox" />
    <input type="file" />
    <input type="hidden" />
    <input type="image" />

    <input type="password" />
    <input type="radio" />
    <input type="reset" />

    <input type="submit" />
    <input type="text" />
    <select><option>Option</option></select>

    <textarea></textarea>
    <button>Button</button>
~~~

**代码示例 【:checked】：**

~~~html
<form>
  <input type="checkbox" name="newsletter" checked="checked" value="Daily" />
  <input type="checkbox" name="newsletter" value="Weekly" />
  <input type="checkbox" name="newsletter" checked="checked" value="Monthly" />
</form>
~~~

jQuery 代码：

~~~
$("input:checked")
~~~

运行结果：

~~~html
 <input type="checkbox" name="newsletter" checked="checked" value="Daily" />
 <input type="checkbox" name="newsletter" checked="checked" value="Monthly" />
~~~

## 五、属性/文本

* **操作标签的属性, 标签体文本**

| 方法                              | 描述                   |
| --------------------------------- | ---------------------- |
| attr(name) / attr(name, value)    | 读写非布尔值的标签属性 |
| prop(name) / prop(name, value)    | 读写布尔值的标签属性   |
| removeAttr(name)/removeProp(name) | 删除属性               |
| addClass(classValue)              | 添加class              |
| removeClass(classValue)           | 移除指定class          |
| val() / val(value)                | 读写标签的value        |
| html() / html(htmlString)         | 读写标签体文本         |

## 六、CSS模块

### 1. style样式

| 方法                  | 描述                   |
| --------------------- | ---------------------- |
| css(styleName)        | 根据样式名得到对应的值 |
| css(styleName, value) | 设置一个样式           |
| css(多个样式对)       | 设置多个样式           |

**代码示例：**

1. 取得第一个段落的color样式属性的值。

~~~html
$("p").css("color");
~~~

2. 将所有段落的字体颜色设为红色并且背景为蓝色。

~~~html
$("p").css({ color: "#ff0011", background: "blue" });
~~~

	3. 将所有段落字体设为红色

~~~
$("p").css("color","red");
~~~

### 2.位置坐标

| 方法                     | 描述                                       |
| ------------------------ | ------------------------------------------ |
| offset()                 | 读/写当前坐标（原点是页面左上角）          |
| position()               | 读写当前元素的坐标的（原点是父元素左上角） |
| scrollTop()/scrollLeft() | 读/写元素/页面的滚动坐标                   |

**代码示例：**

1. **offset()**

~~~html
<p>Hello</p><p>2nd Paragraph</p>
~~~

~~~html
// jQuery代码
var p = $("p:last");
var offset = p.offset();
p.html( "left: " + offset.left + ", top: " + offset.top );
~~~

**运行结果**

~~~html
<p>Hello</p><p>left: 0, top: 35</p>
~~~

2. **position()**

~~~html
<p>Hello</p><p>2nd Paragraph</p>
~~~

~~~html
// jQuery代码
var p = $("p:first");
var position = p.position();
$("p:last").html( "left: " + position.left + ", top: " + position.top );
~~~

**运行结果：**

~~~html
<p>Hello</p><p>left: 15, top: 15</p>
~~~

3. **scrollTop()**

~~~html
<p>Hello</p><p>2nd Paragraph</p>
~~~

~~~html
// jQuery代码
var p = $("p:first");
$("p:last").text( "scrollTop:" + p.scrollTop() );
~~~

**运行结果：**

~~~html
<p>Hello</p><p>scrollTop: 0</p>
~~~

4. **scrollLeft()**

~~~html
<p>Hello</p><p>2nd Paragraph</p>
~~~

~~~
// jQuery代码
var p = $("p:first");
$("p:last").text( "scrollLeft:" + p.scrollLeft() );
~~~

**运行结果：**

~~~
<p>Hello</p>
<p>scrollLeft: 0</p>
~~~

### 3.尺寸

| 方法                               | 描述                            |
| ---------------------------------- | ------------------------------- |
| width()/height()                   | width/height                    |
| innerWidth()/innerHeight()         | width + padding                 |
| outerWidth()/outerHeight()         | width + padding + border        |
| outerWidth(true)/outerHeight(true) | width + padding + border+margin |

**代码示例：**

1. **width()** 获取第一段的高

~~~html
$("p").height();
~~~

2. **innerWidth()** 获取第一段落内部区域高度。

~~~html
<p>Hello</p><p>2nd Paragraph</p>
~~~

~~~js
// jQuery
var p = $("p:first");
$("p:last").text( "innerHeight:" + p.innerHeight() );
~~~

**结果示例：**

~~~html
<p>Hello</p>
<p>innerHeight: 16</p>
~~~

3. **outerWidth()**

~~~html
<p>Hello</p><p>2nd Paragraph</p>
~~~

~~~js
// jQuery
var p = $("p:first");
$("p:last").text( "outerHeight:" + p.outerHeight() + " , outerHeight(true):" + p.outerHeight(true) );
~~~

**运行结果：**

~~~html
<p>Hello</p><p>outerHeight: 35 , outerHeight(true):55</p>
~~~

## 七、筛选模块

### 1.过滤

​	在jQuery对象内部的元素中找出部分匹配的元素, 并封装成新的jQuery对象返回

| 方法             | 描述                                                   |
| ---------------- | ------------------------------------------------------ |
| first()          | 获取第一个元素                                         |
| last()           | 获取最后个元素                                         |
| eq(index)        | 获取第N个元素                                          |
| filter(selector) | 筛选出与指定表达式匹配的元素集合。                     |
| not(selector)    | 删除与指定表达式匹配的元素                             |
| has(selector)    | 保留包含特定后代的元素，去掉那些不含有指定后代的元素。 |

**代码示例：**

1. **filter(selector)**

~~~html
<p>Hello</p>
<p>Hello Again</p>
<p class="selected">And Again</p>
~~~

~~~js
// jQuery
$("p").filter(".selected")
~~~

~~~html
// 运行结果
<p class="selected">And Again</p>
~~~

2. **not(selector)**

~~~html
<p>Hello</p>
<p id="selected">Hello Again</p>
~~~

~~~js
// jQuery
$("p").not( $("#selected")[0] )
~~~

~~~html
// 运行结果
<p>Hello</p>
~~~

	3. **has(selector)**

~~~html
<ul>
  <li>list item 1</li>
  <li>list item 2
    <ul>
      <li>list item 2-a</li>
      <li>list item 2-b</li>
    </ul>
  </li>
  <li>list item 3</li>
  <li>list item 4</li>
</ul>
~~~

~~~js
// jQuery
$('li').has('ul').css('background-color', 'red');
~~~

### 2.查找

​	查找jQuery对象内部的元素的子孙/兄弟/父母元素, 并封装成新的jQuery对象返回

| 方法               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| children(selector) | 取得一个包含匹配的元素集合中每一个元素的所有子元素的元素集合。（子元素） |
| find(selector)     | 搜索所有与指定表达式匹配的元素。这个函数是找出正在处理的元素的后代元素的方法。（后代元素） |
| preAll(selector)   | 查找当前元素之前所有的同辈元素（前的所有兄弟）               |
| siblings(selector) | 取得一个包含匹配的元素集合中每一个元素的所有唯一同辈元素的元素集合。（所有兄弟） |
| parent()           | 取得一个包含着所有匹配元素的唯一父元素的元素集合。（父元素） |

**代码示例：**

1. **preAll(selector)**  

~~~
<div></div>
<div></div>
<div></div>
<div></div>
~~~

~~~js
// jQuery
$("div:last").prevAll().addClass("before");
~~~

~~~html
// 运行结果
<div class="before"></div>
<div class="before"></div>
<div class="before"></div>
~~~

## 八、文档处理(CUD)模块

### 1.增加

| 方法                      | 描述     |
| ------------------------- | -------- |
| append() / appendTo()     | 插入后部 |
| preppend() / preppendTo() | 插入前部 |
| before()                  | 插到前面 |
| after()                   | 插到后面 |

### 2.删除

| 方法     | 描述                                                  |
| -------- | ----------------------------------------------------- |
| remove() | 从DOM中删除所有匹配的元素。(将自己及内部的孩子都删除) |
| empty()  | 删除匹配的元素集合中所有的子节点。(掏空(自己还在))    |

**代码示例：**

1. **remove()**

~~~html
<p>Hello</p> how are <p>you?</p>
~~~

~~~js
// jQuery
$("p").remove();
~~~

~~~html
// 运行结果
how are
~~~

### 3.更新

| 方法          | 描述                                        |
| ------------- | ------------------------------------------- |
| replaceWith() | 将所有匹配的元素替换成指定的HTML或DOM元素。 |

**代码示例：**

~~~html
<p>Hello</p>
<p>cruel</p>
<p>World</p>
~~~

~~~js
// jQuery
$("p").replaceWith("<b>Paragraph. </b>");
~~~

~~~html
// 运行结果
<b>Paragraph. </b>
<b>Paragraph. </b>
<b>Paragraph. </b>
~~~

## 九、事件模块

### 1.绑定事件

* **eventName(function(){})**
* **on('eventName', function(){})**
  * 常用: **click**,**mouseenter /mouseleave** , **mouseover /mouseout**,**focus/blur**
* **hover(function(){}, function(){})**

### 2.解绑事件

* **off('eventName')**

### 3.事件委托

**理解:** 将子元素的事件委托给父辈元素处理

* 事件监听绑定在父元素上, 但事件发生在子元素上
* 事件会冒泡到父元素
* 但最终调用的事件回调函数的是子元素: event.target

**好处:**

* 新增的元素没有事件监听
* 减少监听的数量(n==>1)

**jQuery的事件委托API**

* 设置事件委托: $(parentSelector).delegate(childrenSelector, eventName, callback)
* 移除事件委托: $(parentSelector).undelegate(eventName)

**代码示例**：

~~~html
<ul>
  <li>11111</li>
  <li>1111111</li>
  <li>111111111</li>
  <li>11111111111</li>
</ul>

<li>22222</li>
<br>
<button id="btn">添加新的li</button>
<br>
~~~

~~~js
// jQuery
$('ul>li').click(function () {
    this.style.background= 'red';
  });
  $('#btn').click(function () {
    $('ul').append('<li>新增的li....</li>');
});
~~~

~~~html
// 运行结果
<ul>
  <li>11111</li>
  <li>1111111</li>
  <li>111111111</li>
  <li>11111111111</li>
  <li>新增的li....</li>
</ul>
~~~

### 4.事件坐标

| 方法          | 描述                 |
| ------------- | -------------------- |
| event.offsetX | 原点是当前元素左上角 |
| event.clientX | 原点是窗口左上角     |
| event.pageX   | 原点是页面左上角     |

**代码示例：**

~~~html
<div class="out">
  外部DIV
  <div class="inner">内部div</div>
</div>

<div class='divBtn'>
  <button id="btn1">测试事件坐标</button>
</div>
~~~

~~~js
$('#btn1').click(function (event) { // event 事件
    console.log(event.offsetX, event.offsetY); // 原点为事件元素的左上角
    console.log(event.clientX, event.clientY); // 原点为窗口的左上角
    console.log(event.pageX, event.pageY); // 原点为页面的左上角
  });
~~~



### 5.事件相关

* 停止事件冒泡: event.stopPropagation()
* 阻止事件的默认行为: event.preventDefault()

**代码示例：**

~~~html
<ul>
  <li>1111</li>
  <li>2222</li>
  <li>3333</li>
  <li>4444</li>
</ul>

<li>22222</li>
<br>
<button id="btn1">添加新的li</button>
<button id="btn2">删除ul上的事件委托的监听器</button>
~~~

~~~js
// jQuery 
// 设置事件委托
  $('ul').delegate('li','click', function(){
    this.style.background = 'red';
  });
  $('#btn1').click(function(){
    $('ul').append('<li>新增的li....</li>');
  });
  // 移除事件委托
  $('#btn2').click(function(){
    $('ul').undelegate('click');
  });
~~~

## 十、JQuery 动画

### 1.基本动画

| 方法     | 描述                     |
| -------- | ------------------------ |
| show()   | 将隐藏的元素显示         |
| hide()   | 将可见的元素隐藏         |
| toggle() | 可见就隐藏，不可见就显示 |

**以上的动画都可以添加参数：**

① 第一个参数就是显示 执行的时间，以毫秒为单位

②第二个参数就是动画的回调函数（动画完成以后调用的函数）

**代码示例：**

~~~html
<style type="text/css">
  * {
    margin: 0px;
  }

  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 10px;
    background: red;
    display: none;
  }
</style>
<body>
<button id="btn1">瞬间显示</button>
<button id="btn2">慢慢显示</button>
<button id="btn3">慢慢隐藏</button>
<button id="btn4">显示隐藏切换</button>

<div class="div1">
</div>

<script src="../JS/jquery-3.5.1.js" type="text/javascript"></script>
<script type="text/javascript">

  var $div1 = $('.div1');
  // 1. 点击btn1, 立即显示
  $('#btn1').click(function () {
    $div1.show();
  });
  // 2. 点击btn2，慢慢显示
  $('#btn2').click(function () {
    $div1.show(1000);
  });

  // 3. 点击btn3, 慢慢隐藏
  $('#btn3').click(function(){
    $div1.hide(1000);
  });
  // 4.点击btn4, 切换显示/隐藏
  $('#btn4').click(function(){
    $div1.toggle(1000);
  });
</script>
~~~

### 2.淡入淡出动画

| 动画      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| fadeln()  | 淡入                                                         |
| fadeOut() | 淡出                                                         |
| fade To() | 在指导时长内慢慢将透明度修改指定的值。0 透明 1 完成可见 0.5 透明 |

~~~html
<style type="text/css">
  * {
    margin: 0px;
  }

  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 10px;
    background: red;
  }
</style>

<body>
<button id="btn1">慢慢淡出</button>
<button id="btn2">慢慢淡入</button>
<button id="btn3">淡出/淡入切换</button>

<div class="div1">
</div>

<script src="../JS/jquery-3.5.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
   需求：
   1. 点击btn1, 慢慢淡出
     * 无参
     * 有参
       * 字符串参数
       * 数字参数
   2. 点击btn3, 慢慢淡入
   3. 点击btn3, 淡出/淡入切换，动画结束时提示“动画结束了”
   */
    var $div1 = $('.div1');

    $('#btn1').click(function(){
      $div1.fadeOut(1000, function(){
        alert('动画完成了！！！！');
      });
    });

    $('#btn2').click(function () {
      $div1.fadeIn();
    });

    $('btn3').click(function () {
        $div1.fadeToggle()
    });
</script>
</body>
~~~

