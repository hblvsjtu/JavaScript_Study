# JavaScript框架设计_Study 
  
  
### 作者：冰红茶  
### 参考书籍：《JavaScript框架设计》 司徒正美   

------    



   看完了《javascript权威指南》，算是对JS有了基本的知识体系。不过知识还是零件，想要进入下一层次，就必须要学习如何利用零件去建造一些实用的工具。“在前端最能反映实力的就是框架”，所以我选择了司徒正美老师的《JavaScript框架设计》。现在就来打造属于自己的工具吧^_ ^
  
## 目录

## [一、种子模块](#1)
### [1.1 模块化](#1.1)
### [1.2 对象拓展](#1.2) 
### [1.3 数组化](#1.3) 
### [1.4 类型的判断](#1.4)
### [1.5 无冲突处理](#1.5)
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
### [6.3 编码请求主体](#6.3)      
### [6.4 HTTP进度事件](#6.4)
### [6.5 跨域请求](#6.5)
## [七、客户端储存](#7)
### [7.1 客户端储存简介](#7.1)
### [7.2 localStorage和sessionStorage](#7.2) 
### [7.3 cookie](#7.3)      
### [7.4 应用程存储和离线Web应用](#7.4)
## [八、HTML5 API](#8)
### [8.1 地理位置](#8.1)
### [8.2 历史记录管理](#8.2) 
### [8.3 跨域消息传递](#8.3)      
### [8.4 Web Worker](#8.4)
### [8.5 类型化数组和ArrayBuffer](#8.5)
### [8.6 Blob](#8.6) 
### [8.7 文件系统API](#8.7)      
### [8.8 客户端数据库](#8.8)
### [8.9 Web套接字](#8.9)
## [附件](#10)
### [1、遍历样式表结果](#10.1)
### [2、HTTP状态码列表](#10.2) 
### [3、permanote.js](#10.3)   
------ 		
        

<h2 id='1'> 一、种子模块</h2>
<h3 id='1.1'>1.1 模块化</h3>  

#### 1) 规范 
> - AMD规范 
>> - Asynchronous Moduel Definition 异步模块加载机制
>> - 很短，也很简单，完整描述模块的定义，依赖关系，引用关系以及加载机制
> - CommonJS规范  
>> - JS在服务器端的规范
>> - 该方法读取一个文件并执行，最后返回文件内部的export对象
>> - 打包工具比较成熟
> - ES6 moduel规范 
>> - 暂时还没有浏览器支持
#### 2) 功能介绍 
> - 拓展性
> - 高可用 
> - 稳定性
    
<h3 id='1.2'>1.2 对象拓展</h3>  
        
#### 1) 定义
> - 对一个对象的属性进行随意的添加，更改和删除
> - 叫做extend或者mixin
        
                function extend(denstination, source) {
                    var property;
                    for(property in source) {
                        denstination[property] = source[property];
                    }
                    return denstination;
                }
#### 2) Object.keys() 
> - 方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和使用 for...in 循环遍历该对象时返回的顺序一致 （两者的主要区别是 一个 for-in 循环还会枚举其原型链上的属性）。 
> - 在ES5里，如果此方法的参数不是对象（而是一个原始值），那么它会抛出 TypeError。在ES2015中，非对象的参数将被强制转换为一个对象。
> - 例子出自[MDN Web doc](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
                
                // simple array
                var arr = ['a', 'b', 'c'];
                console.log(Object.keys(arr)); // console: ['0', '1', '2']

                // array like object
                var obj = { 0: 'a', 1: 'b', 2: 'c' };
                console.log(Object.keys(obj)); // console: ['0', '1', '2']

                // array like object with random key ordering
                var anObj = { 100: 'a', 2: 'b', 7: 'c' };
                console.log(Object.keys(anObj)); // console: ['2', '7', '100']
> - 本质：
        
                Object.keys = Object.keys || function(obj) {

                    var a[];

                    // a[0] = name1; a = {name1}; a.length=1;
                    // a[1] = name2; a = {name2}; a.length=2;
                    // ......
                    for(a[a.length] in obj);
                    return a;
                }

        
<h3 id='1.3'>1.3 数组化</h3>  
        
#### 1) 类数组对象
> - HTMLCollection, NodeList等
> - 功能太弱
> - 通常来讲，使用Array.Prototype.slice.call()就能转换类数组对象
> - 但是，由于HTMLCollection, NodeList等在旧的IE版本中并不是Object的子类，所以会出现异常
#### 2) jQuery的makeArray 
> - 代码：
        
                var makeArray = function(array) {
                    var ret = [];
                    if(array != null)  {
                        var i = array.length;

                        // 对待非数组对象
                        if(i == null || typeof array === "string" || \
                        jQuery.isFunction(array)) || array.setInterval)
                            ret[0] = array;

                        // 对待数组对象
                        else
                            while(i)
                                ret[--i] = array[i]; // i由于代表长度，先减1 
                    }
                    return ret;
                }


        
