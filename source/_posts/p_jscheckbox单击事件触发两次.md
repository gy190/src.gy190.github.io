今天帮群里的朋友看一段代码的时候偶然间遇到一个label的坑，点击label的时候，监听的click事件被执行两次；

具体代码如下：

1 　　<div id="test">
2     　　<input type="checkbox" name="abc" id="abc"/>
3     　　<label for="abc">3423432432432432</label>
4  　　</div>
5  　　<script type="text/javascript">
6     　　document.getElementById("test").onclick = function(ev) {
7         　　console.log(ev.target);
8     　　}
9 　　</script>
在控制台我们可以看到：

触发的事件源分别为input和label；

触发条件很简单：

1、监听的是label和input的上层元素click事件

2、label和input关联（for或者input在label下）

问题原因：：

点击label的时候，事件冒泡一次，同时会触发关联的input的click事件，导致事件再次冒泡

解决方案：

1、不用label（最简单直接粗暴的方法），如果为了语义化或者是个人习惯又不得不用label标签，那就继续往下看

2、咱只认input，判断事件源为input，具体代码如下：

1     document.getElementById("test").onclick = function(e) {
2         var ev = e || window.event;
3         var elm = ev.target || ev.srcElement;
4         if (elm.tagName === 'LABEL') {return;}
5         // do something;
6     }
上面代码受场景限制，即当input和label不关联的时候，点击label不作处理就会出现问题了，所以改进如下：

 1     /**
 2      * 是否包含某id的input后代元素
 3      * @param  {Element}  elm 要判断的元素
 4      * @param  {String}   id  要匹配的id
 5      * @return {Boolean}
 6      */
 7     function hasInput(elm, id) {
 8         for (var i = 0, inputs = elm.getElementsByTagName("input"), len = inputs.length; i < len; i++) {
 9             if (inputs[i].id === id) {return true;}
10         }
11         return false;
12     }
13     /**
14      * 判断某元素下的label是否有关联的input
15      * @param  {Element}  elm    要判断的元素
16      * @param  {Element}  label  label元素
17      * @return {Boolean}
18      */
19     function isLabelhasRelativeInput(elm, label) {
20         if (label.getElementsByTagName("input").length) {
21             return true;
22         }
23         var forT = label.getAttribute("for");
24         var isIE6 = !-[1,] && !window.XMLHttpRequest;// IE6不支持for属性
25         if (forT && hasInput(elm, forT) && !isIE6) {
26             return true;
27         }
28         return false;
29     }
30     document.getElementById("test").onclick = function(e) {
31         var ev = e || window.event;
32         var srcElm = ev.target || ev.srcElement;
33         if (srcElm.tagName === 'LABEL' && isLabelhasRelativeInput(this, srcElm)) {return;}
34         // do something;
35     }
顿时不开心了，代码变的这么长，修正了上述问题，通用性会更强一些了

3：祭出终极解决方案

1     var evTimeStamp = 0;
2     document.getElementById("test").onclick = function(e) {
3         var now = +new Date();
4         if (now - evTimeStamp < 100) {
5             return;
6         }
7         evTimeStamp = now;
8         console.log(2);
9     }
通过事件触发的时间戳来判断，其实和事件冒泡有关的问题都可以通过该方法去处理。安全无公害



