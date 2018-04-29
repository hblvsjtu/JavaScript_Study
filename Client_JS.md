# Client_JS  
  
  
### 作者：冰红茶  
### 参考书籍：《JavaScript权威指南》第二部分   

------    



   最开始的时候看完了《javascript权威指南》的第一部分，然后准备进入第二部分客户端JS的学习的时候，发现很多东西都是需要跟HTML和CSS的知识是在几个月前看第一轮学习中从入门到精通系列学的，感觉学得很粗糙，知识体系没有完全建立起来。遂果断进入二轮恶补阶段，把CSS和HTML5权威指南看来一遍，然后又把张老师的CSS世界补完，算是有了基本的知识体系。现在，就是进入《javascript权威指南》的第二部分的时候了^_ ^
  
## 目录

## [一、Web浏览器的JavaStript](#1)
### [1.1 Web文档中的JS](#1.1)
### [1.2 在HTML中嵌入JS](#1.2) 
### [1.3 时间线与同步、异步和延迟](#1.3) 
### [1.4 兼容性和互用性](#1.4)
### [1.5 安全性](#1.5)
## [二、Window对象](#2)
### [2.1 属性](#2.1)
### [2.2 计时器](#2.2) 
### [2.3 对话框](#2.3)
### [2.4 错误处理onerror](#2.4)
### [2.5 多窗口和窗体](#2.5)
## [三、脚本化文档](#3)
### [3.1 DOM概览](#3.1)
### [3.2 选取文档元素](#3.2)
### [3.3 文档结构和遍历](#3.3)
### [3.4 属性](#3.4)
### [3.5 元素的内容](#3.5)
### [3.6 元素操纵方法](#3.6)
### [3.7 document.write()](#3.7)
### [3.8 文档和元素的几何形状和滚动](#3.8)
## [四、事件处理](#4)
### [4.1 简介](#4.1)
### [4.2 事件类型](#4.2) 
### [4.3 注册事件处理程序](#4.3)
### [4.4 循环绑定事件](#4.4)
### [4.5 事件处理程序的调用](#4.5)
### [4.6 文档加载事件](#4.6)
### [4.7 几种页面跳转的方法](#4.7)		  
## [五、脚本化CSS](#5)
### [5.1 脚本化内联样式](#5.1)
### [5.2 脚本化CSS类](#5.2) 
### [5.3 脚本化样式表](#5.3) 
## [六、脚本化HTTP](#6)
### [6.1 Ajax和Comet](#6.1)
### [6.2 XMLHttpRequest](#6.2) 
### [6.3 脚本化样式表](#6.3)        
------ 		
        

<h2 id='1'> 一、Web浏览器的JavaStript </h2>
<h3 id='1.1'>1.1 Web文档中的JS</h3>  

#### 1) [global对象、Windows对象和document对象](https://blog.csdn.net/summer_15/article/details/73255115) 
> - Window对象是所有客户端JS特性和API的主要接入点，它表示Web浏览器的一个窗口或者窗体，并且可以用标识符window来引用它；
> - window对象是宿主对象也就是在一定的环境中才会生成的对象（这里也就是指浏览器），而global对象是在任何环境中都存在的。window对象具体也就是指浏览器打开的那个窗口；
> - document对象是window对象的一个属性，是显示于窗口内的一个文档。而window对象则是一个顶层对象，它不是另一个对象的属性。document可以理解为文档，就是你的网页，而window是你的窗口，就是你的浏览器包含的。它们俩在没有框架的情况下可以说是等同的，在有框架的情况下就要区别对待了。
#### 2) 脚本类型  
> - javascript
> - VBScript 巨硬公司IE专用的，MIME类型必须是type="text/vbscript";

<h3 id='1.2'>1.2 在HTML中嵌入JS</h3>  

#### 1) 在HTML中嵌入JS  
> - 内联，直接放在script的标签之间；
> - 从外部引入，利用script中的src属性，此时标签中间的代码无效化，但是可以添加一些注释和关于脚本的信息；
> - 在事件处理程序onclick()、onmousemove()这样的HTML属性指定；
> - 在URL中添加“javascript:我是代码”    
  
#### 2) “javascript:我是代码”  
> - 利用的是“javascript:”协议
> - 注释必须使用/\*注释\*/
> - 利用的是“javascript:我是代码”中返回的值，如果不返回值的话，最好使用void操作符，否则有的返回值会被转化为字符串显示\[object Window\]
> - Web早期的产物，现在最好不要使用；
> - 应用:书签程序


<h3 id='1.3'>1.3 客户端JS的线程模型</h3>   

#### 1) 单线程  
> - 避免锁，死锁和竞争条件；
#### 2) Web worker  
> - HTML5定义的一种并发控制方式；
> - 不能访问文档内容，不能与其他侠worker或者主线程共享状态；
> - 只可以和主线程和其他worker通过异步事件通讯，所以不能检查并发性；
#### 3) 客户端JS的时间线 
    
>> 次序|动作|readystate属性|能否使用document.write()   
>> -|-|-|-
>> 1|创建document对象，开始解析HTML文档|loading|
>> 2|默认的时候同步下载JS脚本文件|loading|能
>> 3|异步则继续解析文档|loading|不能
>> 4|当文档解析完|interactive|-
>> 5|所有的defer脚本会在文档里按顺序执行，异步脚本则有可能执行|-|异步则不能
>> 6|document对象触发DOMContentLoaded事件，标志着程序执行从同步脚本执行阶段切换到异步事件驱动阶段，但是需要注意的是异步脚本没有执行完成|-|-
>> 7|文档完全解析完成，但浏览器还在等待相关资源的载入，如图片，还有异步脚本还在执行|当所有资源载入和所有异步脚本执行完毕后，complete，Web浏览器触发Windows对象上的load事件|-
>> 8|调用异步事件，以异步相应客户的输入|-|-   

> - 这是一个非常理想的时间线，DOMContentLoaded事件在load时间之前触发

<h3 id='1.4'>1.4 兼容性和互用性</h3>   

#### 1) 问题总结  
> - 演化——新老浏览器之间的不兼容 随着标准规范的更新，一些新的浏览器会支持，一些老的不支持，需要在老浏览器的大群体和新浏览器的小群体中做出权衡
> - 未实现——各家浏览器之间的不兼容 对于某个特性，各家浏览器实现的情况都不一样。
> - bug 每个浏览器都有bug    

#### 2) 兼容性框架——jQuery  
> - 事件处理程序的注册是通过叫bind()的方法完成的，不用担心和考虑addEventListener（这是JavaStript的函数）和attachEvent()（这是VBStript的函数）之间的不兼容性问题。
#### 3) 分级浏览器 
> - 起初是Yahoo！率先提出的一种测试技术，从某个维度对浏览器厂商/版本/操作系统进行分级。分级浏览器中的A级要通过所有功能测试用例，C级则不必通过所有。
#### 4) 怪异模式和标准模式 
> - 标准模式则需要兼容CSS标准规范 document.compatMode==CSS1Compat
> - 怪异模式则需要遵循浏览器自己的规范（这主要是为了兼容老版本的浏览器） document.compatMode==BackCompat/undefined

<h3 id='1.5'>1.5 安全性</h3>   

#### 1) JS不能做什么  
> - 不支持对用户文件进行访问和修改
> - 没有通用的网络能力
>> - 只有用户点击确认才能打开新的浏览器窗口（防止广告弹窗）
>> - 只能关闭自己的窗口，不能关闭其他的浏览器窗口
>> - 上传文件的value属性只读
>> - 脚本不能读取来自不同浏览器载入的文档内容（同源策略）
#### 2) 同源策略
> - 何为同源：采用相同的协议 主机 端口
> - 脚本只能读取和所属文档来源相同的窗口和文档，或者说脚本只能对直接文档起作用，对间接文档不能访问
#### 3) 不严格的同源策略
> - 默认情况下document的domain属性存放的是载入文档的服务器的主机名，如果两个窗口或者窗体的脚本的domain属性设置成相同的值，则不受同源策略的约束；
> - 跨域资源共享Crossing-Origin Resource Sharing 它允许服务器用头信息显示地列出源，或者使用通配符来匹配所有的源并允许其访问。请求头是Origin，相应头是Access-Control-Allow-Origin，这样XMLHttpRequest就不受同源的约束了
> - 跨文档消息 允许来自一个文档的脚本可以传递文本消息到另一个文档的脚本，而不管脚本是否同源。调用的是Windows对象上的postMessage()方法，异步传递消息。但是还是不能调用其他文档的方法和读取里面的属性，一次以此实现安全的通讯。
#### 4) 跨站脚本
> - 在URL地址上添加脚本
#### 5) 拒绝服务攻击
        
------
        
<h2 id='2'> 二 Window对象 </h2>    
<h3 id='2.1'>2.1 属性</h3>  
  
>> Window属性|Window属性|方法
>> -|-|-
>> Window.location|Location对象|asign()/replace()/reload()
>> Window.history|History对象|back()和forward()
>> Window.navigator|Navigator对象|引用包含浏览器厂商和版本信息
>> Window.screen|Screen对象|有关窗口显示的大小和可用颜色数量的信息 
		
>> - Document也有一个URL属性，是文档首次载入时保存该文档的URL静态字符串，Location对象的href属性（当前文档的URL的完整文本的字符串）可以改变，但是Document.URL首次载入后就不能改变。
>> - Location对象的href属性保存当前文档的URL的完整文本的字符串，可以使用Location.toString()方法返回href属性的值，同时也可以隐式调用。调用的时候便可替代Location.href；
>> - Location的assign(URL)表示使窗口载入并显示你指定的URL中的文档。replace()方法也类似，但它载入的时候会将浏览历史中的它的记录删除；
>> - history back()和forward()方法只接受一个数字类型作为参数，可以是负数，表示前进或者返回第n个页面。如：
		
        		history.go(-2);			
        		//后退两个历史记录，相当于单击“后退”按钮两次			
>> - location对象
>>>>>> ![图3-11 location对象](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-11%20location%E5%AF%B9%E8%B1%A1.png?raw=true)
>> - document对象
>>>>>> ![图3-9 document对象A](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-9%20document%E5%AF%B9%E8%B1%A1A.png?raw=true)  
>>>>>> ![图3-10 document对象B](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-10%20document%E5%AF%B9%E8%B1%A1B.png?raw=true)  
>> -  Window对象
>>>>>> ![图3-12 Window对象a](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-12%20Window%E5%AF%B9%E8%B1%A1a.png?raw=true)  
>>>>>> ![图3-12 Window对象b](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-12%20Window%E5%AF%B9%E8%B1%A1b.png?raw=true)		
>> -  History对象
>>>>>> ![图3-13 History对象](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-13%20History%E5%AF%B9%E8%B1%A1.png?raw=true)  
>> -  Screen对象
>>>>>> ![图3-14 Screen对象.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-14%20Screen%E5%AF%B9%E8%B1%A1.png?raw=true)  


<h3 id='2.2'>2.2 计时器</h3>  

#### 1) setTimeout(function, delaytime)
#### 2) setInterval(function, repeattime)
#### 3) 如果需要终止，需利用返回的值作为clearTimeout的参数
>>>>>> ![图2-2 定时器应用函数](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-2%20%E5%AE%9A%E6%97%B6%E5%99%A8%E5%BA%94%E7%94%A8%E5%87%BD%E6%95%B0.png?raw=true)     

<h3 id='2.3'>2.3 对话框</h3>  