<h3 id='1.4'>1.4 类型的判断</h3>  
        
#### 1) 两套类型系统
> - 基本数据类型：undefined，string，null, boolean, function和number，基本数据类型都是可以通过typeof来检测的
> - 对象类型系统 通过instanceof来检测
> - 但是JS原生的这两套识别机制都不靠谱，通过typeof只能检测undefined，string, boolean, function，number和object这6种数据类型。 不能检测Null,RegExp,Argument等细分对象类型用
> - !!一般用来将后面的表达式转换为布尔型的数据（boolean）
#### 2) 陷阱
> - 数组的跨域检测，原因：无法跨帧检测
        
                var iframe = document.createElement("iframe");
                document.body.appendChild(iframe);
                var xArray = window.frames[window.frames.length-1].Array;
                var arr = new xArray(1,2,3); // [1, 2, 3]
                arr instanceof Array; //false
                arr.constructor === Array; //false
> - isNaN非常的不靠谱
        
                isNaN(0/0)  // =>true；
                isNaN(undefined)     // =>true；
                isNaN("nihao");     // =>true；
> - 序列化的时候也不能分辨NaN，null
        
                JSON.stringify(0/0);    // =>'null'；
                JSON.stringify(null);    // =>'null'；
                JSON.stringify(undefined);  // =>undefined;
> - safari的typeof坑
        
                typeof document.childNodes;     // =>fcunction；
> - 在旧版本的IE下，DOM和BOM对象的construction属性没有暴露出来，所以是undefined
        
                typeof document.constructor     // =>undefined;
#### 3) 最佳实践
> - 通过typeof检测undefined，string, boolean, function，number和object这6种数据类型。如jQuery
        
                var isFunction = function isFunction( obj ) {

                // Support: Chrome <=57, Firefox <=52
                // In some browsers, typeof returns "function" for HTML <object> elements
                // (i.e., `typeof document.createElement( "object" ) === "function"`).
                // We don't want to classify *any* DOM node as a function.
                return typeof obj === "function" && typeof obj.nodeType !== "number";
  };
> - NaN
        
                function isNaN(obj) {
                    return obj !==obj;
                }
> - undefined
        
                function isUndefined(obj) {

                    //或者直接与undefined比较
                    return obj === void 0;
                };
> - null
        
                function isNull(obj) {
                    return obj === null;
                }
> - Array
        
                function isArray(obj) {

                    return Object.prototype.toString.call(obj) === "[object Array]"
                }
> - type jQuery版本，主要用toString的方法
        
                var class2type = [];
                // Populate the class2type map
                jQuery.each( "Boolean Number String Function Array Date RegExp Object Error Symbol".split( " " ),
                function( i, name ) {
                    class2type[ "[object " + name + "]" ] = name.toLowerCase();
                } );

                function toType( obj ) {
                    if ( obj == null ) {
                        return obj + "";
                    }

                    // Support: Android <=2.3 only (functionish RegExp)
                    return typeof obj === "object" || typeof obj === "function" ?
                        class2type[ toString.call( obj ) ] || "object" :
                        typeof obj;
                }
                /* global Symbol */
                // Defining this global in .eslintrc.json would create a danger of using the global
                // unguarded in another place, it seems safer to define global only for this module

                var bool = true;
                var num = 1;
                var str = "hello";
                var func = function(){};
                var arr = new Array(1,2,3);
                var date = new Date();
                var reg = /^a/;
                var error = new Error();

                console.log("类型判别：Boolean = " + toType(bool));
                console.log("类型判别：Number = " + toType(num));
                console.log("类型判别：String = " + toType(str));
                console.log("类型判别：Function = " + toType(func));
                console.log("类型判别：Array = " + toType(arr));
                console.log("类型判别：Date = " + toType(date));
                console.log("类型判别：RegExp = " + toType(reg));
                console.log("类型判别：Error = " + toType(error));

                //结果
                类型判别：Boolean = boolean
                类型判别：Number = number
                类型判别：String = string
                类型判别：Function = function
                类型判别：Array = array
                类型判别：Date = date
                类型判别：RegExp = regexp
                类型判别：Error = error
> - window
>> - jQuery  使用window.window，但是会有缺陷，可以通过伪造骗过jQuery
        
                var isWindow = function(obj) {
                    return obj != null && obj === obj.window;
                }

                // 通过伪造骗过jQuery
                var fakeWindow = {};
                fakeWindow.window = fakeWindow;
                isWindow(fakeWindow); // =>true;
>> - avalon 
        
                //IE6~8 使用window == window.document 为true，window.document == window 为false的特性
                var isWindow = function(obj) {
                    return obj == obj.document && obj.document != obj;
                }

                //标准浏览器和IE9，IE10使用正则检测
                var isWindow = function(obj) {
                    rwindow = /^\[object (?:Window|DOMWindow|global)\]$/
                    return rwindow.test(toString.call(obj));
                };
