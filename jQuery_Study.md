# jQuery_Study  
  
  
### 作者：冰红茶  
### 参考书籍：《锋利的jQuery》第二版  
        
------

   刚看完了乌龟书，准备看司徒老师的JavaScript设计框架的时候，发现还是需要恶补一下jQuery和Ajax方面的知识，于是就准备进入《锋利的jQuery》的学习吧^_ ^
  
## 目录

## [一、Web浏览器的JavaStript](#1)
### [1.1 jQuery对象和DOM对象](#1.1)
### [1.2 jQuery选择器的优势](#1.2) 
## [二、事件处理](#2)
### [2.1 简介](#2.1)
### [2.2 事件类型](#2.2) 
### [2.3 注册事件处理程序](#2.3)
### [2.4 循环绑定事件](#2.4)
### [2.5 事件处理程序的调用](#2.5)
### [2.6 文档加载事件](#2.6)
## [三、脚本化文档](#3)
### [3.1 DOM概览](#3.1)
### [3.2 选取文档元素](#3.2)
### [3.3 文档结构和遍历](#3.3)
### [3.4 属性](#3.4)
### [3.5 元素的内容](#3.5)
### [3.6 元素操纵方法](#3.6)       
        
------      
            

<h2 id='1'> 一、认识JavaScript </h2>
<h3 id='1.1'>1.1 jQuery对象和DOM对象</h3>  

#### 1) DOM对象的获取
              
                var seemore=document.getElementById('seemore');     
        
#### 2) jQuery对象的获取      
                var  var $myfocusicon = $("#myfocusicon");            
#### 3) jQuery对象和DOM对象的互相转化
    
                var $myfocus = $("#myfocus");
                var myfocus = $myfocus[0];  //jQuery对象是一个类数组的对象   
        
<h3 id='1.2'>1.2 解决jQuery和其他库的冲突</h3>       

#### 1) jQuery.noConflict()函数       

> - 这个函数用来废除已有的快捷定义，如不再用$代表jQuery。
        
                jQuery.noConflict();    //这样你就可以把$快捷键的控制权交给别的库

> - 或者你可以使用该函数自定义一个新的快捷方式       
        
                var $j = jQuery.noConflict();
    
<h3 id='1.2'>1.2 jQuery选择器的优势</h3>  

#### 1)         
                  