#### 1) prompt() 
>> - 获取输入对话框，需要用户输入后选择确认。会产生阻塞。
#### 2) confirm() 
>> - 确认对话框，需要用户点击确认。会产生阻塞。
#### 3) alert() 
>> - 警告对话框，需要用户点击关闭。会产生阻塞。
#### 4) 模态对话框showModalDialog() 
>>>>>> ![图2-1 模态对话框showModalDialog()](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE2-1%20%E6%A8%A1%E6%80%81%E5%AF%B9%E8%AF%9D%E6%A1%86showModalDialog.png?raw=true)   


<h3 id='2.4'>2.4 错误处理onerror</h3>  

#### 1) onerror()三个参数
>> - window.onerror(description, URL, Line)
>>>>>> ![图2-3 错误处理](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE2-3%20%E9%94%99%E8%AF%AF%E5%A4%84%E7%90%86.png?raw=true)    

<h3 id='2.5'>2.5 多窗口和窗体</h3>  

#### 1) 子窗口和子窗体的区别：
>> - 子窗口指的是使用window.open打开的新的页面，双方不存在嵌套窗体的作用；
>> - 子窗体指的是窗口内通过iframe元素嵌套着的小窗体；
  
#### 2) [global对象、Windows对象和document对象](https://blog.csdn.net/summer_15/article/details/73255115) 
>> - Window对象是所有客户端JS特性和API的主要接入点，它表示Web浏览器的一个窗口或者窗体，并且可以用标识符window来引用它。包括：窗口，标签页，iframe和框架
>> - indow对象是宿主对象也就是在一定的环境中才会生成的对象（这里也就是指浏览器），而global对象是在任何环境中都存在的。window对象具体也就是指浏览器打开的那个窗口；
>> - document对象是window对象的一个属性，是显示于窗口内的一个文档。而window对象则是一个顶层对象，它不是另一个对象的属性。document可以理解为文档，就是你的网页，而window是你的窗口，就是你的浏览器包含的。它们俩在没有框架的情况下可以说是等同的，在有框架的情况下就要区别对待了。   

#### 3) id属性
>> - 必须是唯一的
>> - 元素的id属性为脚本可访问的全局变量；
>> - 但是不能与已有的关键字重复，否则无效，比如history,navigator, screen等    

#### 4) 标签页
>> - 理论上讲每个标签页都是独立的“浏览器上下文”（browsing content），每个上下文都有独立的Window对象，互相互不干扰。
>> - 虽然Window对象相互独立，但是不代表窗口之间也是相互独立。当一个标签页或者一个窗口是由另一个标签页或者窗口的脚本打开的时候，这样的窗口之间就可以互相操作了（但是也会受到同源策略的约束）
>> - 同样道理，嵌套的窗体之间也是可以互相看见的（但是也会受到同源策略的约束）
  
#### 5) [窗口的引用](http://javascript.ruanyifeng.com/bom/window.html#toc29) 
>> - top：顶层窗口，即最上层的那个窗口
>> - parent：父窗口
>> - self：当前窗口，即自身
    
                top === self  //下面代码可以判断，当前窗口是否为顶层窗口。   
                
                // 更好的写法
                window.top === window.self    
                
                parent.history.back();  //下面的代码让父窗口的访问历史后退一次。       
#### 6) [iframe标签——子窗体](http://javascript.ruanyifeng.com/bom/window.html#toc29) 
>> - 对于iframe嵌入的窗口，document.getElementById方法可以拿到该窗口的DOM节点，然后使用contentWindow属性获得iframe节点包含的window对象，或者使用contentDocument属性获得包含的document对象。
    
                var frame = document.getElementById('theFrame');
                var frameWindow = frame.contentWindow;

                // 等同于 frame.contentWindow.document
                var frameDoc = frame.contentDocument;

                // 获取子窗口的变量和属性
                frameWindow.function()

                // 获取子窗口的标题
                frameWindow.title   
>> - iframe元素遵守同源政策，只有当父页面与框架页面来自同一个域名，两者之间才可以用脚本通信，否则只有使用 *window.postMessage* 方法。iframe窗口内部，使用window.parent引用父窗口。如果当前页面没有父窗口，则window.parent属性返回自身。
        
                if (window.parent !== window.self) {
                  // 当前窗口是子窗口
                }       
>> - iframe嵌入窗口的window对象，有一个frameElement属性，返回它在父窗口中的DOM节点。对于那么非嵌入的窗口，该属性等于null。
        
                var f1Element = document.getElementById('f1');
                var fiWindow = f1Element.contentWindow;
                f1Window.frameElement === f1Element // true
                window.frameElement === null // 对于顶级窗口而言永远是true，因为它没有父窗口        
>> - 但是通常不需要搞得那么复杂，先要获取iframe元素，然后再通过该元素或者子窗体的的window对象。只要使用frame属性一步到位。frame属性是一个类数组对象，frame\[0\]表示所有嵌套子窗体排序的第一个。parent.frames\[1\]表示引用兄弟窗体。		
        
------		
                
<h2 id='3'> 三、脚本化文档 </h2>    
<h3 id='3.1'>3.1 DOM概览</h3>  
  	
#### 1) 相关概念
>> - DOM是表示和操作HTML和XML文档内容的基础API
>> - 祖先节点 父节点 子节点 兄弟节点 后代节点
>> - 文档Document又分HTMLDocument和XMLDocument，元素Element又分HTMLElement和XMLElement，两者是不一样的；
>> - document.body显式指代body标签；document.head显式指代head标签；document.documentElement显式指代根元素html；
>>>>>> ![图3-1 文档节点的部分层次结构](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-1%20%E6%96%87%E6%A1%A3%E8%8A%82%E7%82%B9%E7%9A%84%E9%83%A8%E5%88%86%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84.png?raw=true)  


<h3 id='3.2'>3.2 选取文档元素</h3>		
		
>>>>>> ![图3-16 寻找元素的Document方法](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-16%20%E5%AF%BB%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84Document%E6%96%B9%E6%B3%95.png?raw=true) 		

#### 1) 通过ID属性选取
>> - getElementByID()		
#### 2) 通过name属性选取
>> - getElementsByName() 返回的是NodeList对象（按照文档出现的顺序进行排序），这是因为同名的元素可能不止一个；
>> - 名字name会自动加入到Document对象中并添加相应的属性；
>> - name的属性只出现在HTML中，XML没有
#### 3) 通过标签选取
>> - getElementsByTagName() 返回的是NodeList对象（按照文档出现的顺序进行排序），这是因为同名的元素可能不止一个；		
#### 4) 通过指定的CSS类选取
>> - getElementsByClassName() 返回的是NodeList对象（按照文档出现的顺序进行排序），这是因为同名的元素可能不止一个；对元素以及其子元素进行匹配；	
>> - 在HTML中，元素的类可以进行叠加，中间使用空格隔开。所以，在匹配的时候getElementsByClassName()的类名参数也可以用空格隔开，类名可以不按顺序；
>> - 怪异模式的出现是为了向后兼容（在文档的开头<!DOCTYPE>），class类名不区分大小写，如果在这种情况下，脚本的类名参数也不区分大小写，否则区分大小写；
>>>>>> ![图3-2 静态副本](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-2%20%E9%9D%99%E6%80%81%E5%89%AF%E6%9C%AC.png?raw=true) 
#### 5) 通过指定的CSS选择器选取
>> - querySelectorAll() 参数是CSS选择器的，返回的是匹配成功的NodeList对象；
>> - querySelector()参数是CSS选择器的，返回的是匹配成功的第一个对象；
>> - 对于伪类选择器，比如：link()或者：visited，很多浏览器会拒绝返回，因为可能会泄漏客户的浏览记录；
#### 6) document.all\[\]
>> - 出现在DOM标准化之前，现在已经弃用；
>>>>>> ![图3-3 document.all\[\]](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-3%20document.all%5B%5D.png?raw=true) 		

#### 7) NodeList和HTMLCollection的实时性
>> - HTMLCollection对象是document.images和document.forms的返回值
>> - NodeList和HTMLCollection对象都是只读的类数组对象，有length属性，可以按照数组那样使用编号进行索引，但不能直接调用Array的方法；
>> - 实时性即会跟据HTML和CSS的变化实时改变NodeList和HTMLCollection的返回值；
>> - 需要迭代进行添加或者删除元素的时候，需要建立一个副本
>>>>>> ![图3-2 静态副本](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-2%20%E9%9D%99%E6%80%81%E5%89%AF%E6%9C%AC.png?raw=true) 		
                        
<h3 id='3.3'>3.3 文档结构和遍历</h3>		
        
#### 1) 作为节点树的文档        
>> - 节点树主要包括Document对象，Element对象和Text对象都是Node对象
        
>> 次序|名字|含义   
>> -|-|-
>> 1|parentNode|父节点
>> 2|childNodes|子节点
>> 3|firstChild，lastChild|子节点的第一个和最后一个
>> 4|nextSibling，previousSibling|该节点的兄弟节点的前一个和后一个
>> 5|nodeType|返回节点的类型
>> 6|nodeValue|Text节点和Comment节点的文本内容
>> 7|nodeName|元素的标签名，以答谢的形式表示
>> 8|parentNode|父节点		

>> - nodeType返回值 9代表Document节点，1代表Element节点，3代表text节点，8代表Comment节点，11代表DocumentFragment节点；
>> - 用法：他的参考是Node对象，从Node对象出发：	
>>>>>> ![图3-4 作为节点树的文档](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-4%20%E4%BD%9C%E4%B8%BA%E8%8A%82%E7%82%B9%E6%A0%91%E7%9A%84%E6%96%87%E6%A1%A3.png?raw=true) 	
		
#### 2) 作为元素树的文档
>> - 主要额度研究兴趣点在文档的元素上而非它们之间的文本（和他们之间的空白，包括Text和Comment节点），参考点是具体的某个元素
        
>> 次序|名字|含义|返回   
>> -|-|-|-
>> 1|children|子节点|NodeList对象
>> 2|firstElementChild，lastElementChild|子元素的第一个和最后一个
>> 3|nextElementSibling，previousElementSibling|该元素的兄弟元素的前一个和后一个
>> 4|childElementCount|子元素的数量，返回值跟children.length的值相同		

>> - 说起奇怪，好像唯独是缺了parent，此时需要借助作为节点树的文档的parentNode。		
>>>>>> ![图3-5 返回元素e的第n层祖先元素](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-5%20%E8%BF%94%E5%9B%9E%E5%85%83%E7%B4%A0e%E7%9A%84%E7%AC%ACn%E5%B1%82%E7%A5%96%E5%85%88%E5%85%83%E7%B4%A0.png?raw=true)		

<h3 id='3.4'>3.4 属性</h3>		

#### 1) attribute VS proerty
>> - attributed代表的是元素的属性，名值对；
>> - proerty代表的是对象的属性；		
#### 2) HTML属性作为Element的属性
>> - 返回的类型基本与元素的属性的相同，而不是简单的额字符串
>> - HTML的属性是不区分大小写的，但是JS是区分的，所以在转化的过程中需要采用驼峰式的命名方式
>>>>>> ![图3-6 HTML属性作为Element的属性](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-6%20HTML%E5%B1%9E%E6%80%A7%E4%BD%9C%E4%B8%BAElement%E7%9A%84%E5%B1%9E%E6%80%A7.png?raw=true)		

