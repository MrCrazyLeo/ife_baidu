# ife_baidu
百度前端技术学院的作业代码仓库
---- 
# day 1

- HTML5新增特性：
  - 用于绘画的canvas元素；
  - 用于媒介回放的video和audio元素；
  - 对本地离线存储有更好的支持；
  - 新的特殊内容元素，比如article、footer、header、nav、section
  - 新的表单控件，比如calendar、date、time、email、url、search 
- HTML5的改进：
    - 新元素
    - 新属性
    - 完全支持CSS3
    - Video和Audio
    - 2D/3D制图
    - 本地存储
    - 本地SQL数据
    - Web应用
- 文档类型（DOCTYPE）是用来说明HTML还是XHTML文档以使浏览器准确地渲染。
- meta元素：不显示在页面上，被机器（浏览器、搜索引擎、其他网络服务设备）解析所用。它指定页面描述、所用字符集、作者等内容。
- web语义化是使用恰当的html标签、class类名让页面有良好的结构和含义，方便人和机器理解。

---
# day 2 
- - JS中表示“假”：0、0.0、NaN、""、null和undefined；
  - 表示“真":除上边几个的其他所有，比如字符串零（"0"） 
-
    |    表达式    | 真假  |
    | :----------: | :---: |
    |  10 < "42"   | true  |
    | 10 < "42人"  | false |
    | 10 > "42人"  | false |
    | 10 == "42人" | false |
    |  42 == "42"  | true  |
    | 42 == "42.0" | true  |
    | 42 === 42.0  | true  |
    | 42 === "42"  | false |
- 
  |        类别(优先级降序)        |         运算符         |
  | :----------------------------: | :--------------------: |
  |              括号              |          ( )           |
  |        成员、索引操作符        |         . [ ]          |
  |    方法(函数)调用、对象创建    |         () new         |
  | 逻辑非、负号、自增、自减、类型 |    ! - ++ -- typeof    |
  |          乘、除、取模          |         * / %          |
  |             加、减             |          + -           |
  |      关系比较、实例、包含      | <> <= >= instanceof in |
  |         相等、不等比较         |     ==  != === !==     |
  |             逻辑与             |           &&           |
  |             逻辑非             |         \|  \|         |
  |              赋值              |    = += -= *= /= %=    |

- 变量作用域：
  - 函数外声明为全局变量
  - 函数内声明为局部变量
  - 函数内不声明（没有使用 var 关键字）、直接使用，为全局变量
  - JS变量生命周期在它声明时初始化，局部变量在函数执行完毕后销毁；全局变量在页面关闭后销毁。

---
# day 3
- **DOM**，Document Objuct Model，文档对象模型，是HTML和XML编程接口。
- \<button \>貌似没有data-value这个属性啊，什么鬼。
- Node类型：文档类、元素类、文本类、属性类、内容类

