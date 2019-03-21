# HowTomcatWorks
Servlet容器是如何工作的  
-------  
servlet容器是一个复杂的系统。不过，一个servlet容器要为一个servlet的请求提供服务，基本上有三件事要做:  
>创建一个request对象并填充那些有可能被所引用的servlet使用的信息，如参数、头部、cookies、查询字符串、URI等等。  
>一个request对象是javax.servlet.ServletRequest或javax.servlet.http.ServletRequest接口的一个实例。  
>创建一个response对象，所引用的servlet使用它来给客户端发送响应。
>一个response对象javax.servlet.ServletResponse或javax.servlet.http.ServletResponse接口的一个实例。  
>调用servlet的service方法，并传入request和response对象。在这里servlet会从request对象取值，给response写值。  
   
Catalina架构  
-------  
Catalina是一个非常复杂的，并优雅的设计开发出来的软件，同时它也是模块化的。   
基于“Servlet容器是如何工作的”这一节中提到的任务，你可以把Catalina看成是由两个主要模块所组成的：连接器(connector)和容器(container)。

连接器是用来“连接”容器里边的请求的。它的工作是为接收到每一个HTTP请求构造一个request和response对象。然后它把流程传递给容器。    
容器从连接器接收到requset和response对象之后调用servlet的service方法用于响应。   
谨记，这个描述仅仅是冰山一角而已。这里容器做了相当多事情。   
例如，在它调用servlet的service方法之前，它必须加载这个servlet，验证用户(假如需要的话)，更新用户会话等等。一个容器为了处理这个进程使用了很多不同的模块，这也并不奇怪。例如，管理模块是用来处理用户会话，而加载器是用来加载servlet类等等。  