#### 3) 获取和设置非标准的HTML属性
>> - 跟前面的API最大的区别是：返回的是字符串格式，其次，属性名采用标准属性名；
>> - html的属性不区分大小写；
>> - 方法包括getAttribute()；setAttribute()；hasAttribute()；removeAttribute()
>>>>>> ![图3-7 获取和设置非标准的HTML属性](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-7%20%E8%8E%B7%E5%8F%96%E5%92%8C%E8%AE%BE%E7%BD%AE%E9%9D%9E%E6%A0%87%E5%87%86%E7%9A%84HTML%E5%B1%9E%E6%80%A7.png?raw=true)		

#### 4) 作为Attr节点的属性
>> - 针对任何非Element对象的任何节点，该属性为null;
>> - 针对任何Element对象的任何节点，返回值是像NodeLists的类数组对象；
>>>>>> ![图3-8 作为Attr节点的属性](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-8%20%E4%BD%9C%E4%B8%BAAttr%E8%8A%82%E7%82%B9%E7%9A%84%E5%B1%9E%E6%80%A7.png?raw=true)			

<h3 id='3.5'> <a href="https://blog.csdn.net/debugingstudy/article/details/11100977">3.5 元素的内容</a></h3>		

        		<div id="test">     
        		   <span style="color:red">test1</span> test2     
        		</div> 		
#### 1) test.innerHTML（所有浏览器支持）：
        
                <span style="color:red">test1</span> test2
#### 2) test.outerHTML（所有浏览器支持）: 
>> - 除了包含innerHTML的全部内容外, 还包含对象标签本身。 
>> - 上例中的text.outerHTML的值也就是
        
                <div id="test"><span style="color:red">test1</span> test2</div> 
#### 3) test.innerText（IE仅支持）: 
>> - 从起始位置到终止位置的内容, 但它去除Html标签
>> - 上例中的text.innerTest的值也就是“test1 test2”, 其中span标签去除了。 
#### 4) test.textContent(除了IE都支持):
>> - 从起始位置到终止位置的内容, 但它去除Html标签
>> - 上例中的text.textContent的值也就是“test1 test2”, 其中span标签去除了。 所以同IE的innerText。
>> - 注意，要判断test.textContent在浏览器中是否兼容，不能直接使用
        
                if(test.textContent)，
>> - 这是因为假如test.textContent的值是一个空字符串，也会返回假值，所以最好是使用
        
                if(test.textContent === undefine )

<h3 id='3.6'>3.6 元素操纵方法</h3>		

#### 1) 新建添加删除复制
>>>>>> ![图3-17 DOM操纵成员](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-17%20DOM%E6%93%8D%E7%BA%B5%E6%88%90%E5%91%98.png?raw=true)
>>>>>> ![图3-17 DOM操纵成员b](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-17%20DOM%E6%93%8D%E7%BA%B5%E6%88%90%E5%91%98b.png?raw=true)
> - 新建节点creatElement()和增加节点appendChild()  appendChild()在最后一个子节点中插入
        
                /* 增加节点creatElement()
                 * 当contentbox高度增加的时候添加节点
                 */
                  var addnewsrows = function() {
                        var newstable = document.getElementById("newstable");
                        var newsrows = document.createElement("div");
                        var length = document.getElementsByName("newsrows").length;
                        newsrows.id = "newsrows_" + length;
                        newsrows.className = "newsrows1";
                        //newsrows.name = "newsrows";无法设置name
                        newsrows.setAttribute("name","newsrows");
                        newstable.appendChild(newsrows);
                  }
> - 复制节点cloneNode(bool)  当里面的布尔值为true的时候复制后代在内的所有，如果是false的话就仅复制自己；
                
                /* 通过复制的方式添加节点cloneNode()
                   * 当contentbox高度增加的时候添加节点
                   */
                  var addnewsrows = function() {
                        var newstable = document.getElementById("newstable");
                        var oldnewsrows = document.getElementById("newsrows_1");
                        var newsrows = oldnewsrows.cloneNode(true);
                        length = document.getElementsByName("newsrows").length;
                        lengths=length+1;
                        newsrows.id = "newsrows_" + lengths;
                        newstable.appendChild(newsrows);
                        var newsinterest=document.getElementsByName("newsinterest")
                        newsinterest[length].id="newsinterest_"+ lengths;
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter.bind(newsinterest[length]), false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave.bind(newsinterest[length]), false);
                  }        
> - 增加节点insertBefore(newNode,existNode) 在已存在的子元素的前面插入新的元素。
> - 删除节点removeChild(childrenObj) 作用在父元素上
        
                fatherObj.removeChild(childrenObj)
> - 替换节点replaceChild(newNode, oldNode)
        
                fatherObj.replaceChild(newNode, oldNode)
> - 文档节点documentFragment
>> - 作为其他节点的一个临时容器而存在； 
>> - var frag = document.createDocumentFragment();
>> - 它的parentNode总是为null
>> - 它的特殊之处在于：如果把它作为一个节点传递给appendChild(),insertBefore()或者replaceChild(),相当于把它里面的所有子节点插入到文档中，而非片段本身，此时文档片段被清空以便重用。另外，给文档片段添加子节点的时候，原来的子节点被清除。
>> - 其实就相当于剪切和粘贴的作用
>>>>>> ![图4-1 文档片段](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE4-1%20%E6%96%87%E6%A1%A3%E7%89%87%E6%AE%B5.png?raw=true)  
           
<h3 id='3.7'><a href="https://blog.csdn.net/qq_34986769/article/details/52160532">3.7 document.write()</a></h3> 
        
#### 1) 格式: 
>> - 在调用document.write，最好不要把document.open和document.close漏掉，尽管多数时候浏览器会帮忙完成这些操作。即，一个标准的document.write应该是这样的：

                document.open();
                document.write('anthing')
                document.close(); 
#### 2) 弊端 
>> - 从某个角度说，document.write的实际功能确实很强，能够直接修改文档流，但它有很多弊端：在非loading阶段调用document.write会清除已加载的页面；
>> - document.write不能够在XHTML中使用；
>> - 嵌入script中的document.write不能给任意节点添加子节点，因为它是随着DOM的构建执行的；
>> - 利用document.write写入HTML字符串流并不是一个好方法，它有违DOM操作的概念；
>> - 利用document.write添加script加载外部脚本时，浏览器的HTML解析会被script的加载所阻塞；

<h3 id='3.8'>3.8 文档和元素的几何形状和滚动</h3>                
        
#### 1) 文档坐标和视口坐标
> - 元素的坐标用像素作为单位来度量，向右表示X坐标增加，向下代表Y坐标增加
> - "视口"不包括浏览器的外壳（如菜单栏，工具栏等），而是实际显示文档内容的浏览器的一部分；
> - 如果文档要比视口要小，说明还没有出现滚动。其转换公式为：
                
                文档X坐标 = 视口X坐标 + 滚动偏移量X
                文档Y坐标 = 视口Y坐标 + 滚动动偏移量Y 
#### 2) 滚动偏移量
> - 提供滚动条的位置 除IE8及更早的版以外所有的浏览器，均可使用pageXOffest和pageYOffest属性获得，而所有的IE都可以使用scrollLeft和scrollTop属性获得滚动条的位置。不过比较奇怪的是，在怪异模式下，必须通过body元素来查询，而在普通模式下则是通过html元素获得；
        
                /* checkScrollOffset
                 * 获取窗口滚动条的偏移量
                 */
                var checkScrollOffset = function(gundong_X, gundong_Y, myWindow) {
                    
                    //使用指定接受参数的元素
                    var gundong_X = document.getElementById(gundong_X);
                    var gundong_Y = document.getElementById(gundong_Y);
    
                    //使用指定的窗口，如果不带参数则使用当前窗口
                    var w = myWindow || window;
                    var d = w.document;
    
                    //除IE8及之前的版本，其他所有的浏览器都能用
                    if(w.pageXOffset != null) {
                        gundong_X.innerHTML = "正常版本_" + w.pageXOffset;
                        gundong_Y.innerHTML = "正常版本_" + w.pageYOffset;
                    }
                    
                    //标准模式下的IE浏览器或其他所有的浏览器
                    
                    else if(document.compatMode == "CSS1Compat") {
                        gundong_X.innerHTML = "标准模式_" + d.documentElement.scrollLeft;
                        gundong_Y.innerHTML = "标准模式_" + d.documentElement.scrollTop;
                    }
    
                    //怪异模式下的IE浏览器或其他所有的浏览器
                    else {
                        gundong_X.innerHTML = "怪异模式_" + d.body.scrollLeft;
                        gundong_Y.innerHTML = "怪异模式_" + d.body.scrollTop;
                    }   
                }
    
                document.addEventListener("mousemove", function() {
                        checkScrollOffset("gundong_X", "gundong_Y");
                }, false);
#### 3) 视窗大小
> - 提供视窗的宽度和高度 除IE8及更早的版以外所有的浏览器，均可使用innerWidth和innerHeight属性获得，而所有的IE都可以使用clientWidth和clientHeight属性获得视窗的大小。不过比较奇怪的是，在怪异模式下，必须通过body元素来查询，而在普通模式下则是通过html元素获得；
        
                /* getViewportSize
                 * 获取视窗的宽度和高度
                 */
                var getViewportSize = function(shichuang_X, shichuang_Y, myWindow) {
    
                    var shichuang_X = document.getElementById(shichuang_X);
                    var shichuang_Y = document.getElementById(shichuang_Y);
    
                    //使用指定的窗口，如果不带参数则使用当前窗口
                    var w = myWindow || window;
                    var d = w.document;
    
                    //除IE8及之前的版本，其他所有的浏览器都能用
                    if(w.pageXOffset != null) {
                        shichuang_X.innerHTML = "正常版本_" + w.innerWidth;
                        shichuang_Y.innerHTML = "正常版本_" + w.innerHeight;
                    }
                    
                    //标准模式下的IE浏览器或其他所有的浏览器
                    
                    else if(document.compatMode == "CSS1Compat") {
                        shichuang_X.innerHTML = "标准模式_" + d.documentElement.clientWidth;
                        shichuang_Y.innerHTML = "标准模式_" + d.documentElement.clientHeight;
                    }
    
                    //怪异模式下的IE浏览器或其他所有的浏览器
                    else {
                        shichuang_X.innerHTML = "怪异模式_" + d.body.clientWidth;
                        shichuang_Y.innerHTML = "怪异模式_" + d.body.clientHeight;
                    }   
                }
    
                document.addEventListener("mousemove", function() {
                        getViewportSize("shichuang_X", "shichuang_Y");
                }, false);
#### 4) 查询元素的几何尺寸
> - IE5引入了getBoundingClinetRect()，返回一个有left，right，top和bottom属性的对象，left，top表示左上角的以视窗为参考系的X和Y坐标，right和bottom属性表示的是以视窗为参考系的右下角的X和Y坐标。这个坐标以元素的边框为边界。后来被标准收入并广泛传播到其他浏览器。
        
                /* getElementSize
                 * 获取元素的宽度和长度
                 */
                var getElementSize = function(myElement) {
                        var myElement = document.getElementById(myElement);
                        var box = myElement.getBoundingClientRect();
                        console.log("box的左上角X坐标："+ box.left +"px;");
                        console.log("box的左上角Y坐标："+ box.top +"px;");
                        console.log("box的右下角X坐标："+ box.right +"px;");
                        console.log("box的右下角Y坐标："+ box.bottom +"px;");
                }
            
                var myElement = document.getElementById("position");
                myElement.addEventListener("mousemove", function() {
                        getElementSize("position");
                }, false);