---
# day 4
- display:flex 弹性布局，参考[阮一峰大佬的文章](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
 
- 相对长度<br>
- 
  |单位|描述|
  |:--:|:--|
  |em|它是描述相对于应用在当前元素的字体尺寸，所以它也是相对长度单位。一般浏览器字体大小默认是16px，则2em=32px|
  |ex|依赖于英文字母小x的高度|
  |ch|数字0的高度|
  |rem|根元素(html)的font-size|
  |vm|viewpoint width，视窗宽度，1vw=视窗宽度的1%|
  |vh|viewpoint height，视窗高度，1vh=视窗高度的1%|
  |vmin|vw和vh的较小的那个|
  |vmax|vw和vh中较大的那个|

- 绝对长度
- |单位|描述|
  |:--:|:--|
  |cm|厘米|
  |mm|毫米|
  |in|英寸|
  |px|像素|
  |pt|point|
  |pc|pica|

---
# day 5
- JS是由ECMAScript、DOM、BOM组成。
- JS字符串不可改变，除非重新赋值。

---
# day6
- 逆波兰表达式：又叫“后缀表达式”，需要利用一个栈和一个输出字符串Output，从左到右读入中缀表达式：
```
class Stack {
  constructor() {
    // 使用 Array 保存栈数据
    this.stack = [];
  }

  // 压栈
  push(value) {
    this.stack.push(value);
  }

  // 出栈，栈为空时返回 undefined
  pop() {
    return this.stack.pop();
  }

  size() {
    return this.stack.length;
  }

  empty() {
    return this.size() === 0;
  }
}

const convertToReversePolish = (infixExpression) => {
  const operators = ['+', '-', '*', '/', '(', ')'];

  let stack = new Stack();
  let ret = [];

  // 切割表达式，模拟读取
  infixExpression.replace(/([\d+|\+|\-|\*|\/|\(|\)])/g, (_, expression) => {
    if (operators.includes(expression)) {
      // 读取到操作符，输出所有优先级更低的操作符
      while (true) {
        // 栈为空，直接将当前操作符压入栈中，并跳出循环
        if (stack.empty()) {
          stack.push(expression);
          break;
        }

        // `(` 的优先级最高，直接压入栈中，并跳出循环
        if (expression === '(') {
          stack.push(expression);
          break;
        }

        const op = stack.pop();

        // `)` 的优先级最高，只要操作符不为 `(` 则一直输出
        if (expression === ')') {
          if (op !== '(') {
            ret.push(op);
            continue;
          }
          // 跳出循环，不需要输出 `(`
          break;
        }

        // `(` 只在处理 `)` 时出栈
        if (op === '(') {
          stack.push(op);
          stack.push(expression);
          break;
        }

        if (expression === '+' || expression === '-') {
          // `+` 和 `-` 的优先级最低
          // 除非栈顶操作符也为 `+` 和 `-`，否则输出栈顶操作符，并继续
          if (op !== '+' || op !== '-') {
            ret.push(op);
            continue;
          }
        }

        // 比栈顶预算符优先级相同或更低，将操作符压回栈中，中止
        stack.push(op);
        stack.push(expression);
        break;
      }
    } else {
      // 操作数直接输出
      ret.push(expression);
    }
  });

  // 依次弹出栈中剩下的操作符，并输出
  while (!stack.empty()) {
    let op = stack.pop();

    if (op !== '(') {
      ret.push(op);
    }
  }

  return ret.join(' ');
};


console.log(convertToReversePolish('1 + 1 * 2'));  // => 1 1 2 * +
console.log(convertToReversePolish('(1 + 1) * 2')); // => 1 1 + 2 *
console.log(convertToReversePolish('1 + 2 * 3 + (4 * 5 + 6) * 7'));
// => 1 2 3 * + 4 5 * 6 + 7 * +

const evalReversePolish = (suffixExpression) => {
  const operators = ['+', '-', '*', '/'];

  let stack = new Stack();

  // 切割表达式，模拟读取
  suffixExpression.replace(/([\d+|\+|\-|\*|\/])/g, (_, expression) => {
    if (operators.includes(expression)) {
      const val1 = stack.pop(),
            val2 = stack.pop();

      switch (expression) {
        case '+':
          stack.push(val1 + val2);
          break;
        case '-':
          stack.push(val2 - val1);
          break;
        case '*':
          stack.push(val1 * val2);
          break;
        case '/':
          stack.push(val2 / val1);
          break
      }
    } else {
      // 操作值直接压入栈中
      stack.push(parseInt(expression));
    }
  });

  return stack.pop();
};


console.log(
  evalReversePolish(
    convertToReversePolish('1 + 1 * 2')));  // => 3
console.log(
  evalReversePolish(
    convertToReversePolish('(1 + 1) * 2')));  // => 4
console.log(
  evalReversePolish(
    convertToReversePolish('1 + 2 * 3 + (4 * 5 + 6) * 7')));  // => 189
```


- JS里的正则表达式：使用一个正则表达式字面量，其由包含在斜杠之间的模式组成，如下所示：
```
var re = /ab+c/;
```

&nbsp;&nbsp;&nbsp;&nbsp;或者调用RegExp对象的构造函数，如下所示：
```
var re = new RegExp("ab+c");
```
- 操作数：“操作符”即“运算符”，“操作数”就是在算式中被计算的数。
- flexbox盒子模型

---
# day7
- JS里的快排，[阮一峰大神的博客](http://www.ruanyifeng.com/blog/2011/04/quicksort_in_javascript.html)，主要用了递归和分治法的思想。

---
# day8
- 斐波那契数列的解法：
```
create a Fibonacci function, fabonacci(n), which returns the nth element of the Fibonacci sequence
```
```html
//解法1使用递归：
function fibonacci1(nth){
    if(nth == 1 || nth ==2){
        return 1;}
    else{
        return fibonacci1(nth-1)+fibonacci1(nth-2);
        }}

//解法2使用迭代：
function fibonacci2(nth){
    if(nth == 1 ||nth ==2){
        return 1;}
    else{
        var result=0;var one=1; var two=1;
        for(var i = 2; i<nth; i++){
            result = one+two;
            two = one;
            one = result;}
        return result;}
}
//通用公式法
function fibonacci3(n) {
      const SQRT_FIVE = Math.sqrt(5);
      return Math.round(1/SQRT_FIVE * (Math.pow(0.5 + SQRT_FIVE/2, n) - Math.pow(0.5 - SQRT_FIVE/2, n)));
    }
```

- 隐藏语句
```
create a function hideVowel(str), which returns a string replacing all vowels in the given str with “*”
```
```
function hideVowel(str){
    var result = '';
    for(var i=0;i<str.length;i++){
        result+="*";}
    return result;}
```
- 对于一些由value属性定义其显示内容的元素，例如：文本框、各种按钮等，不能使用textContent和innerHTML ，而应该通过其DOM元素的value property来获取/改变其显示内容。
- |DOM style property|CSS|
  |:---:|:--:|
  |backgroundColor|background-color|
  |border|border|
  |color|color|
  |cssFloat|float|
  |fontWeight|font-weight|
  |fontSize|font-size|
  |zIndex|z-index|

- **常见错误**对于fontSize、borderWidth、padding这些有单位的style属性，应该赋予字符串，而不是直接赋值。
- 非侵入式编程：避免在HTML标签中写上onchange、onclick等属性来注册JS事件处理程序，而是通过id、class等简单标识来找到相应需要改动的HTML元素，从而使HTML和JS分离开来。
- |property名|描述|
  |---|---|
  |nodeName|节点名，元素节点为HTML标签名（大写），属性节点为HTML属性名，文本节点始终为“#text”，文档节点名为“#document”|
  |nodeValue|节点值，元素节点值为null，属性节点值为属性值，文本节点值为文本内容。**文档节点值为？？？**|
  |nodeType|节点类型，元素节点为1，属性节点为2，文本节点为3，文档节点为9，注释节点为8。|
  |parentNode|父节点|
  |previousSibling|前一个兄弟节点|
  |nextSibling|后一个兄弟节点|
  |firstChild|第一个子节点|
  |lastChild|最后一个子节点|
  |childNodes|所有子节点的数目|

  ---
# day9
- 文档节点和元素节点可以拥有子节点，但是文本节点和属性节点不行；
- window.onload()：用于浏览器加载完网页之后立刻执行某些操作。这是因为JS中的函数方法等需要在HTML文件渲染完成之后才可使用；如果没有渲染完成，此时的DOM树是不完整的，这样JS文件可能报出“undefined”错误。
- |BOM对象|描述|
  |:---:|:---:|
  |window|浏览器用于显示网页的窗口|
  |document|浏览器窗口内当前的网页，DOM树的根（即使BOM成员，又是DOM成员）
  |location|当前网页的URL|
  |navigator|浏览器本身|
  |screen|浏览器当前占据的屏幕区域|
  |history|浏览器用户访问历史|

- |window对象常用方法：对象名|描述|
  |----|----|
  |alert、confirm、prompt|弹出对话框|
  |setInterval、setTimeout、clearInterval、clearTimeout|定时器|
  |open(url, name, options)、close()|打开新的浏览器窗口，关闭当前浏览器窗口|
  |print()|打印当前网页|
  |focus()、blur()|使当前浏览器获得焦点/失去焦点|
  |scrollBy(dx,dy)、scrollBy(x,y)|将浏览器窗口内页面纵向滚动dx（负值为向上），横向滚动dy（负值向左）；将浏览器窗口内页面滚动到(x,y)坐标处。|  

- |document对象property列表|描述|
  |---|---|
  |cookie|当前网页有效的所有cookie，以键值对的形式返回|
  |domain|提供当前网页的Web服务器域名|
  |referrer|前一个网页，用户从那里点击链接访问了当前网页|
  |title|当前网页的title|
  |URL|以字符串形式返回文档的地址栏链接。|
  |anchors|返回文档中所有锚点元素的列表|



--- 
# day10
- 什么时候不带“( )”，什么时候带？
> 加括号会立即调用函数。
- HTML文档和DOM都是树型结构，因此当一个事件发生的时候，既作用在当前元素上，也作用在当前元素的父元素和祖先元素上。

--- 
# day11
- Don`t write a loaded document.
- 给事件添加监听器，方法第一个参数为时间名，第二个参数为事件处理器。
```
button.addEventListener('click', function(){alert('hello world');});
```
- |比较对象|说明|
  |---|---|
  |this|**this表示当前对象的一个引用**。在方法中，this表示该方法所属的对象；如果单独使用，this表示全局对象；在函数中，this表示全局对象；在函数中，在严格模式下，this是未定义的；在实践中，this表示接收事件的元素；类似call()和apply()方法可以将this引用到任何对象。
  |self|self 指窗口本身，它返回的对象跟window对象是一模一样的。也正因为如此，window对象的常用方法和函数都可以用self代替window。|
  |window||

--- 
# day12
- JS中的let
- 当使用 position 属性时，IE8 以及更早的版本存在一个问题。如果容器元素（在我们的案例中是 <div class="container">）设置了指定的宽度，并且省略了 !DOCTYPE 声明，那么 IE8 以及更早的版本会在右侧增加 17px 的外边距。这似乎是为滚动条预留的空间。当使用 position 属性时，请始终设置 !DOCTYPE 声明。

---
# day13
- ES6中新增了两个重要的关键字：**let**和**const**。let声明的变量只在let命令所在的代码块中有效；const声明一个只读变量，一旦声明就不能改变。ES6之前，JS只有全局变量和函数内局部变量这两种作用域。let可以理解为局部变量的局部变量。关于js作用域的范围，我还理解不够彻底。
```
var x = 10;
// 这里输出 x 为 10
{ 
    var x = 2;
    // 这里输出 x 为 2
}
// 这里输出 x 为 2

------------------------------

var x = 10;
// 这里输出 x 为 10
{ 
    let x = 2;
    // 这里输出 x 为 2
}
// 这里输出 x 为 10
```

- display : grid 参考[阮一峰大神的博客](http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)。grid布局是比flex布局更强大的一种布局。grid-template-columns设置多少列，grid-template-rows设置行数。repeat()能重复写入相同的值，或者重复某种模式。1fr表示某种比例关系，比如“grid-template-columns: repeat(10, 1fr)”表示列宽设成10列，每列是当前块width的1/10。

- event.dataset
- html5的**data-\*** 属性用于存储私有页面后应用的自定义数据，是新增的属性。自定义的数据可以让页面拥有更好的交互体验（不需要使用 Ajax 或去服务端查询数据）。自定义属性前缀 "data-" 会被客户端忽略。