> - isEmptyObject  是否li'miisEmptyObject
                        : function( obj ) {


                    /* eslint-disable no-unused-vars */
                    // See https://github.com/eslint/eslint/issues/6125
                    var name;

                    for ( name in obj ) {
                        return false;
                    }
                    return true;
                }
> - isNumeric 判断是否是数字或者可以转化w，但是有的数字是通过new Number()的方法建立的，他是一个对象类型，但我们也认为他是一个数字，此时如果采用typeof的方法去判断的话，就会把它过滤掉了。所以为了把它保留，需要就加上!isNaN( obj - parseFloat( obj ) )，另外，数组的话也会被保留，所以需要在前面把数组给过滤掉。
        
                jQuery.isNumeric = function( obj ) {

                    // As of jQuery 3.0, isNumeric is limited to
                    // strings an
                    d numbers (primitives or objects)
                    // that can be coerced to finite numbers (gh-2662)
                    var type = jQuery.type( obj );
                    // type() 允许数字基本量或者数字包装类
                    return ( type === "number" || type === "string" ) &&

                        // parseFloat NaNs numeric-cast false positives ("")
                        // ...but misinterprets leading-number strings, particularly hex literals ("0x...")
                        // subtraction forces infinities to NaN
                        !isNaN( obj - parseFloat( obj ) );
                };

    JavaScript parseFloat() 函数
    parseFloat() 函数可解析一个字符串，并返回一个浮点数。该函数指定字符串中的首个字符是否是数字。如果是，则对字符串进行解析，直到到达数字的末端为止，然后以数字返回该数字，而不是作为字符串
    注意： 字符串中只返回第一个数字。
    注意： 开头和结尾的空格是允许的。
    注意： 如果字符串的第一个字符不能被转换为数字，那么 parseFloat() 会返回 NaN。
    如：
                console.log(parseFloat("10"));
                console.log(parseFloat("10.33"));
                console.log(parseFloat("34 45 66"));
                console.log(parseFloat(" 60 "));
                console.log(parseFloat("40 years"));
                console.log(parseFloat("He was 40"));
                console.log(parseFloat([1,2,3]));
    结果：
                10:55:52.945 VM342:1 10
                10:55:52.946 VM342:2 10.33
                10:55:52.946 VM342:3 34
                10:55:52.946 VM342:4 60
                10:55:52.946 VM342:5 40
                10:55:52.946 VM342:6 NaN
                10:57:17.574 VM348:7 
                10:57:17.574 VM348:7 1
> - isArrayLike 判断是否是类数组，这个判断主要看在不是函数或者window对象的前提下，拥有一个大于或者等于零的整形length属性
        
                function isArrayLike( obj ) {
                    // Support: real iOS 8.2 only (not reproducible in simulator)
                    // `in` check used to prevent JIT error (gh-2145)
                    // hasOwn isn't used here due to false negatives
                    // regarding Nodelist length in IE
                    var length = !!obj && "length" in obj && obj.length,
                        type = toType( obj );

                    if ( isFunction( obj ) || isWindow( obj ) ) {
                        return false;
                    }

                    //当length属性值大于零的时候判断其对应的key是否存在
                    return type === "array" || length === 0 ||
                        typeof length === "number" && length > 0 && ( length - 1 ) in obj;
                }

                function toType( obj ) {
                    if ( obj == null ) {
                        return obj + "";
                    }

                    // Support: Android <=2.3 only (functionish RegExp)
                    return typeof obj === "object" || typeof obj === "function" ?
                        class2type[ toString.call( obj ) ] || "object" :
                        typeof obj;
                }
                /* global Symbol */
                // Defining this global in .eslintrc.json would create a danger of using the global
                // unguarded in another place, it seems safer to define global only for this module

        
<h3 id='1.5'>1.5 无冲突处理</h3>  
        
#### 1) jQuery的noConflict
> - 一开始如果有别的库，后来再引入jQuery的时候，首先_jQuery的值就是undefined，_$=window.$就是别的库，接着window.jQuery = window.$ = jQuery; window.$就变成jQuery的库了，此时执行jQuery.noConflict方法，window.$ = _$就变成别人的库，如果deep为真，那么连window.jQuery都会变成undefined;
        
                var

                    // Map over jQuery in case of overwrite
                    _jQuery = window.jQuery,

                    // Map over the $ in case of overwrite
                    _$ = window.$;

                jQuery.noConflict = function( deep ) {
                    if ( window.$ === jQuery ) {
                        window.$ = _$;
                    }

                    if ( deep && window.jQuery === jQuery ) {
                        window.jQuery = _jQuery;
                    }

                    return jQuery;
                };

                // Expose jQuery and $ identifiers, even in AMD
                // (#7102#comment:10, https://github.com/jquery/jquery/pull/557)
                // and CommonJS for browser emulators (#13566)
                if ( !noGlobal ) {
                    window.jQuery = window.$ = jQuery;
                }
> - 