> - 如果想要查询行内元素的具体尺寸，需要单独采用getClinetRect(),返回的内容跟getBoundingClinetRect()类似，是一个类数组的对象。
> - 关于实时性的问题，大多数DOM方法都是实时更新的，但是getBoundingClinetRect()和getClinetRect()却不是，他只是一个瞬时的快照
#### 5) 判断某元素在某点
> - elementFromPoint(),参数是X坐标和Y坐标，返回在视窗范围内某坐标上的一个元素，如果某点在视窗之外，则返回null。由于鼠标的事件对象的target属性已经包含了这些信息，所以这个功能显得有些鸡肋。
#### 6) 鼠标事件
>>>>>> ![图2-2 鼠标事件.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-2%20%E9%BC%A0%E6%A0%87%E4%BA%8B%E4%BB%B6.png?raw=true)
#### 7) 滚动
> - scrollTo(X，Y)或着scroll(X，Y) 接受两个参数，分别是相对于视窗的X坐标和Y坐标，那个点将会出现在视窗的左上角，属于window的属性；
> - scrollBy(X，Y)，接受两个参数，分别是相对于视窗的X坐标和Y坐标，那个点将会出现在视窗的左上角，属于window的属性；
                
                // 注意它一旦开始就没办法停止^-^
                setInterval(function() {scrollBy(0,-10)}, 1000); 
> - scrollIntoView()的行为是尽量将所选择的元素放在视窗中，默认把元素的上边缘尽量靠经视窗的上边缘，如果传递false作为参数，则把元素的下边缘尽量靠经视窗的下边缘，类似于a元素的锚点功能；
#### 8) 滚动关于元素尺寸，位置和溢出
> - offsetLeft和offSetHeigt是以文档坐标为参考的
>>>>>> ![图2-3 关于元素尺寸，位置和溢出](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-3%20%E5%85%B3%E4%BA%8E%E5%85%83%E7%B4%A0%E5%B0%BA%E5%AF%B8%EF%BC%8C%E4%BD%8D%E7%BD%AE%E5%92%8C%E6%BA%A2%E5%87%BA.png?raw=true)
           
                /* 判断元素是否溢出
                 * 先利用clientHeight获取元素高度，在利用scrollHeight获取内容高度
                 * 然后比较这两个高度，如果scrollHeight>clientHeight,则溢出
                 */ 
                 var isOverflow = function(ele) {
                    var element = document.getElementById(ele);
                    var scrollHeight = element.scrollHeight;
                    var clientHeight = element.clientHeight;
                    if(scrollHeight > clientHeight) {
                        console.log(ele + "溢出了");
                    }else {
                        console.log(ele + "没有溢出");
                    }
                 }
                 document.addEventListener("mousemove", function() {
                        isOverflow("contentbox");
                 }, false); 
------ 
            
<h2 id='4'> 四、事件处理 </h2>        
<h3 id='4.1'>4.1 简介</h3>    
        
#### 1) 简介
> -  异步事件驱动编程模型，广泛应用于图形界面；
> -  事件类型
> -  事件目标
> -  事件处理程序或事件监听程序
> -  事件对象，至少包含事件类型和事件目标等信息
> -  事件传播，比如冒泡；
> -  [1-1 事件处理概念.png](https://blog.csdn.net/wuqinfei_cs/article/details/48413809) 
>>>>>> ![1-1 事件处理概念.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/1-1%20%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%A6%82%E5%BF%B5.png?raw=true)        
        
<h3 id='4.2'>4.2 事件类型 </h3>    

#### 1) 传统事件类型   
> - 表单事件
> - window事件
>> - 比如著名的onload()，仅在文档及图片全部加载完毕时触发。 
>> - DomContentLoaded()，当文档加载解析完毕且所有延迟脚本都执行完毕时会触发，此时图片和异步（async）脚本可能还在加载
>> - document.readyState属性随着文档加载过程而变，每次改变都伴随着document上的readystatechange事件
>> - whenReady函数
> - 鼠标事件
> - 键盘事件
#### 2) DOM事件
#### 3) HTML5事件
> - audio和video
> - drag
> - 历史管理机制
> - HTML表单
> - 离线web应用
#### 4) 注册事件处理程序
> - 设置HTML标签属性为事件处理程序（不推荐）
> - addEventListener()和removeEventListener()
> - attachEvent()和detachEvent()，IE不支持事件捕获，但允许同一事件处理程序注册多次，且事件触发时，程序执行次数和注册次数一样
    
<h3 id='4.3'>4.3 注册事件处理程序 </h3>    
        
#### 1) 两种方法 
> - 直接给事件目标对象或者元素设置属性，这种方法出现在Web初期比较多；利用JS将事件处理程序传递给对象或者元素；
> - (1) 设置JS对象的属性添加事件处理程序
>> - 由于属性名区分大小写，所以约定所有都是小写，on+事件名，这种方法适用于所有浏览器的所有常用事件类型，但是这种方法也有一个缺陷是，每个属性最多添加一个事件处理函数，意味着后来的事件处理函数会覆盖前面的事件处理函数。如： 
               
               window.onload = function() {
                    var elt = document.getElementById("myform");
                    elt.onsubmit = function() { 
                        return validate(this);
                    }
                } 
> - (2) 设置HTML标签属性为事件处理程序 
>> - 具体就是用于设置的文档元素时间处理程序属性property换成对应的HTML标签的属性attribute。如果这样做，属性值应该是JS代码的字符串，而非完整的函数声明，也就意味着HTML时间处理程序的程序代码不应该用大括号包围而且使用function关键字作为前缀。如：<button onclick="alert('Hello');" >点击这里</button>                 
        
                <button onclick="alert('Hello');" >点击这里</button>
                       
>> - 但是实际上浏览器会把该代码转为类似如下的完整代码：

                function() {
                    with(document);
                        with(this.form || {}) {
                            with(this) {
                                /* 这里是程序代码 */
                            }
                        }       
                }       
>> - 由于客户端编程的风格偏向于把内容和行为分离，所以并不支持用这种方式；
>> - 还有一些是直接作用在浏览器而非某个单独的元素，其完整的HTML5事件处理程序列表如下：
>>>>>> ![1-2 完整的HTML5事件处理程序列表.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/1-2%20%E5%AE%8C%E6%95%B4%E7%9A%84HTML5%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E7%A8%8B%E5%BA%8F%E5%88%97%E8%A1%A8.png?raw=true)   
    
> - (3) addEventListener(type, func, bool)与removeEventListener(type, func, bool) 
>> - 适用范围：除IE8及之前版本外的所有浏览器
>> - 三个参数 type是事件类型的字符串，不带“on”前缀；func是非立即执行事件处理程序，不带参数，如果强行需要带参数的话，可以在外面嵌套一个function(){//执行代码},然后参数直接写进执行代码中； bool值是true的话，那么函数将会注册为捕获事件处理程序，并在事件不同的调度阶段调用。不过一般我们会默认用false。[布尔值参数是true，表示在捕获阶段调用事件处理程序；就是最不具体的节点先接收事件，最具体的节点最后接收事件;如果是false，在冒泡阶段调用事件处理程序;则是先寻找指定的位置，由最具体的元素接收，然后逐级向上传播至最不具体的元素的节点（文档）。由图可知捕获过程要先于冒泡过程即，true的触发顺序在false前面](https://blog.csdn.net/qq_29606781/article/details/67650869)。
>>>>>> ![DOM事件流如图（剪自javascript高级程序设计）](http://images.cnitblog.com/i/187577/201407/110857551929664.png)
>> - 可以同时为事件对象注册相同类型的多个不同事件处理程序，但是如果连事件处理程序都相同的话那只能执行一个。
>> - 与之相对的还有removeEventListener(type, func, bool)，用于移除相关的监听器，由于需要捕获相关的事件，可以灵活使用bool=true，需要注意的是，removeEventListener函数与对应的addEventListener函数的第二个参数必须使用相同的引用，意味着不能直接把函数的定义全都写进去，必须在外面写好引用再传递过去。如：
        
        //当mousemove事件到来后，可以注销相关的时间处理程序
        var length = document.getElementsByName("newsrows").length;
                for(i=1; i<length+1; i++) {
                    (function() {
                        var newsrows=document.getElementById("newsrows_"+i);
                        var newsinterest=document.getElementById("newsinterest_"+i);
                        console.log(newsrows);
                        var newsinterest_mouseenter=function() {
                            newsinterest.style.visibility='visible';
                        };
                        var newsinterest_mouseleave=function() {
                            newsinterest.style.visibility="hidden";
                        };
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter, false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave, false);
                        newsrows.removeEventListener('mouseleave', newsinterest_mouseleave, false);
                    })();
                }
        
> - (4) attachEvent(type, func)与detachEvent(type, func) 
>> - 适用范围：IE5~IE8
>> - 与addEventListener和removeEventListener不同的地方有三个：A：attachEvent(type, func)与detachEvent(type, func)不支持事件捕获，所以只有两个参数；B：相同事件目标相同事件类型可以注册多个相同或者不相同的事件处理程序，注册的次数和函数的个数相同；attachEvent(type, func)与detachEvent(type, func)的事件类型需要有前缀“on”;
        
<h3 id='4.4'>4.4 循环绑定事件</h3>        
        
#### 1) [误区](https://www.cnblogs.com/yangjiewu/p/4753202.html)
> - 这段代码如果不仔细看的话会误以为三个按钮点击结果分别为0，1，2。但是运行结果却是3，3，3。我们来分析一下代码执行过程：前三遍循环分别给按钮0，1，2绑定了alert(i)的事件，第四遍循环开始时i=3，不符合i<=2的条件，因此终止循环。这里要注意的是，前三遍循环绑定的是alert(i)事件，而不是alert(0)，alert(1)，alert(2)，因为在绑定的过程中on的事件处理函数里的代码并没有运行，因此在触发click事件之前并不知道i等于几，代码此时只认为i是一个全局变量（实际上i的作用域为最外层的function）。上面分析了，当循环结束时i等于3，因此3个按钮点击均为alert(3)。
        
                <button id="0">0</button>
                <button id="1">1</button>
                <button id="2">2</button>
                <script> 
                $(function(){
                    for (var i=0; i<=2; i++) {
                        $("#" + i).on("click", function() {
                            alert(i);
                        });
                    };
                })
                </script>
#### 2) [原生的解决方案](https://www.cnblogs.com/yangjiewu/p/4753202.html)
> - 在on函数的外层写一个立即执行的函数，其目的是生成作用域，循环三遍即生成三个作用域，i的值由最下面的参数传入，三个作用域互不影响，因此也可以实现循环绑定的效果   
        
                for (var i=0; i<=2; i++) {
                    (function(i) {
                        $("#" + i).on("click", function(){
                            alert(i);
                        });
                    })(i);
                };
                
            或者：
                var length = document.getElementsByName("newsrows").length;
                for(i=1; i<length+1; i++) {
                    (function() {
                        var newsrows=document.getElementById("newsrows_"+i);
                        var newsinterest=document.getElementById("newsinterest_"+i);
                        console.log(newsrows);
                        var newsinterest_mouseenter=function() {
                            newsinterest.style.visibility='visible';
                        };
                        var newsinterest_mouseleave=function() {
                            newsinterest.style.visibility="hidden";
                        };
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter, false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave, false);
                    })();
                }
        
            或者：
                var newsrows=document.getElementsByName("newsrows");
                var newsinterest=document.getElementsByName("newsinterest");
                for(i=0; i<3; i++) {
                    (function(newsrows,newsinterest) {
                        var newsinterest_mouseenter=function() {
                            newsinterest.style.visibility='visible';
                        };
                        var newsinterest_mouseleave=function() {
                            newsinterest.style.visibility="hidden";
                        };
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter, false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave, false);
                    })(newsrows[i],newsinterest[i]);
                }
    
            或者：
                var newsrows=document.getElementsByName("newsrows");
                var newsinterest=document.getElementsByName("newsinterest");
                var newsinterest_mouseenter=function(e) {
                    e.style.visibility='visible';
                };
                var newsinterest_mouseleave=function(e) {
                    e.style.visibility="hidden";
                };
                for(i=0; i<3; i++) {
                    (function(newsrows,newsinterest) {
                        newsrows.addEventListener('mouseenter', function() {
                                                                    newsinterest_mouseenter(newsinterest);
                                                                }, false);
                        newsrows.addEventListener('mouseleave', function() {
                                                                    newsinterest_mouseleave(newsinterest);
                                                                }, false);
                    })(newsrows[i],newsinterest[i]);
                }
            或者：
                var newsrows=document.getElementsByName("newsrows");
                var newsinterest=document.getElementsByName("newsinterest");
                var newsinterest_mouseenter=function() {
                    this.style.visibility='visible';
                };
                var newsinterest_mouseleave=function() {
                    this.style.visibility="hidden";
                };
                for(i=0; i<3; i++) {
                    newsrows[i].addEventListener('mouseenter', newsinterest_mouseenter.bind(newsinterest[i]), false);
                    newsrows[i].addEventListener('mouseleave', newsinterest_mouseleave.bind(newsinterest[i]), false);
                }
        
<h3 id='4.5'>4.5 事件处理程序的调用</h3>                
        
#### 1) 事件对象
> - 事件对象用event表示，在IE8之前，当调用属性注册事件处理程序的时候，如果为传递event，则会通过全局对象window.event来获取事件对象：
        
                function() {
                    event = event || window.event;
                    //事件处理程序或事件监听程序代码；
                }
#### 2) 事件处理程序的运行环境
> - 运行环境一般就是事件目标，直白一点说即this关键字指的就是事件目标；
> - 但是在IE8及以前的attachEvent与detachEvent，this关键字指的却是全局Window对象，可以使用如下代码解决这个问题：
        
                function addEvent(target, type, handler) {
                        if(target.addEventListener()) {
                            target.addEventListener(type, handler, false);
                        }else {
                            target.attachEvent("on"+type,
                                    function(event) {
                                        return handler.call(target,event);
                                    }); //注意：该函数不能通过detachEvent函数进行解除，因为该函数的引用并没有保留下来；
                        }
                }

#### 3) 事件处理程序的作用域
> - 如果忘了JS的作用域可以[点击这里](https://www.cnblogs.com/skylar/p/3986087.html), 或者[这里](https://blog.csdn.net/qq_23980427/article/details/54645701),又或者是大名鼎鼎的[阮一峰同学的个人网站](http://es6.ruanyifeng.com/#docs/let)
> - 关于javascript中call()、apply()、bind()的用法理解可以[看这里](https://www.cnblogs.com/Shd-Study/archive/2017/03/16/6560808.html)
> - 像所有的JS函数一样，事件处理程序的在其定义时的作用域中执行，而非调用时的作用域
> - **扩展作用域**   HTML属性注册函数，实际上，这样扩展作用域的方式，无非就是让事件处理程序无需引用表单元素就能访问其他表单字段。
>>>>>> ![HTML属性注册函数作用域简要说明](https://pic2.zhimg.com/688ced70669d07c5659b8304dd75eed4_r.jpg)
    
#### 4) 调用顺序
> - 设置HTML标签属性为事件处理程序优先；
> - 使用addEventLisener()注册事件处理程序按照它们的注册顺序来调用；
> - 使用attachEvent()注册事件处理程序可能按照任何顺序调用；
        
#### 5) 事件传播的三个阶段
> - 第一阶段：事件捕获；
> - 第二阶段：目标对象本身的事件处理程序调用；
> - 第三阶段：事件冒泡；
> - [事件委托](https://www.cnblogs.com/liugang-vip/p/5616484.html)

#### 6) [事件取消](https://blog.csdn.net/wxl1555/article/details/53128966)
> - 取消浏览器的默认操作。event.preventDefault()方法。这是阻止默认事件的方法，调用此方法是，连接不会被打开，但是会发生冒泡，冒泡会传递到上一层的父元素。
        
                $(".box1 a").click(function(event){           
                    //阻止默认事件  
                    event.preventDefault();//页面不会跳转，但是会打印出1，  
                })；  
                              
                $(".box1").click(function(){  
                console.log("1")；                 
                });         

> - 取消事件传播，如果在同一对象上定义了其他处理程序，剩下的处理程序将依旧被调用，但是调用event.stopPropagation后其他对象的事件处理程序将不会被调用，另外该方法可以在事件传播的各个阶段被调用；
                
                $(".box1").click(function(){  
                    console.log("1")//不阻止事件冒泡会打印1，页面跳转;               
                });
    
                //阻止冒泡  
                $(".box1 a").click(function(event){  
                    event.stopPropagation();//不会打印1，但是页面会跳转；              
                });
    
            或者
                //event是事件对象
                box.onmouseover = function (event) {
                    // 阻止冒泡
                    event = event || window.event;
                    if(event && event.stopPropagation){
                        event.stopPropagation();    //IE不支持event.stopPropagation
                    }else{
                        event.cancelBubble = true;  //IE支持event.cancelBubble
                    }
                }
> - return false  这个方法比较暴力，他会同事阻止事件冒泡也会阻止默认事件；写上此代码，连接不会被打开，事件也不会传递到上一层的父元素；可以理解为return false就等于同时调用了event.stopPropagation()和event.preventDefault()
    
<h3 id='4.6'>4.6 文档加载事件</h3>                
        
#### 1) 执行顺序
> - 文档加载解析(同步下载JS脚本文件)完毕  -->   
> - 延迟（deferred）脚本执行完毕  -->   
> - document对象触发DOMContentLoaded事件，标志着程序执行从同步脚本执行阶段切换到异步事件驱动阶段，但是需要注意的是异步脚本没有执行完成  -->  
> - 文档完全解析完成，但浏览器还在等待相关资源的载入，如图片，还有异步脚本还在执行  --> 
> - 当所有资源载入和所有异步脚本执行完毕后，complete，Web浏览器触发Windows对象上的load事件  -->   
> - 调用异步事件，以异步相应客户的输入
>>>>>> ![图2-1 事件执行顺序.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-1%20%E4%BA%8B%E4%BB%B6%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8F.png?raw=true)
#### 2) 测试代码：
> - index.js代码：
        
                //index.js代码
                console.log("加载index.js完成");
> - HTML:代码：
                
                //HTML:代码
                <!DOCTYPE html>
                <html>
                <head>
                    <meta charset="utf-8">
                    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
                    <title>文档加载事件顺序</title>
                    <meta name="description" content=""/>
                    <meta name="keywords" content=""/>
                    <link href="./test.css" rel="stylesheet">
                    <script>
                            var i=0;
                            if(document.readyState === "loading") {
                                console.log("目前document.readyState = loading");
                            }
    
                            document.onreadystatechange = function () {
                                console.log("第"+(++i)+"次状态改变；");
                                console.log("目前document.readyState = "+document.readyState);   
                            }
    
                            document.addEventListener("DOMContentLoaded", function (event) {
                                console.log("初始DOM，加载并解析完成，触发DOMContentLoaded事件");
                            });
    
                            window.addEventListener("load", function (event) {
                                console.log("window 所有资源加载完成，触发Load事件");
                            });
    
    
                            window.addEventListener("beforeunload", function (event) {
                                console.log('即将关闭')
                                event.returnValue = "\o/";
                            });
    
                            window.addEventListener('unload', function (event) {
                                console.log('即将关闭1');
                            });
                        </script>    
                    </head>
        
                    <body>
                        <div id="root">dom事件</div>
                        <script src="./index.js"></script>
                    </body>
                </html>
> - 测试结果：
                
                //测试结果：
                Failed to load resource: net::ERR_FILE_NOT_FOUND

                目前document.readyState = loading

                index.js:8 加载index.js完成

                第1次状态改变；

                目前document.readyState = interactive

                初始DOM，加载并解析完成，触发DOMContentLoaded事件

                第2次状态改变；

                目前document.readyState = complete

                window 所有资源加载完成，触发Load事件

                即将关闭

<h3 id='4.7'>4.7 几种页面跳转的方法 具体请看<a href="https://blog.csdn.net/cordova/article/details/50853451">Mr_厚厚的博客</a></h3>                
        
#### 1) 定时跳转或者原地刷新
> - 对于刷新当前页面js控制为：
    
                window.location.reload();//刷新当前页面，重新向服务器请求数据
> - head标签内部的meta标签方式，定时刷新当前界面或刷新到另一个页面：
                
                // 3秒后跳转到another.html页面
                <meta charset="utf-8" http-equiv="refresh" content="3;url=another.html">    
#### 2) js手动替换跳转
> - 优点：灵活，可以结合更多的其他功能
> - 缺点：受到不同浏览器的影响
> - 上面的方法跳转会保留历史页面记录，通过返回键可以返回上一个界面，如果不想返回，直接替换页面的函数：
                
                //刷新当前页面，重新向服务器请求数据  
                window.location.replace("hello.html");

                或者
                window.location.href="hello.html";
#### 3) js手动新建跳转
> -    window.open(url);
    
                window.open("hello.html");
#### 4) 历史记录跳转
> - window.history.go():
    
                window.history.go(-1); // 返回上一页  
                  
                window.history.go(-2); // 返回上两页  
                  
                window.history.go("hello.html");// 跳转到hello.html  
> - window.history.back()
    
                window.history.back();

                等同于：window.history.go(-1);//返回上一页

                window.history.forward(); //返回下一页

        

------ 
            
<h2 id='5'> 五、脚本化CSS </h2>        
<h3 id='5.1'>5.1 脚本化内联样式</h3>    
        
#### 1) CSSStyleDeclaration对象
> - style是元素的属性，而CSSStyleDeclaration是style的属性，如：
        
                e.style.fontSize = "24pt";
> - CSSStyleDeclaration对象的值都是字符串  
> - 复合属性
        
                 e.style.border = topMargin + "px " + bottomMargin + "px "
                        + leftMargin + "px " + rightMargin + "px"; 
> - 内联样式的优先级一般都会比样式表的要高；
#### 2) cssText 具体的可以看[这里](https://www.cnblogs.com/majingyi/p/6840818.html)
> - cssText 的本质就是设置 HTML 元素的 style 属性值，
        
                obj.style.cssText=”样式”;
                element.style.cssText=”width:20px;height:20px;border:solid 1px red;”;  
> - 但是，这样会有一个问题，会把原有的cssText清掉，比如原来的style中有’display:none;’，那么执行完上面的JS后，display就被删掉了。为了解决这个问题，可以采用cssText累加的方法：
        
                 Element.style.cssText += ‘width:100px;height:100px;top:100px;left:100px;’
> - 因此，上面cssText累加的方法在IE中是无效的。最后，可以在前面添加一个分号来解决这个问题：
        
                Element.style.cssText += ‘;width:100px;height:100px;top:100px;left:100px;’
> - 再进一步，如果前面有样式表文件写着 div { text-decoration:underline; }，这个会被覆盖吗？不会！因为它不是直接作用于 HTML 元素的 style 属性。
> - 内联样式的setter和getter
        
                //setter
                e.setAttribute("style", s);
                e.style.cssText = s;

                //getter
                s = e.getAttribute("style");
                s = e.style.cssText;

#### 3) window.getComputedStyle(element, 伪元素)
> - 这个属性是属于浏览器窗口的，第一个参数是你想要计算的元素，第二个参数表示第一个参数的伪元素，但也可以是null或者是空字符串，最后返回一个CSSStyleDeclaration对象
> - 所以可以利用返回的CSSStyleDeclaration对象来读取某个具体的属性，如font-size；
> - 计算样式的CSSStyleDeclaration对象和内联元素的CSSStyleDeclaration对象是有区别的
>> - 计算样式的属性是只读的
>> - 计算样式的值是绝对值，这意味着单位是px或者“rgb(#, #, #)” 或者“rgba(#, #, #, #)”
>> - 不计算复合属性，也就是说不能直接返回margin属性，只能基于基本属性，如：margin-left;
>> - 计算样式的cssText属性没有定义；
>> - 在IE8及之前没有实现           
#### 4) currentStyle 具体的可以看[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/)
> - currentStyle是IE浏览器自娱自乐的一个属性，其与element.style可以说是近亲，至少在使用形式上类似，element.currentStyle，差别在于element.currentStyle返回的是元素当前应用的最终CSS属性值（包括外链CSS文件，页面中嵌入的style元素的属性等）。
> - 因此，从作用上讲，getComputedStyle方法与currentStyle属性走的很近，形式上则style与currentStyle走的近。不过，currentStyle属性貌似不支持伪类样式获取，这是与getComputedStyle方法的差异，也是jQuery css()方法无法体现的一点。  
#### 5) getPropertyValue方法 具体的可以看[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/)
> - getPropertyValue方法可以获取CSS样式申明对象上的属性值（直接属性名称），例如：
        
                window.getComputedStyle(element, null).getPropertyValue("float");
> - 如果我们不使用getPropertyValue方法，直接使用键值访问，其实也是可以的。但是，比如这里的的float，如果使用键值访问，则不能直接使用getComputedStyle(element, null).float，而应该是cssFloat与styleFloat，自然需要浏览器判断了，比较折腾！
> - 使用getPropertyValue方法不必可以驼峰书写形式（不支持驼峰写法），例如：style.getPropertyValue("border-top-left-radius");
        
<h3 id='5.2'>5.2 脚本化CSS类</h3>    
        
#### 1) className
> - 直接方法
        
                e.className = "某类名1 某类名2"；
> - 直接方法有个缺点，它会覆盖原有的方法
#### 2) classList 具体的可以看[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2013/07/domtokenlist-html5-dom-classlist-%E7%B1%BB%E5%90%8D/)
> - HTML5中为每个元素都定义了classList，该属性值是DOMTokenList对象————一个只读的类数组对象
> - classList的返回值显示，其本质上是DOMTokenList – DOM标记列表.
> - DOMTokenList这种类型表示一组空间分隔的标记。通常由HTMLElement.classList, HTMLLinkElement.relList, HTMLAnchorElement.relList或HTMLAreaElement.relList返回。从0开始的类JavaScript数组索引。DOMTokenList始终是区分大小写的。
> - 在FireFox以及Chrome下，我们执行typeof DOMTokenList的结果是："function"; 但是在IE10下，却是："object".IE10 DOMTokenList对象类型同时虽然typeof结果为"function"，但是执行DOMTokenList()会报”Illegal constructor”错误；IE10执行DOMTokenList()也会报错，错误是”缺少函数”。因此，试图通过typeof obj == "function"来判断obj就是个函数的做法是不完全正确的。
                
                //在控制台中输入
                document.getElementById('newsrows_1').classList；
                document.getElementById('newsrows_1').classList.item(0);

                //返回结果
                DOMTokenList ["newsrows2", value: "newsrows2"]
                "newsrows2"

                //DOMTokenList被暴露的属性
                __proto__: DOMTokenList     
                0: "newsrows2"
                length: 1
                value: "newsrows2"
                add:ƒ add()
                contains: ƒ contains()
                entries: ƒ entries()
                forEach: ƒ forEach()
                item: ƒ item()
                keys: ƒ keys()
                length: (...)
                remove: ƒ remove()
                replace: ƒ replace()
                supports: ƒ supports()
                toString: ƒ toString()
                toggle: ƒ toggle()
                value: (...)
                values: ƒ values()
                constructor: ƒ DOMTokenList()
                Symbol(Symbol.iterator): ƒ values()
                Symbol(Symbol.toStringTag): "DOMTokenList"
                get length: ƒ ()
                get value: ƒ ()
                set value: ƒ ()
                __proto__: Object

> - 拥有add()和remove()方法
        
                document.body.classList.add("c");
                document.body.classList.length    // 3
> - classList的局限
>> - classList除了上面提到的不能级联这个无关痛痒的局限外，还有个比较头疼的局限，就是不能一次add或remove或toggle多个类名。//zxx: 级联指的是$().a().b().c()这种可以连在一起调用方法的写法。例如：
        
                document.body.classList.add("c d");    // Error: String contains an invalid character
                document.body.classList.add("c\x20d");   // Error: String contains an invalid character
                document.body.classList.remove("c d");    // Error: String contains an invalid character
>> - 我们要想多类名处理，需要一个一个来，例如：
        
                var clList = document.body.classList;
                clList.add("d");
                clList.add("e");
        
<h3 id='5.3'>5.3 脚本化样式表 具体看<a href="https://www.cnblogs.com/limingxi/p/4526518.html">李明夕同学的博客</a></h3>    
        
#### 1) document.styleSheets
> - 它是一个只读的类数组对象——CSSStyleSheet，表示与文档关联在一起的样式表，可以定义或者引用link元素或者style元素的title属性值       
#### 2) 开启和关闭样式表
            
                //关闭样式表
                document.styleSheets[0].disabled = true;

                //查询样式表
                document.styleSheets[0].href
                "http://localhost:8080/CompatTest/BaiduHomePage.css"
#### 3) 查询
> - 数组的元素是CSSStyleSheet对象，CSSStyleSheet对象有一个cssRule[]数组，包含如@import和@page等指令，在IE中使用rules[]代替cssRule[]，但是区别在于IE的rules[]只包含样式表中实际存在样式规则；
                
                document.styleSheets[0].cssRules[0]

    //结果
    CSSStyleRule {selectorText: "body", style: CSSStyleDeclaration, styleMap: StylePropertyMap, type: 1, cssText: "body { background: pink; }", …}
    cssText: "body { background: pink; }"
    parentRule: null
    parentStyleSheet: CSSStyleSheet {disable: true, ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", …}
    selectorText: "body"
    style: CSSStyleDeclaration {0: "background-image", 1: "background-position-x", 2: "background-position-y", 3: "background-size", 4: "background-repeat-x", 5: "background-repeat-y", 6: "background-attachment", 7: "background-origin", 8: "background-clip", 9: "background-color", alignContent: "", alignItems: "", alignSelf: "", alignmentBaseline: "", all: "", …}
    styleMap: StylePropertyMap {size: 10}
    type: 1
    __proto__: CSSStyleRule
> - 更加具体的查询相关属性
        
                document.styleSheets[0].cssRules[0].cssText;

    //结果
    "body { background: pink; }"

                document.styleSheets[0].cssRules[0].style.cssText;

    //结果
    background: pink;
> - 遍历样式表
                
                var ss = document.styleSheets[0];
                var rules = ss.cssRules?ss.cssRules:ss.rules;
                for(var i = 0; i < rules.length; i++) {
                    if(!rules[i].selectorText) {
                        continue;
                    } 
                    var selector = rules[i].selectorText; 
                    var ruleText = rules[i].style.cssText;
                    console.log(selector+": {" + ruleText + "}")};

    //结果
    body: {background: pink;}
    body: {background: yellow;}
    .top: {padding-right: 95px; min-width: 1000px; height: 30px; font-family: sans-serif; font-size: 12px; line-height: 0px; border-bottom: 1px solid rgb(231, 231, 231);}
    .top a: {padding: 0px 0.5em; line-height: 30px; vertical-align: middle; color: black;}
    .weatherclick: {display: inline-block; margin-left: 15px; padding-right: 7px; text-decoration: none; line-height: 20px !important;}
    .weatherclick:hover: {background: pink;}
    .icon: {display: inline-block; width: 20px; height: 20px; vertical-align: bottom; background: url("https://ss0.bdstatic.com/k4oZeXSm1A5BphGlnYG/icon/weather/aladdin/png_18/a0.png") no-repeat;}
    .weatherquality: {color: rgb(186, 220, 0); margin-left: 7px; margin-right: 7px;}
    .weatherqualitynumber::after: {content: ""; font-size: 10px; border-right: 1px solid black; padding-left: 1em;}
    .toprightlist: {float: right; height: 30px; line-height: 30px; text-align: center; overflow: hidden;}
    .toprightlist:hover: {overflow: visible;}
    .triangle: {width: 0px; border-bottom: 8px solid rgb(153, 153, 153); border-left: 4px solid transparent; border-right: 4px solid transparent; margin-left: auto; margin-right: auto;}
    .outertriangle: {width: 0px; border-bottom: 8px solid rgb(153, 153, 153); border-left: 8px solid transparent; border-right: 8px solid transparent; margin-left: auto; margin-right: auto;}
    .innertriangle: {position: relative; margin-top: -7px; margin-left: auto; margin-right: auto; width: 0px; border-bottom: 7px solid white; border-left: 7px solid transparent; border-right: 7px solid transparent;}
    .toprightlist .itembox: {display: inline-block; margin-top: -1px; line-height: 30px; text-decoration: none; border: 1px solid rgb(153, 153, 153); box-shadow: rgb(153, 153, 153) 2px 2px 2px;}
    .toprightlist li: {display: block; text-align: center;}
    .toprightlist li a: {text-decoration: none;}
    .toprightlink: {float: right; font-size: 14px; line-height: 30px;}
    .productbox: {position: absolute; top: 0px; right: 0px; height: 30px; width: 85px; color: white; background: rgb(57, 139, 251); overflow: hidden;}
    .productbox:hover: {float: none; bottom: 0px; height: 100%; color: black; background: rgb(240, 240, 240);}
    .productupbox: {width: 100%; height: 31px; line-height: 30px; text-align: center;}
    .productupbox span: {font-size: 13px; vertical-align: middle;}
    .productdownbox: {height: 100%; background: rgb(240, 240, 240); overflow: auto;}
    .productdownboxcontent: {height: 700px; width: 65px; margin-left: 10px; background: rgb(240, 240, 240);}
    .productdownboxcontent a: {display: block; padding: 10px 0px; font-size: 12px; color: black; text-align: center; text-decoration: none; border-bottom: 1px solid rgb(231, 231, 231);}
    .productdownboxcontent a:first-child: {margin-top: 10px; border-top: 1px solid rgb(231, 231, 231);}
    .logozone: {margin: 70px auto auto; height: 151px; line-height: 151px; width: 641px; text-align: center;}
    .logozone img: {width: 270px; height: 129px; vertical-align: middle;}
    .searchform: {position: relative; margin: 0px auto; width: 641px; height: 40px; font-size: 0px; text-align: left;}
    .searchinput: {width: 523px; height: 20px; padding: 9px 7px; font-size: 16px; vertical-align: top; border: 1px solid rgb(184, 184, 184);}
    .searchicon: {position: absolute; top: 0px; right: 111px; bottom: 0px; margin: auto; height: 16px; width: 18px; background: -webkit-image-set(url("https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/static/protocol/https/soutu/img/camera_new_5606e8f.png") 1x, url("https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/static/protocol/https/soutu/img/camera_new_x2_fb6c085.png") 2x) no-repeat rgb(255, 255, 255); cursor: pointer;}
    .searchbutton: {display: inline-block; cursor: pointer; margin: 0px; padding: 0px; width: 102px; height: 40px; font-size: 16px; vertical-align: top; color: white; background-color: rgb(51, 136, 255); border: 0px;}
    .contentbox: {margin: 100px auto auto; width: 896px; height: 404px; overflow: hidden; border: 1px solid rgb(231, 231, 231);}
    .contentboxtopbar: {height: 40px; font-size: 0px; line-height: 0; border-bottom: 1px solid rgb(231, 231, 231);}
    .myfocus, .myrecommand, .mynavigation: {display: inline-block; zoom: 1; width: 80px; height: 40px; font-size: 14px; line-height: 40px; color: rgb(51, 51, 51); vertical-align: top; text-align: center; cursor: pointer;}
    .myfocus: {width: 124px;}
    .myrecommand: {color: white; background: rgb(157, 157, 157);}
    .myfocuslogo: {width: 17px; height: 17px; background: url("picture/myfocus_a2.png") 1px 0px no-repeat;}
    .myfocus > *, .myrecommand > *, .mynavigation > *: {vertical-align: middle;}
    .myfocus:hover, .myrecommand:hover, .mynavigation:hover: {font-weight: bold; color: white; background: rgb(190, 190, 190);}
    .contentfocusbox: {display: inline-block; margin-top: 20px; margin-right: 5px; width: 100%;}
    .contentfocusbox aside: {float: right; display: inline-block; width: 300px;}
    .title-text, .hot-refresh, .hot-refresh-text: {color: black; text-decoration: none;}
    .title-text: {font-size: 14px; font-weight: bold;}
    .hot-refresh: {display: block; float: right; height: 22px; padding-top: 3px; padding-right: 30px; width: 60px; cursor: pointer;}
    .hot-refresh-icon: {width: 20px; height: 16px; background: url("https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/mantpl/img/news/news_88aeb6fe.png") -23px -25px no-repeat; vertical-align: bottom;}
    .hot-refresh-text: {font-size: 13px; width: 40px; text-align: center; white-space: nowrap;}
    .newslistul: {float: left; padding-top: 20px; padding-right: 5px; width: 300px;}
    .newslistli: {float: left; display: inline-block; margin-right: 3px; zoom: 1; width: 145px; height: 34px;}
    .newslistli > *: {vertical-align: middle;}
    .newslistli a: {max-width: 113px; font-size: 14px; color: rgb(51, 51, 51); text-overflow: ellipsis; text-decoration: none;}
    .newslistli a:hover: {color: rgb(51, 153, 204); text-decoration: underline; font-weight: bold;}
    .contentfocusboxleftside: {padding: 0px 25px; height: 100px; font-size: 0px;}
    .contentfocusboxleftsidetop: {font-size: 13px; color: rgba(0, 0, 0, 0.4);}
    .contentfocusboxleftsidetop > *: {vertical-align: middle;}
    .line: {display: inline-block; height: 0px; width: 172px; font-size: 0px; border-bottom: 1px solid rgb(226, 226, 226);}
    .baiduicon: {margin: 0px 6px; height: 14px; width: 14px; background: url("picture/zhuazi2.png") 1px 0px no-repeat;}
    .newstable: {float: left; text-align: left; width: 535px;}
    .hot-point: {padding: 0px 2px; font-size: 12px; line-height: 12px; color: rgb(241, 63, 64); border: 1px solid rgb(239, 185, 185); border-radius: 3px;}
    .newsrows1title, .newsrows2title: {width: 100%; font-family: arial, "Microsoft Yahei", 微软雅黑; font-size: 18px; color: rgb(51, 51, 51); font-weight: bold; line-height: 53.6px; vertical-align: middle; text-decoration: none; text-overflow: ellipsis;}
    .newsrows2title: {line-height: 24px;}
    .newsrows1, .newsrows2: {padding-top: 8px; border-bottom: 1px solid rgb(226, 226, 226);}
    .newsrows1picture: {font-size: 3px;}
    .newsrows1 footer, .newsrows2 footer: {padding-top: 10px; padding-bottom: 19px; height: 15px; line-height: 15px; font-size: 13px; color: rgba(0, 0, 0, 0.4);}
    .newsrows1 footer img, .newsrows2 footer img: {float: right; width: 19px; height: 15px; background: url("https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/mantpl/img/news/dustbin_new_41cbcb37.png") 0px -19px no-repeat; visibility: hidden;}
    .src-net, .src-time: {margin-right: 10px; line-height: 15px; font-size: 13px; text-decoration: none; color: rgba(0, 0, 0, 0.4);}
    .newsrows2: {display: table; zoom: 1; min-height: 140px; overflow: hidden;}
    .newsrows2picture: {display: table-cell; padding: 20px 0px; vertical-align: middle; zoom: 1;}
    .newsrows2textzone: {display: table-cell; padding-left: 21px; zoom: 1; width: 337px; vertical-align: middle;}
    .morebar: {padding-top: 20px; margin: auto; cursor: pointer; width: 90px; height: 45px; text-align: center;}
    .morebartext: {font-size: 12px; color: rgb(153, 153, 153);}
    .morebartexttriangele: {height: 18px; width: 34px; margin: 10px auto 0px; border: 0px; font-size: 0px;}
    .morebaroutertriangele: {position: relative; margin: 0px; padding: 0px; width: 0px; border-width: 16px; border-style: solid; border-color: black transparent transparent; border-image: initial;}
    .morebarinnertriangele: {position: absolute; top: -16px; left: -15px; margin: 0px; padding: 0px; width: 0px; border-width: 15px; border-style: solid; border-color: white transparent transparent; border-image: initial;}
    .myfooter: {margin: 70px auto; color: rgb(153, 153, 153); zoom: 1; font-size: 12px; text-align: center;}
    .myfooter *: {vertical-align: middle; color: rgb(153, 153, 153); line-height: 19px;}
    .ICPlogo: {display: inline-block; width: 19px; height: 19px; background: url("picture/ICPlogo2.png") 3px 0px no-repeat rgb(255, 255, 255);}
    .sercuelogo: {display: inline-block; width: 20px; height: 20px; background: url("picture/surcue2.png") 3px 0px no-repeat rgb(255, 255, 255);}

#### 4) 获取样式表
> - 我们可以选择向页面内的某条stylesheet中添加样式。可以给link标签或者style标签添加ID，通过引用节点的sheet属性来获取CSSStyleSheet对象。页面中的stylesheets可以使用document.styleSheets来获取
#### 5) 添加样式表
> - 有些情况下，可能新建一个style节点来承装新添加的style rule。方法很简单：
    
                var addStyles = (function(styles) {
                    
                    var styleSheet, styleElt;
                    if(document.createStyleSheet) {
                        var styleSheet = document.createStyleSheet();
                    }else{

                        // Create the <style> tag
                        styleElt = document.createElement("style");
                        styleElt.appendChild(document.createTextNode(""));
                        document.head.appendChild(styleElt);

                        //新的样式表应该是最后一个
                        styleSheet = document.styleSheets[document.styleSheets.length-1];
                    }
    
                        //向样式表插入样式
                        if(typeof styles === "string") {
                            if(styleElt) {
                                styleElt.innerHTML = styles;
                            }else {
                                styleSheet.cssText = styles; //IE API
                            }
                        }else {

                            //强制使用insertRule或者addRule插入
                        }
                })("body {background: pink;}");  
#### 6) 插入样式表
> - **insertRule(styles,[index])** Stylesheets对象提供了insertRule（译者注：IE8及以下不兼容，具体参考链接http://www.quirksmode.org/dom/w3c_css.html ）
> - **方法** insertRule函数要求传入css样式风格的str作为参数。
> - **具体调用方法**：
        
               document.styleSheets[0].insertRule("body {background:pink;}", 1);
                //（译者注：传入的样式str的格式要求很多。就我目前发现的：
                // 1.{}两个花括号和前后最好都有一个空格 
                // 2.如果是webkit内核，函数在解析带有-moz-前缀的样式规则时会抛err）

                //结果
                body {
                    background: yellow;
                }
> - 这种方法看上去有点丑，但是确实有用。第二个参数Index，表示我们将在样式内部的哪一条插入新样式css rule，这就可以帮助我们实现原有样式的覆盖。默认index取值是-1(译者注：但是输入-1在chrome 41下抛了err，提示参数不能小于0，这里值得在研究一下)，表示默认在样式最后追加。如果想强制覆盖，可以使用！important，来避免插入次序引起其他问题。
> - **非标准函数  addRule(selector,styles,index)**  CSSStyleSheet对象有一个非标准函数addRule，和insertRule相比，它更像js api的调用风格，无需自己注意插入的样式字符串的格式。addRule方法接受三个参数，分别是选择器selector，样式字符串"color:red;font-size:12px",和插入次序index。
                
                document.styleSheets[0].addRule("body", "background: white;", 4);
                //方法有返回值，为-1。但是没有什么具体含义。
                //这种方式可以快速高效的改变页面上节点的已有样式。

                //结果
                body {
                    background: white;
                }
> - **应用样式** 因为上面提到两个函数都不是常见api函数，所以需要做浏览器兼容性处理。这种方法可以应用于所有高级的浏览器，如果还是有担心的话，可以在调用时使用try-catch结构
        
                function addCSSRule(sheet, selector, rules, index) {
                    if("insertRule" in sheet) {
                        sheet.insertRule(selector + "{" + rules + "}", index);
                    }
                    else if("addRule" in sheet) {
                        sheet.addRule(selector, rules, index);
                    }
                }

                // Use it!
                addCSSRule(document.styleSheets[0], "header", "float: left");
#### 7) 删除样式表
> - 直接删除样式表中一整条规则，包括里面的各个属性　　
            
                document.styleSheets[索引].deleteRule(索引);
                或者
                //仅对IE有效
                document.styleSheets[索引].removeRule(索引);

        
------      
         
        
<h2 id='6'> 六、HTTP脚本化 </h2>
<h3 id='6.1'>6.1 Ajax和Comet</h3>  

#### 1) Ajax 
> - Ajax Asynchronous JavaScript and XML，是一种使用脚本操纵HTTP的Web应用架构
> - 主要特点是使用脚本操纵HTTP和Web服务器进行数据Ajax Asynchronous JavaScript and XML，交换，不会导致页面重载。
> - 方向是从client指向server；
> - 异步
#### 2) Comet 
> - 也是一种使用脚本操纵HTTP的Web应用架构
> - 方向跟Ajax相反，server指向client
> - 在Comet中，Web服务器发起通信并异步发送消息到客户端。如果Web应用需要响应服务端发送的消息，则会利用Ajax技术发送或者请求数据
> - 服务器保持打开直到它需要推送一条消息，服务器每发送完一条消息就关闭连接，这样可以确保客户端正确接收到消息，处理该消息之后，客户端马上为后续的消息推送建立一个新的连接。
> - 异步
#### 3) 实现方式
> - img标签的src属性，通过URL用GET的方式传递消息给server，server必须返回一个图片作为请求结果，而且这个图片必须不可见，因为我只需要把信息从client指向server，不需要返回的消息，所以这个图片一般是一个1 X 1像素的透明图片。这种类型的图片又叫做网页信标(Web bug)，通常用于统计点击次数或者网站流量分析。但是它也有自己的缺陷，就是没办法返回有用的响应信息；
> - iframe元素更为强大，利用src属性设置URL，可以使用server返回的文档并从中读取有用的信息。一般把iframe元素设置为不可见即可，但是它也有一个限制：受同源策略的限制；
> - script元素，利用src属性设置URL并发起HTTP GET请求，由于其有规避同源策略的能力，且不受同源策略的限制
        
<h3 id='6.2'>6.2 XMLHttpRequest</h3>         
        
#### 1) XMLHttpRequest类
> - 浏览器的XMLHttpRequest类定义了它们的HTTP API。这个类的每个实例都表示一个独立的请求/响应对，并且允许指定请求细节和提取响应数据
        
                var httpRequest = new XMLHttpRequest();
> - 你也能重用之前的实例，但是这样的话会终止之前通过该对象挂起的任何请求。
#### 2) 请求
> - 由四部分组成：
>> - HTTP请求方法或动作；
>> - 正在请求的URL；
>> - 一个可选的请求头集合(表明请求主题的类型，以便server调用合适的程序进行处理)，其中包括身份验证的消息；
>> - 一个可选的请求主体
> - open(method, url)的第一个参数指定HTTP方法和动作，没有大小写的区分，但一般用大写。具体可以看[默默淡然的博客](https://www.cnblogs.com/liangxiaofeng/p/5798607.html)
>> - GET 用于常规请求，适用于当URL完全指定请求资源，当请求对server没有副作用以及当server的响应可缓存
>> - POST 常用于表单，请求主体中包含表单数据且这些数据需要存储到server中，这也就是所谓的副作用，同时不应该缓存使用这个方法的请求
>>>>>> ![图6-2 GET和POST的区别](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE6-2%20GET%E5%92%8CPOST%E7%9A%84%E5%8C%BA%E5%88%AB.png?raw=true)
>> - DELETE 请求服务器删除Request-URI所标识的资源。 
>> - HEAD 向服务器索要与GET请求相一致的响应，只不过响应体将不会被返回。这一方法可以在不必传输整个响应内容的情况下，就可以获取包含在响应消息头中的元信息。
>> - OPTIONS 返回服务器针对特定资源所支持的HTTP请求方法。也可以利用向Web服务器发送'*'的请求来测试服务器的功能性。
>> - PUT [跟POST方法很像，也是向服务器提交数据。但是，它们之间有不同。PUT指定了资源在服务器上的位置，而POST没有。PUT方法请求服务器去把请求里的实体存储在请求,URI（Request-URI）标识下。如果请求URI（Request-URI）指定的的资源已经在源服务器上存在，那么此请求里的实体应该被当作是源服务器关于此URI所指定资源,实体的最新修改版本。如果请求RI（Request-URI）指定的资源不存在，并且此URI被用户代理定义为一个新资源，那么源服务器就应该根据请求里的实体创建一个此URI所标识下的资源。如果一个新的资源被创建了，源服务器必须能向用户代理（user agent）发送201（已创建）响应。如果已存在的资源被改变了，那么源服务器应该发送200（Ok）或者204（无内容）响应。如果资源不能根据请求URI创建或者改变，一个合适的错误响应应该给出以反应问题的性质。实体的接收者不能忽略任何它不理解和不能实现的Content-*（如：Content-Range）头域，并且必须返回501（没有被实现）响应。如果请求穿过一个缓存（cache），并且此请求URI（Request-URI）指示了一个或多个当前缓存的实体，那么这些实体应该被看作是旧的。PUT方法的响应是不可缓存的。POST方法和PUT方法请求最根本的区别是请求URI（Request-URI）的含义不同。POST请求里的URI 指示一个能处理请求实体的资源（译注：此资源可能是一段程序，如jsp 里的servlet。此资源可能是一个数据接收过程，一个网关（gateway，译注：网关和代理的区别是：网关可以进行协议转换，而代理不能，只是起代理的作用，比如缓存服务器其实就是一个代理），或者一个单独接收注释的实体。对比而言，PUT方法请求里的URI标识请求里封装的实体一一用户代理知道URI意指什么，并且服务器不能把此请求应用于其它资源（resource）。如果服务器期望请求被应用于一个不同的URI，那么它必须发送301（永久移动）响应；用户代理可以自己决定是否重定向请求。一个单独的资  
源可能会被许多不同的URI指定。如：一篇文章可能会有一个URI指定当前版本，而这个URI区别于这篇文章其它特殊版本的URI。这种情况下，对一个通用URI的PUT请求可能会导致其资源的其它URI请求被源服务器重定义。HTTP/1.1没有定义PUT方法对源服务器的状态影响。PUT方法请求里的实体头域应该被用于资源的创建或修改。](https://blog.csdn.net/resilient/article/details/52585724)  
>> - TRACE 由于危险被禁止，回显服务器收到的请求，主要用于测试或诊断。 
>> - CONNECT 由于危险被禁止，HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
>> - TRACK 由于危险被禁止
> - setRequestHeader(header, value)，它可以进行多次请求，而且后者并不会覆盖前者，这些请求头主要包括：
>> - "Content-Type"，其值为MIME类型，如"text/plain"
>> - 但是自己不能指定其他请求头，如"Content-Length"，"Date"，"Referer"或者"User-Agent"等，原因是XMLHtmlRequest为了避免请求头被伪造
        
                //General
                Request URL: http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html
                Request Method: GET
                Status Code: 304 
                Remote Address: 103.46.128.47:51688
                Referrer Policy: no-referrer-when-downgrade

                //Request Headers
                GET /CompatTest/BaiduHomePage.html HTTP/1.1
                Host: hblvsjtu.picp.io:51688
                Connection: keep-alive
                Cache-Control: max-age=0
                Upgrade-Insecure-Requests: 1
                User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.117 Safari/537.36
                Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
                Accept-Encoding: gzip, deflate
                Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
                If-None-Match: W/"28460-1524908730654"
                If-Modified-Since: Sat, 28 Apr 2018 09:45:30 GMTSafari/537.36
        
> - send(body) 
>> - GET请求绝对没有主体，所以send(null)或者send()
>> - POST请求通常拥有主体，同时它应该匹配使用setRequestHeader()指定的"Content-Type"头
> - 例子：
             
             var postMeg = function(msg) {
                var httpRequest = new XMLHttpRequest();
                httpRequest.open("POST", "http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html");
                httpRequest.setRequestHeader("Content-Type", "text/plain;charset=UTF-8");
                httpRequest.send(msg);
             }
> - 顺序问题 先是请求方法和URL到达，然后是请求头，最后是请求主体。XMLHTMLRequest类直到调用send()方法的时候才开始启动网络。请求头必须在调用open()方法之后send()方法之前
#### 3) 响应
> - 由三部分组成：
>> - 由数字或者文字组成的状态码，用来显式请求的成功或者失败
>> - 一个响应头头集合
>> - 响应主体               
> - 例子：                              
    
                //General
                Request URL: http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html
                Request Method: GET
                Status Code: 304 
                Remote Address: 103.46.128.47:51688
                Referrer Policy: no-referrer-when-downgrade

                //Response Headers
                HTTP/1.1 304
                ETag: W/"28460-1524908730654"
                Date: Sun, 29 Apr 2018 02:48:21 GMT                                                           
> - 数字status或者文字statusText组成的状态码 
        
<center>**[HTTP状态码分类](http://www.runoob.com/http/http-status-codes.html)**</center>
>> 分类|分类描述
>> -|-
>> 1** |信息，服务器收到请求，需要请求者继续执行操作
>> 2** |成功，操作被成功接收并处理
>> 3** |重定向，需要进一步的操作以完成请求
>> 4** |客户端错误，请求包含语法错误或无法完成请求
>> 5** |服务器错误，服务器在处理请求的过程中发生了错误
    
<center>**[HTTP状态码列表](http://www.runoob.com/http/http-status-codes.html)**</center>
>> 状态码 | 状态码英文名称 | 中文描述
>> -|-|-
>> 100 | Continue | 继续。客户端应继续其请求
>> 101 | Switching Protocols | 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议
>> 200 | OK | 请求成功。一般用于GET与POST请求
>> 201 | Created | 已创建。成功请求并创建了新的资源
>> 202 | Accepted | 已接受。已经接受请求，但未处理完成
>> 203 | Non-Authoritative Information | 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本
>> 204 | No Content | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档
>> 205 | Reset Content | 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域
>> 206 | Partial Content | 部分内容。服务器成功处理了部分GET请求
>> 300 | Multiple Choices | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择
>> 301 | Moved Permanently | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替
>> 302 | Found | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
>> 303 | See Other | 查看其它地址。与301类似。使用GET和POST请求查看
>> 304 | Not Modified | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
>> 305 | Use Proxy | 使用代理。所请求的资源必须通过代理访问
>> 306 | Unused | 已经被废弃的HTTP状态码
>> 307 | Temporary Redirect | 临时重定向。与302类似。使用GET请求重定向
>> 400 | Bad Request | 客户端请求的语法错误，服务器无法理解
>> 401 | Unauthorized | 请求要求用户的身份认证
>> 402 | Payment Required | 保留，将来使用
>> 403 | Forbidden | 服务器理解请求客户端的请求，但是拒绝执行此请求
>> 404 | Not Found | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
>> 405 | Method Not Allowed | 客户端请求中的方法被禁止
>> 406 | Not Acceptable | 服务器无法根据客户端请求的内容特性完成请求
>> 407 | Proxy Authentication Required | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
>> 408 | Request Time-out | 服务器等待客户端发送的请求时间过长，超时
>> 409 | Conflict |  服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突
>> 410 | Gone | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置
>> 411 | Length Required | 服务器无法处理客户端发送的不带Content-Length的请求信息
>> 412 | Precondition Failed | 客户端请求信息的先决条件错误
>> 413 | Request Entity Too Large | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息
>> 414 | Request-URI Too Large | 请求的URI过长（URI通常为网址），服务器无法处理
>> 415 | Unsupported Media Type | 服务器无法处理请求附带的媒体格式
>> 416 | Requested range not satisfiable | 客户端请求的范围无效
>> 417 | Expectation Failed | 服务器无法满足Expect的请求头信息
>> 500 | Internal Server Error | 服务器内部错误，无法完成请求
>> 501 | Not Implemented | 服务器不支持请求的功能，无法完成请求
>> 502 | Bad Gateway | 充当网关或代理的服务器，从远端服务器接收到了一个无效的请求
>> 503 | Service Unavailable | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中
>> 504 | Gateway Time-out | 充当网关或代理的服务器，未及时从远端服务器获取请求
>> 505 | HTTP Version not supported | 服务器不支持请求的HTTP协议的版本，无法完成处理









