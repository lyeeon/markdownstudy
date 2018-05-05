# JMeter中文使用手册
 
 ## 1.简介
　　Apache JMeter是100%纯java桌面应用程序，被设计用来测试C/S结构的软件（例如web应用程序）。它可以被用来测试包括基于静态和动态资源程序的性能，例如静态  文件，JavaServlets，Java 对象，数据库，FTP 服务器等等。JMeter可以用来模拟一个在服务器、网络或者对象上大的负载来测试或分析在不同的负载类型下全面性能.

　　另外，JMeter能够通过让你们用断言创造测试脚本来验证我们的应用程序是否返回了我们期望的结果，从而帮助我们回归测试我们的程序。为了最大的灵活性，JMeter允许我们使用正则表达式创建断言。

### 1.1 历史
　　Apache软件组织的Stefano Mazzocchi是JMeter的创始人。他写出它起初是为了测试Apache JServ的性能（一个已经被Apache Tomcat工程所替代的工程）。我们重新设计JMeter来增强用户界面和增加功能测试的能力。

### 1.2 未来
　　我们希望看到作为开发者利用它的可插入架构使JMeter的功能快速扩展。未来发展的主要目标是在没有危机JMeter的负载测试能力的情况下尽可能使JMeter成为最实用的回归测试工具。
 
 ## 2 入门
　　开始使用JMeter最容易的方法是首先下载最新版并且安装它。这个版本包含所有你在构建和运行Web，FTP，JDBC，和JNDI测试时使用的所有文件。如果你想执行JDBC测试，你当然需要从厂商得到适当的JDBC驱动。JMeter没有提供任何JDBC驱动。

其它你可能需要下载的软件：

·　　[BeanShell](http://www.beanshell.org/)

·　　[Java Activation Framework](http://java.sun.com/products/javabeans/glasgow/jaf.html) - JavaMail需要

·　　[Java Mail - mail](http://java.sun.com/products/javamail/index.jsp) 显示 and SOAP 测试需要

·　　[JMS](http://java.sun.com/products/jms/docs.html) - JMS 取样器

·　　[General Java download page](http://java.sun.com/downloads/)

	详细参见安装的jar包中的 JMeter Classpath 一章

　　下一步, 开始使用JMeter并且参见用户手册构建测试计划一章使自己更加熟悉JMeter基础 (例如，添加和删除元素)。

　　最后, 参见如何构建一个明确类型的测试用例的适合章节。例如，如果你对Web应用测试感兴趣，那就参见构建一个Web测试计划。其他测试计划的细节是JDBC, FTP, and JNDI。

　　一旦你熟练构建和执行JMeter测试计划, 通过你的测试计划你会观察到给你更多帮助的各种元素的配置(定时器, 监听器, 断言, 和其他)。

### 2.1 需求
JMeter 需要运行环境匹配的最小需求。

#### 2.1.1 Java 版本
　　JMeter 需要一个完整适当的JVM 1.3或更高的版本. 我们现在尽力与JVM 1.3保持兼容,然而JMeter在1.4或者更高运行的会最好。因为JMeter 仅使用Java标准API,请不要把因为JRE实现版本而无法运行JMeter的bug报告提交。
　　Java 1.3 不包括 SSL (HTTPS) 支持 - 你将需要下载 JSSE. 同样, 它不会像其他更高版本的Java那样好的运行。为了更好的结果使用Java1.4或者1.5。

#### 2.1.2 操作系统
　　JMeter是100%纯Java应用程序并且能够正确的在任何有适当的Java实现的操作系统上运行。JMeter 在下列环境已经被测试:

·　　Unix (Solaris, Linux, 等)

·　　Windows (98, NT, 2000, xp)

·　　OpenVMS Alpha 7.3+

### 2.2 可选
如果你计划做JMeter开发或者想使用SUN的java标准扩展包，你将需要下列更多的可选包。

#### 2.2.1 Java 编译器
如果你想编译JMeter源代码或者开发JMeter插件，你将需要一个完整的适当的JDK1.3或者更高。

#### 2.2.2 SAX XML解析器
　　JMeter 使用 Apache's Xerces XML 解析器你可以选择告诉JMeter使用一个不同的XML 解析器。 这样做，把第三方的解析器的类包包含在JMeter的classpath 中， 并更新 jmeter.properties 文件里的解析器实现的全类名。

#### 2.2.3 Email 支持
　　JMeter 有有限的 Email 能力。 它能够发送给你测试结果的email，并且支持POP/IMAP 取样器。它现在不支持 SMTP 取样。 为了能够支持 Email, 需要添加Sun 的JavaMail包和activation包到JMeter classpath 。

#### 2.2.4 SSL 加密
　　为了测试一个使用SSL加密（HPPS）的web服务器， JMeter 需要一个提供SSL实现(例如 Sun的 Java Secure SocketsExtension - JSSE）。包含需要的加密包到JMeter的 classpath 。 同样,通过注册SSL提供者更新 jmeter.properties 。为了更好的管理证书，也要有一个SSL 管理器 。
##### 注意  
如果你在JDK1.4上运行，你将不需要下载JSSE，因为SUN已经集成它到JDK1.4中做为标准类库了。JMeter 代理服务器(见下)不支持记录SSL(https)。

#### 2.2.5 JDBC 驱动
你需要添加你的厂商的JDBC驱动到classpath，如果你需要JDBC测试.确认文件是一个jar文件，而不是zip。

#### 2.2.6 Apache SOAP
　　ApacheSOAP 需要 mail.jar 和 activation.jar. 你需要下载并拷贝两个jar文件到你jmeter/lib 目录.一旦文件放到那里，JMeter 会自动找到它们。
详细参见安装的jar包中的 JMeter Classpath 一章

### 2.3 安装
快速安装JMeter。细节依赖你下载的发布文件。
##### 注意  
避免在一个有空格的路径安装 JMeter。这将导致远程测试出现问题。

#### 2.3.1 下载最新版本
　　我们推荐大多数用户运行最新版本。要安装一个构建版本，简单解压zip/tar文件到你想安装JMeter的目录。保证一个JRE/JDK正确的安装并且设置环境变量JAVA_HOME，其它不需要做什么了。

#### 2.3.2 下载夜晚构建
　　如果你不介意使用beta版软件，你可以下载运行最新夜晚构建。要安装一个夜晚构建，解压_bin和_lib zip/tar文件到相同的目录结构。保证一个JRE/JDK正确的安装并且设置环境变量JAVA_HOME， JMeter 就可以正确的运行了。

### 2.4 运行 JMeter
　　要运行JMeter, 运行 jmeter.bat (for Windows) 或者 jmeter (for Unix) 文件。 JMeter 必须从 JMeter 的bin 目录 (那些文件没有发现的地方)启动。如果jmeter.bat文件能够的话，它试图改变到一个适当的目录。

#### 2.4.1 JMeterClasspath
　　JMeter 自动从在它的/lib 和 /lib/ext目录中的jar包发现类。如果你开发新的 JMeter 组件，你可以压缩它们成jar包并拷贝到 JMeter 的 /lib/ext 目录。　　JMeter 将会自导发现在这里的任何jar包的JMeter 组件。如果你不想把扩展jar包放到lib/ext 目录，可以在jmeter.properties中定义search_paths属性。不要使用lib/ext 给那些有用的jar包；它仅仅是存放 JMeter 组件。其他jar包 (例如 JDBC, 和任何JMeter代码需要支持的类库)应该被代替放在lib目录。
##### 注意：  
　　JMeter 会发现.jar文件，而不是.zip文件。你可以在$JAVA_HOME/jre/lib/ext安装有用的jar文件，或者(自从 2.1.1版本)你可以在jmeter.properties中设置user.classpath属性。注意设置CLASSPATH 环境变量将不起作用。这是因为JMeter使用"java --jar"启动，并且java命令无记录忽略CLASSPATH 变量，并且当使用-jar选项时-classpath/-cp 选项也被使用。所有的java程序都是这样，不仅仅是JMeter。
  
#### 2.4.2 使用代理服务器
　　如果你在防火墙/代理服务器后测试，你需要提供给JMeter防火墙/代理服务器的主机名和端口号。这样做，从命令行使用以下参数运行jmeter.bat -parameter: 

　　　-H *代理服务器主机名或者ip地址*

　　　-P *代理服务器端口*

　　　-N *非代理主机* (例如：*.apache.org|localhost)

　　　-u *代理证书用户名- 如果需要*

　　　-a *代理证书密码 - 如果需要*


　　例如: <strong>jmeter -H my.proxy.server -P 8000 -u username -a password -Nlocalhost</strong>

　　或者使用 --proxyHost, --proxyPort, --username,and --password

JMeter也有内建的HTTP代理服务器记录HTTP（不是 HTTPS)浏览器会话。这和上面的代理设置描述是不混淆的，它是在JMeter发出HTTP或者HTTPS请求时使用的。

#### 2.4.3 非用户界面模式 (命令行模式)

为了不相互影响测试, 你可以选择运行没有用户界面的JMeter。这样做，使用下列命令选项：

-n 这是指定JMeter在非用户界面模式运行

-t [包含测试计划的JMX文件的名字]

-l [记录取样结果的JTL文件的名字]

-r 运行在jmeter.properties文件里所有的远程服务器 (或者通过在命令行覆盖属性指定远程服务器)

这个脚本也允许我们指定可选的防火墙/代理服务器信息：

-H [代理服务器主机名或者ip地址]

-P [代理服务器端口]

例如 : jmeter -n -t my_test.jmx -l log.jtl -H my.proxy.server -P 8000
#### 2.4.4 服务器模式

为了分布测试 ，在服务器模式运行JMeter，并且通过用户界面控制每一台服务器。

	

jmeter-server/jmeter-server.bat 脚本使用适当的classpath为你开始远程注册。如果失败，参见关于JMeter服务器启动细节。

运行jmeter-server/jmeter-server.bat，加上下列选项命令：

这个脚本也允许我们指定可选的防火墙/代理服务器信息：

-H [代理服务器主机名或者ip地址]

-P [代理服务器端口]

例如 : jmeter-server -H my.proxy.server -P 8000
#### 2.4.5 通过命令行覆盖属性

Java系统属性，JMeter属性，和日志属性可以通过命令行直接覆盖(代替更改jmeter.properties文件)。这样做，使用下列选项：

-D[prop_name]=[value]- 定义一个java系统属性值。

-J[propname]=[value] - 覆盖一个JMeter属性。

-L[category]=[priority]- 覆盖一个日志设置，设置一个特殊目录为给定的优先级。

-L 标志也可以使用没有目录名来设置根目录日志等级。

例如 :

jmeter-Duser.dir=/home/mstover/jmeter_stuff \

-Jremote_hosts=127.0.0.1-Ljmeter.engine=DEBUG

jmeter-LDEBUG

	

注意
命令行参数在启动时较早被处理，但是在日志系统被设置以后。尝试使用-J标志更新log_level或者log_file属性无效。

#### 2.4.6日志和错误信息

　　如果JMeter发现一个错误, 一个消息将被写入日志文件。日志文件名在jmeter.properties文件中定义。一般定义为 jmeter.log 。并且在JMeter启动目录，例如bin。当在Windows下运行时,如果你不设置Windows显示文件扩展名，文件名会仅显示为 JMeter。你可以做一些事都很容易地发现伪装成文本文件的病毒和垃圾文件还有记录错误，jmeter.log 文件记录一些测试运行信息。例如：
 
　10/17/200312:19:20 PM INFO - jmeter.JMeter: Version 1.9.20031002  
 
　10/17/2003 12:19:45 PM INFO - jmeter.gui.action.Load: Loading file:c:\mytestfiles\BSH.jmx  
 
　10/17/2003 12:19:52 PM INFO - jmeter.engine.StandardJMeterEngine: Running thetest!  
 
　10/17/2003 12:19:52 PM INFO - jmeter.engine.StandardJMeterEngine: Starting 1threads for group BSH. Ramp up = 1.  
 
  10/17/2003 12:19:52 PM INFO - jmeter.engine.StandardJMeterEngine: Continue onerror  
 
　10/17/2003 12:19:52 PM INFO - jmeter.threads.JMeterThread: Thread BSH1-1started  
 
　10/17/2003 12:19:52 PM INFO - jmeter.threads.JMeterThread: Thread BSH1-1 isdone  
 
　10/17/2003 12:19:52 PM INFO - jmeter.engine.StandardJMeterEngine: Test hasended  
 

　　日志文件对发现错误原因很有帮助，作为JMeter不会打断一个测试来显示一个错误对话框。
#### 2.4.7 命令行选项目录

调用JMeter的 "jmeter -?"命令将打印所有命令选项的一个列表。列表如下：

-h,--help 打印使用信息并退出

-v,--version 打印版本信息并推出

-p,--propfile {argument} 使用的JMeter属性文件

-q,--addprop {argument} 附加的属性文件

-t,--testfile {argument} 运行的JMeter测试文件(.jmx)

-l,--logfile {argument} 日志取样文件

-n,--nongui 非用户界面运行JMeter

-s,--server 运行JMeter服务器

-H,--proxyHost {argument} 设置JMeter使用的代理服务器

-P,--proxyPort {argument} 设置JMeter使用的代理服务器端口

-u,--username {argument} 设置JMeter使用的代理服务器用户名

-a,--password {argument} 设置JMeter使用的代理服务器密码

-J,--jmeterproperty {argument}={value} 定义附加的 JMeter 属性

-D,--systemproperty {argument}={value} 定义附加的 System 属性

-S,--systemPropertyFile {filename} 一个属性文件被做为系统属性添加

-L,--loglevel {argument}={value} 定义日志等级: [category=]level

例如 jorphan=INFO or jmeter.util=DEBUG

-r,--runremote从非用户界面模式启动远程服务器

-d,--homedir {argument} 使用的JMeter目录
### 2.5 配置 JMeter

如果你希望改变JMeter运行时的属性你需要改变在/bin目录的jmeter.properties文件，或者创建你自己的jmeter.properties文件并且在命令行指定它。

	

注意
自从 2.1.2,你能够通过JMeter属性user.properties在文件中定义附加的JMeter属性，user.properties默认值是user.properties。如果在当前目录被发现，这个文件被自动加载。类似的，system.properties 被用来更新系统属性。


参数

属性
	

描述
	

需要

ssl.provider
	

你可以为你的SSL实现指定类。如果你想使用来自sun的JSSE，是这样：
	

No

com.sun.net.ssl.internal.ssl.Provider。
	

JMeter默认提供https支持是在你使用 JDK1.4或者你使用把JSSE类的jar包放到JMeter classpath中的JDK1.3时候。
	

No

xml.parser
	

你可以指明一个你的XML解析器实现。 默认值是：org.apache.xerces.parsers.SAXParser
	

No

remote_hosts
	

逗号分割远程JMeter主机列表。如果你在一个分布式环境运行JMeter，列出你用JMeter远程主机运行的机器。这允许你使用机器的用户界面控制那些服务器。
	

No

not_in_menu
	

在JMeter选项屏中你不想看到的组件列表。 如果JMeter被添加越来越多的组件，你会希望定制JMeter只出现那些你感兴趣的组件。你可以在这儿列出那些类名和他们的类标签(JMeter的用户界面出现的字符串), 它们将在选项屏中不出现。
	

No

search_paths
	

列出那些JMeter搜索JMeter附加类的路径(以;分割)；例如增加的取样器。被添加到lib/ext目录的任何jar包都被发现。
	

No

user.classpath
	

JMeter搜索的有用类库的路径列表。被添加到lib目录的任何jar包都被发现。
	

No

user.properties
	

附加的JMeter属性文件名。 初始化属性文件后它们被添加，但是在-q和-J选项被处理之前。
	

No

system.properties
	

附加的系统属性文件名。 -S和-D选项被执行前被添加。
	

No

又见 jmeter.properties 文件注释，在你改变其它设置时会给你更多的信息。

3. 创建一个测试计划

一个测试计划描述了一系列Jmeter运行时要执行的步骤。一个完整的测试计划包含一个或者多个线程组，逻辑控制，取样发生控制，监听器，定时器，断言和配置元件。

3.1 添加和删除元件

在一个树上通过右击可以添加 元件到一个测试计划 ，并且从"list"列表中选择一个新元件。或者，元件从文件加载并且通过选择"open"选项添加。

为了删除元件，确保元件被选中，正确在元件上右击，并且选择"remove"选项。

3.2 加载和保存元件

为了从文件加载元件，右击将要加载元件到的已经存在的树元件，并选择"open"选项。选择你的元件保存的文件。JMeter会加载元件到树中。

为了保存树元件，在一个元件上右击，选择"save"选项。JMeter会保存已选的元件，加上所有下面的子元件。用这种方法，你能够保存测试树段，单独元件，或者这个测试计划。

3.3 配置树元件

在测试树中的任何元件控制在JMeter的右手结构。那些控制允许你配置测试元件的细节行为，什么被配置为一个依赖元件类型的元件。

	

可以通过拖拉测试树周围的元件操作测试树。

3.4 运行一个测试计划

为了运行一个测试计划，从"run"菜单项选择"start"。为了停止你的测试计划，从同样的菜单选择"stop"。JMeter 不会自动给它是否正在运行任何显示。如果JMeter运行，一些监听器使它变明显，但是唯一确定的方法是检查"run"菜单。如果"start"不可用，"stop"可用，证明JMeter正在运行你的测试计划(或者，至少， 它认为它是)。

3.5 作用域规则

jmeter 测试树包含元件总是分等级和顺序的。在测试树中的一些元件是严格分级(监听器，配置元素，后置处理器，前置处理器，断言，定时器)，一些主要是顺序的(控制器，取样器)。当你创建你的测试计划时，你将创建一个描述被执行的步骤集的取样请求有序列表。那些请求常组织在也有序的控制器中。给出如下测试树：

Example test tree

请求的顺序是 One，Two，Three，Four。

一些控制器影响它的子元件的顺序，你可以在 组件参考 看到详细的控制器。

其他元素是分等级的。例如，一个断言在测试树中是分等级的。如果你的父元件是请求，它就被应用于那个请求。如果它的父元件是控制器，它就影响所有那个控制器下的所有请求。如下测试树：

Hierarchy example

Assertion #1 仅被应用于请求 One， Assertion #2 仅被应用于 请求 Two 和 Three。

其它例子，这次使用定时器：

complex example

在这个例子里，请求的命名表现它们被执行的顺序。Timer#1 应用于 请求 Two, Three, 和 Four (注意对于分等级的元件怎样的顺序是不相关的)。Assertion #1 应用于请求Three。Timer #2 对所有请求有效。

希望那些例子使你弄清了配置（分等级的）元件如何被应用。如果你想每个请求都被树分叉拒绝，到它的父元件，到它的父元件的父元件，等等，每次收集所有它的父元件的配置元件，你将看到它如何工作的。

元件Header Manager, CookieManager 和Authorization manager 的配置和默认元件的配置被视为是不同的。默认元件配置的设置并入取样器到达的值的集里。然而来自管理器的设置没有并入。如果多于一个管理器在一个取样器范围中，仅仅一个被使用，但是现在没有办法指定那个被使用。

Comments (Hide)

3.6Error reporting
3.6 錯誤報告
JMeter reports warnings and errors to the jmeter.log file, as well as someinformation on the test run itself. Just occaisionally there may be some errorsthat JMeter is unable to trap and log; these will appear on the commandconsole. If a test is not behaving as you expect, please check the log file incase any errors have been reported (e.g. perhaps a syntax error in a functioncall).
JMeter 把警告和錯誤訊息回報在jmeter.log這個檔案中，就像測試本身在執行時產生的某些資訊。只是偶爾地，JMeter對於某些錯誤是無法補捉和記錄的，這些資訊都會顯示在執行命令台上。如果一個測試的執行並不是你所期待的，那麼當錯誤發生時，請你檢查記錄檔(例如：也許在函數的調用上有語法上的錯誤)。

Sampling errors (e.g. HTTP 404 - file notfound) are not normally reported in the log file. Instead these are stored asattributes of the sample result. The status of a sample result can be seen inthe various different Listeners.
取樣錯誤(例如：HTTP 404 - 找不到檔案)是不會被正常的記錄在記錄檔中的，取而代之的，他們會被當作取樣結果的屬性來儲存，取樣結果的狀態能被許多不同的監聽器所得知。

4. 测试计划元件

测试计划对象有一个叫做"功能测试"复选框。如果被选择，它将导致JMeter记录来自服务器返回的每个取样的数据。如果你在你的测试监听器中选择一个文件，这个数据将被写入文件。你尝试一个小的运行来保证JMeter配置正确并且你的服务器正在返回期望的结果是很有用的。

4.8 后置处理器元件

一个后置控制器在一个取样器请求被建立后执行一些操作。如果一个后置处理器附属于一个取样器元件，它仅在取样器元件运行后执行。后置处理器最多用来处理响应数据，常用来从它里面摘录数值。见范围规则 关于前置处理器执行细节

4.9 执行顺序

1. 定时器 - 任何个

2. 取样器

3. 后置处理器 (如果SampleResult不为空)

4. 断言 (如果SampleResult不为空)

5. 监听器 (如果SampleResult不为空)
5. 创建一个网站测试计划

在这一部分，你将学会如何创建一个基础的测试计划来测试网站，你将会创建5个用户向Jackrta网站上的两个网页发送请求。当然，你也可以让每个用户发送两次。这样，总的HTTP发送请求为（5个用户*2次请求*重复2次）＝20。要构建这个测试计划，你将会用来下面的元素:线程组 , HTTP请求 , HTTP请求默认值和图形结果 。

要创建更好的测试计划，可以参考创建一个高级的测试计划网站。
5.1添加用户

处理每个JMeter测试计划的第一步就是添加 线程组元件。这个线程组会告诉JMeter你想要模拟的用户数量，用户应该发送请求的频率和应该发送的数量。

进一步来添加一个线程组：首先选择这个测试计划，用鼠标右键点击然后在得到的菜单中选择添加--> 线程组。

这时你应该看到这个线程组已经在测试计划下面了，如果没有看到，就点击测试计划元件展开这个测试计划树。

下一步，你需要修改这些默认的属性。如果你还没有选择线程组元件,则从测试计划树型结构中选择它。这时你应该看到JMeter窗口右边的线程组控制面板了。

图5.1.线程组默认值

首先给这个线程组起一个有意义的名字。在名称域中, 输入Jakarta Users.

下一步，增加用户的数量为5。

在下一个the Ramp-Up Period文本域中 , 使用默认值为0。这个属性表示每个用户启动的迟延时间。例如，如果你输入Ramp-Up Period 为5秒，JMeter将会在五秒结束前完成 启动所有的用户。所以，如果你有五个用户并且Ramp-Up Period为五秒，那么开始用户的延迟就是1秒。(5个用户 / 5秒 = 1 用户每秒). JMeter将会立即启动你所有的用户，如果你设置其值为0。

最后，取消标记为"永远"的复选框选择并设置循环次数为2。 这个属性表示你的测试的重复次数。如果你设置为1，JMeter将你的测试只运行一次。 要让JMeter不断的运行，你要选择"永远"这个复选框。

	

在大多数的应用程序中，你需要手动来接受你在控制面板中所做的修改。但在JMeter中，如果你做了修改，控制面板可以自动的接受。如果你修改的元件的名字，树型菜单自动更新当你离开控制面板后。 (例如, 当你选择另外一个树元件。)

图5.2 为完整的Jakarta Users线程组。

图5.2. Jakarta Users 线程组
5.2 添加默认HTTP请求属性

我们已经定义了用户，现在要定义他们的行为了。在这一部分，你将学会对你的HTTP请求设置默认值。然后在5.3节，用你在这里指定的默认设置来添加HTTP请求元件。

首先选择Jakarta Users元件，右键点击并在弹出的菜单中选择添加 -->配置元件 --> HTTP请求默认值。 然后选择这个新元件来显示其控制面板（见图5.3）。

图5.3.HTTP 请求默认值

跟大多数的JMeter元件一样， HTTP请求默认值控制面板也有一个名称域。在这个例子中将它保留为默认值。

下面这个文本域是Web Server的Server名字/IP。对于这个测试计划中，所有的HTTP请求都将发送到相同的网站服务器jakarta.apache.org。向文本域中输入名字，这是唯一的一个需要我们去修改它的默认值，其它的文本域都保留它们的默认值。

	

HTTP请求默认值元件并不告诉JMeter来发送HTTP请求，它仅仅定义这个HTTP请求所用的默认值。

图5.4表示为完整的HTTP请求默认值元件

图5.4.测试计划的HTTP 默认值
5.3 添加 Cookie 支持

除非你的应用程序明确的不使用Cookies，几乎所有的网站应用程序都会使用cookie支持。要添加cookie支持，可以简单的在你的测试计划中给每一个线程组 添加 一个 HTTPCookie 管理器 。这样确信每个线程组有自己的cookies，但是通过所有交互的 HTTP 请求 对象变成共享。

添加 HTTP Cookie 管理器 , 简单地，选择这个 线程组 ，选择添加--> HTTP Cookie管理器，也可以从编辑菜单或通过右键点击来实现添加。
5.4 添加 HTTP 请求

在这个测试计划中，我们需要实现两个HTTP请求。第一个就是 Jakarta网站首页(http://jakarta.apache.org/),第二个就是工程向导网页(http://jakarta.apache.org/site/guidelines.html)。

	

JMeter按照它们在树的出现的次序来发送请求。

首先给Jakarta Users元件添加第一个 HTTP请求 (添加 --> 取样器--> HTTP 请求)。然后从树中选择HTTP请求元件并修改正面的属性（看图5.5）：

更改名称域为"Home Page".
设置路径域为 "/"。

	

你不必要设计服务器的名称域，因为你已经在HTTP请求默认值元件中设定过了。

图5.5. Jakarta首页的HTTP请求

下一步，添加每二个HTTP请求并修改下面的属性（见图5.6）：

更改名称域为"Project Guidelines"。
设置路径域为 "/site/guidelines.html"。

图5.6. Jakarta工程Guidelines页的HTTP请求
5.5 添加一个监听器到试图储存测试结果

最后一个你需要给测试计划的元件是监听器。这个元件的用途是将所有的HTTP请求结果存储在一个文件中并显现出数据的可视模型。

选择Jakarta Users 元件，然后添加一个 图形结果 监听器 (添加 -->图形结果). 接着，你需要指定一个文件路径和输出文件名。你可以在文件名域中输入或选择浏览按钮并选择一个路径然后输入文件名。

图5.7. 图像结果监听器
5.6 保存测试计划

尽管它并不必要，我们还是建议你在运行测试计划前将它保存在一个文件里边。通过选择文件菜单中的"保存测试计划"来保存（在最新版本中你不需要先选择测试计划元件）。

	

JMeter允许你保存整个测试计划树，也可以只保存其中的一部分。要保存特别树枝中的一些元件，首先选择树枝的起始元件，然后在右键弹出的菜单中选择保存为菜单项。同样的，也可以选择合适的元件，然后选择编辑菜单中的"另存为"。
5.7 运行测试计划

从Run 菜单中选择Run。

	

如果测试运行正确，JMeter会在上方显现一个绿色的长方形区域。当所有的测试结束时，它将会变成灰色。即使在你选择了"stop"后，这个绿色的灯还将保持，直到所有的线程结束。

一旦JMeter已经完成测试计划，选择"run"菜单中的"stop"。

如果你选择了一个文件来保存你监听器中的结果，那么你将有一个文件，它可以在任何的视图中打开。每一个视图将以它自己的样子显示结果。

	

相同的文件可以在多个视图中打开，这是没有问题的。在测试运行期间，JMeter确信没有例子被多次保存在同一个文件中。
6. 创建一个高级web测试计划

在这章，你将学到如何创建高级测试计划 测试web站点。

如果需要一个基础的测试计划例子，见构建一个web测试计划 。
6.1 用URL重写处理用户会话

如果你的web应用程序使用URL重写优于cookies保存会话信息，那么为了测试你的站点你将需要做一点额外的工作。

为了响应正确到URL重写，JMeter需要解析从服务器接受的HTML和重新得到唯一的会话ID。利用适当的 HTTP URL 重写修改器 来完成这些。 简单地输入你的会话ID参数名到修改器，它会找到它并添加它到每一个请求。如果请求已经有一个值，它将会被替代。如果"Cache Session Id?"被选中，那么最后被发现的会话ID将被保存，并且如果HTTP的上次取样不包含一个会话ID将会被使用。

URL 重写例子

下载 这个例子 。 在图1 展示了一个使用URL重写的测试计划。注意URL重写修改器附属于线程组，因此确定它对在那个线程组的每一个请求有效。

图 1 - 测试树

在图2中，我们看到了URL重写修改器的GUI，它仅仅有一个让用户指定会话ID参数名的文本域。 有一个复选框来指示会话ID将被化为为路径 (以";"隔开)，这样胜过使用一个请求参数。

图 2 - 请求参数
6.2 使用消息头管理

HTTP 消息头管理 让你定制JMeter在HTTP请求消息头发送的信息。这个消息头包括像"User-Agent","Pragma", "Referer"等属性。

HTTP 消息头管理 好像 HTTP Cookie 管理 ,如果你因为一些原因你不希望在你的测试里为不同的HTTP 请求对象指定不同的消息头，可以被添加到线程组水平。

7.创建一个数据库测试计划

在这一部分，你将学会如何去创建一个基础的测试计划来测试一个数据库服务器。你会创建10个用户来给数据库服务器发送2次SQL请求。同样，你也可以让用户运行他们的测试三次。这样总的JDBC请求数量就是（10用户）*（2次请求）*（重复3次）=60。要构建这个测试计划，你将会用到下面的元件：线程组，JDBC请求，图形结果。

	

这个例子使用了MySQL数据库驱动。要使用这个驱动，它所包涵的.jar文件必须复制到../lib/directory下(详情参见JMeter's ClassPath)。另外我们期望在运行这个测试计划的时候有的堆栈跟踪数量。

7.1 添加用户

处理每个JMeter测试计划的第一步就是添加线程组元件。这个线程组会告诉JMeter你想要模拟的用户数量，用户应该发送请求的频率和应该发送的数量。下一步来添加一个线程组：首先选择这个测试计划，用鼠标右键点击然后在得到的菜单中选择添加--> 线程组。这时你应该看到这个线程组已经在测试计划下面了，如果没有看到，就点击测试计划元件展开这个测试计划树。

下一步，你需要修改这些默认的属性。如果你还没有选择线程组元件,则从测试计划树型结构中选择它。这时你应该看到JMeter窗口右边的线程组控制面板了(见图7.1)。

首先给这个线程组起一个有意义的名字。在名称域中, 输入JDBC Users

	

你将需要一个可用的数据库，数据库表，和表的用户使用权限。在这个例子中，数据库是'mydb'，表名是'Stocks'。

接下来，将用户的数量（即threads）增加不10。在下一个the Ramp-Up Period文本域中 , 使用默认值为0。这个属性表示每个用户启动的迟延时间。例如，如果你输入Ramp-Up Period 为5秒，JMeter将会在五秒结束前完成启动所有的用户。所以，如果你有五个用户并且Ramp-Up Period为五秒，那么开始用户的延迟就是1秒。(5个用户 / 5秒 = 1 用户每秒). JMeter将会立即启动你所有的用户，如果你设置其值为0。

最后，取消标记为"永远"的复选框选择并设置循环次数为2。 这个属性表示你的测试的重复次数。如果你设置为1，JMeter将你的测试只运行一次。 要让JMeter不断的运行，你要选择"永远"这个复选框。

	

在大多数的应用程序中，你需要手动来接受你在控制面板中所做的修改。但在JMeter中，如果你做了修改，控制面板可以自动的接受。如果你修改的元件的名字，树型菜单自动更新当你离开控制面板后。 (例如, 当你选择另外一个树元件。)

图 7.2 为完整的JDBC Users线程组。

7.2 添加JDBC请求

我们已经定义了用户，现在要定义他们的行为了。在这一部分，我们将会详细说明JDBC请求。

首先选择JDBC用户元件，右键点击，在弹出的菜单中选择Add --> Config Element --> JDBC Connection Configuration。然后，选择这个新的元件来显示它的控制面板（见图7.3）。

设定下面的文本域的值(我们这里假定用一个本地的MySQL数据库名为test)。

·        Variablename bound to pool. 这需要能够唯一标识这个配置。

·        DatabaseURL: jdbc: mysql://localhost:3306/test

·        JDBCDriver class: com.mysql.jdbc.Driver

·        Username:guest

·        Password:password for guest

剩下的文本域我们可以保留默认的值。

Figure 7.3. JDBC Configuration

再次选择JDBC用户元件。右键点击，并在弹出的菜单中选择Add --> Sampler --> JDBC Request。然后，选择一个新的元件来显示其控制面板（见图7.4）。

Figure 7.4. JDBC Request

在我们这个测试计划中，我们将发送2个JDBC请求。第一个是向Eastman Kodak stock,第二个是向Pfizer stock(很显然需要改变这些例子来适合你的特殊的数据库)。下面的插图文字说明。

	

JMeter发送请求的次序就是你向树中添加它们的次序。

首先修改下面的属性值勤(见图7.5):

·        修改名字Name为"Kodak"

·        输入Pool Name:MySQL(在配置元件里面一样)

·        输入SQL Query String(数据库查讯字符串)

Figure 7.5. JDBC Request for Eastman Kodakstock

然后，添加第二个JDBC请求并编辑正面的属性（见图7.6）：

·        修改名字Name为"Pfizer"

·        输入SQL Query 语句

Figure 7.6. JDBC Request for Pfizer stock

7.4添加一个监听器浏览/保存测试结果

你需要添加到你测试计划的最后元件是一个监听器。这个元件责任是储存所有你的JDBC请求结果到文件，并且展示一个可视数据模型。

选择JDBC Users元件，添加一个Graph Results监听器（Add --> Listener -->Graph Results）。

Figure 7.7. Graph results Listener

7.5保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从File菜单选择Save Test Plan（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"Save"。或者，选择合适测试计划元件，然后从Edit菜单选择Save。

7.6 运行测试计划

从Run菜单，选择Run。

	

如果你测试正在运行，JMeter在右手上方的角落点燃一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"stop"，绿光依然会继续停留，知道所有测试都已经停止。

7.7 JDBC设置

不同的数据库和JDBC驱动程序需要不同的JDBC设置。JDBC执行的提供者来定义数据库URL和数据库驱动程序类。

下面是一些可能的设置。要得到详细的说明请看JDBC驱动程序文档。

Datebase
	

Driver class
	

Database URL

MySQL
	

com.mysql.jdbc.Driver
	

jdbc:mysql://host:port/{dbname}

PostgreSQL
	

org.postgresql.Driver
	

jdbc:postgresql:{dbname}

Oracle
	

oracle.jdbc.driver.OracleDriver
	

jdbc:oracle:thin:user/pass@//host:port/service

Ingres (2006)
	

ingres.jdbc.IngresDriver
	

jdbc:ingres://host:port/db[;attr=value]

 

	

上面的可能不正确，请查看相应的JDBC驱动程序文档。
8创建一个FTP测试计划

在这章，你将学习到如何创建一个基本的测试计划来测试FTP站点。你将为在O'Reilly的FTP站点上的两个文件创建四个发送请求的用户。同样，你将告诉用户运行测试两次。所以整个测试数目是（4个用户）*（2个请求）*（重复2次）=16个FTP请求。为了构造测试计划，你将需要使用下列元件：测试线程，FTP请求，FTP默认请求和Spline Visualizer。

	

这个例子使用O'Reilly的FTP站点，www.oro.com。当运行这个例子时请考虑周到，并且（如果可能）考虑再次运行其他FTP站点。
8.1添加用户

你想处理每个JMeter测试计划的第一步是添加线程组元件。线程组告诉JMeter你想模拟的用户数，用户发送请求的频率，和发送请求的数量。

顺便说一下，首先选择测试计划，右键点击得到Add菜单，并且选择Add->ThreadGroup，通过这种方式添加线程组。

现在你应该看到了测试计划下的线程组元件了。如果你看不到这个元件，单击测试计划元件展开测试计划树。

下一步，你需要修改默认配置。如果你还没有选择线程组元件，在树里选择它。现在在JMeter窗口右部你应该可以看到线程组控制面板。

（见下图8.1）

图8.1使用默认值的线程组

首先给线程组起一个更加有意义的名字。在name文本域，输入O'Reilly Users。

先一步，增加用户数（调用线程）到四个。

在下一个文本域——Ramp-UP Period，使用默认值0秒。这个属性告诉JMeter启动每个用户之间的时间间隔。例如，你输入Ramp-Up Period 为五秒，JMeter将会在最后5秒结束前启动所有你的用户。所以，如果我们有5个用户和一个5秒的Ramp-UpPeriod，那么启动用户的延迟就是1秒(5用户/5秒=1用户每秒）。如果你设置为那个值为零，那么JMeter将会立刻启动所以你的用户。

最后，清除标为"Forever"的复选框，并且在循环次数文本域中输入2。这个属性告诉JMeter重复你的测试的次数。如果你输入循环次数为0，那么JMeter将会运行你的测试一次。为了让JMeter重复运行你的测试计划，选择Forever复选框。

	

在大部分应用程序中，你必须在控制面板中手工改变。然而，在JMeter中，控制面板中自动接受你做的改变。如果你修改元件名，这个树会在你离开控制面板前自动使用新的文本更新这个树（例如，当你选择另一个树元件时）。

见图8.2 完整的O'Reilly Users线程组。

图8.2O'Reilly Users线程组
8.2添加默认FTP请求配置

既然我们已经定义了我们的用户，是时间定义他们要执行的任务了。在这一节，你将为你的FTP请求指定默认设置。然后在8.3节，你将会添加使用你在这里指定的一些默认设置的FTP请求元件。

首先选择O'Reilly Users元件。右键点击得到Add菜单，然后选择Add --> Config Element --> FTP Request Defaults。于是选择新的元件预览它的控制面板（见图8.3）。

图8.3FTP默认请求

像大多数JMeter元件一样，FTP默认请求控制面板有一个你可以修改的name文本域。在这个例子里，保持这个文本域使用默认值。

忽略下一个文本域，它是FTP服务器的服务器名/IP。为了你正在构建的测试计划，所有的FTP请求将会发送到相同的FTP服务器，ftp.oro.com。输入这个域名到这个文本域。这是我们定制一个默认的唯一文本域，所以保持剩余的文本域使用它们的默认值。

	

FTP默认请求元件没有告诉JMeter发送一个FTP请求。它只是简单定义了FTP请求元件使用的默认值。

见图8.4 完整的FTP默认请求元件。

图8.4我们测试计划的FTP默认
8.3添加FTP请求

在我们的测试计划中，我们需要制作两个FTP请求。第一个是O'Reilly下的mSQL下的java下README文件（ftp://ftp.oro.com/pub/msql/java/README），第一个文件是tutorial文件（ftp://ftp.oro.com/pub/msql/java/tutorial.txt）。

	

JMeter按照它们在树中出现的顺序发送请求。

首先添加第一个FTP请求到O'Reilly Users元件（Add --> Sampler --> FTP Request）。然后早树中选择FTP请求元件，并且编辑下列属性（见图8.5）：

1. 修改Name文本域为"README"。

2. 修改File to Retrieve From Server文本域为"pub/msql/java/README"。

3. 修改Username文本域为"anonymous"。

4. 修改Password文本域为"anonymous"。

	

因为你已经在FTP默认请求元件中指定了服务器名，所以你不需要设置这个值了。

图8.5O'Reilly mSQL java README文件的FTP请求

下一步，添加第二个FTP请求，并修改下列属性（见图8.6）：

1. 修改Name文本域为"tutorial"。

2. 修改File to Retrieve From Server文本域为"pub/msql/java/tutorial.txt"。

3. 修改Username文本域为"anonymous"。

4. 修改Password文本域为"anonymous"。

图8.6O'Reilly mSQL java tutorial文件的FTP请求
8.4添加一个监听器浏览/保存测试结果

你需要添加到你测试计划的最后元件是一个监听器。这个元件责任是储存所有你的FTP请求结果到文件，并且展示一个可视数据模型。

选择O'Reilly Users元件，添加一个Spline Visualizer监听器（Add --> Listener --> Spline Visualizer）。

图8.7Spline Visualizer监听器
8.5保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从File菜单选择Save Test Plan（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"Save"。或者，选择合适测试计划元件，然后从Edit菜单选择Save。
8.6运行测试计划

从Run菜单，选择Run。

	

如果你测试正在运行，JMeter在右手上方的角落点燃一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"stop"，绿光依然会继续停留，知道所有测试都已经停止。

9构建一个LDAP测试计划

在这一节，你将学习到如何创建一个基本的测试计划来测试一个LDAP服务器。你将为在LDAP上的四个测试创建四个用户发送请求。同样，你要告诉用户运行他们的测试两次。所以，整个请求次数是（4用户）x (4请求）x （重复2次）=32LDAP请求。构建测试计划，你将使用下列元件：线程组，LDAP请求，LDAP请求默认值和表格视图结果。

这个例子，假定在你的本地机器上已经安装了LDAP服务器。

9.1添加用户

你想使用JMeter测试计划的第一步是添加一个线程组元件。线程组告诉JMeter你想要模拟的用户数，用户多长时间发送一次请求，和它们发送多少个请求。

继续进行，通过初次的选择测试计划添加线程组，单击鼠标右键得到添加菜单，然后选择添加-->线程组来添加一个线程组。你现在应该在测试计划下看到线程组。如果你没有看到这个元件，那么通过单击测试计划元件展开测试计划树。

图9.1 线程组默认值

9.2添加登录配置元件

开始选择Siptech User元件。点击鼠标右键得到添加菜单，然后选择添加-->登录配置元件。然后选择这个新元件来查看它的控制面板。

像大多JMeter元件一样，登录配置元件控制面板有名称域你可以修改。在这个例子中，保留它为默认值。

图9.2 登录配置元件测试计划

9.3添加LDAP请求默认值

开始选择Siptech User元件。单击鼠标右键得到添加菜单，然后选择添加-->LDAP请求默认值。选择这个新元件来查看它的控制面板。

像大多JMeter元件一样，LDAp请求默认值控制面板有名称域你可以修改。在这个例子中，保留它为默认值。

图9.3 LDAP请求默认值测试计划

	

在DN域输入"你服务器的根DN"。
在LDAP服务器的服务器名域输入"localhost"。
端口为389.
那些就是LDAP请求的默认值。

9.4添加LDAP请求

在我们测试计划我们需要准备四个LDAP请求。

1.  Inbuilt Add Test

2.  Inbuilt Modify Test

3.  Inbuilt Delete Test

4.  Inbuilt Search Test

JMeter以添加它们到树的顺序发送请求。开始添加第一个LADP请求到Siptech User元件（添加-->LDAP请求）。然后，在树中选择LDAP请求元件，编辑下列属性

1.  更改名称为Inbuilt-Add Test

2.  选择添加测试单选按钮

图9.4.1 Inbuilt Add test LDAP请求

你不需要设置服务器域和端口域，用户名，密码和DN，因为你已经在Login Config Element和LDAP请求默认值中指定了。

下一步，添加第二个LDAP请求，编辑下列属性

1.  更改名称为Inbuilt-Modify Test

2.  选择修改测试单选按钮

图9.4.2 Inbuilt Modify test LDAP请求

1.  更改名称为Inbuilt-Delete Test

2.  选择删除测试单选按钮

图9.4.3 Inbuilt-Delete Test LDAP请求

1.  更改名称为Inbuilt-Search Test

2.  选择搜索测试单选按钮

图9.4.4 Inbuilt-Search Test LDAP请求

9.5添加一个监听器浏览/保存测试结果

你需要添加到你测试计划的最后元件是一个监听器。这个元件责任是保存所有你的LDAP请求结果到一个文件，并且显示一个可视化数据模型。选择Siptech Users元件，添加一个表格视图结果（添加-->表格视图结果）。

图9.5表格视图结果监听器

9.6保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从文件菜单选择保存测试计划（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者仅仅其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"保存"。或者，选择合适测试计划元件，然后从编辑菜单选择保存。

9.7运行测试计划

从运行菜单，选择运行。

	

如果你测试正在运行，JMeter在右手上方的角落点亮一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"停止"，绿光依然会继续持续，直到所有测试都已经退出。

9 添加一个LDAP测试计划

在这一部分，你将学会如何去创建一个基础的测试计划来测试一个LDAP服务器。你会创建4个用户来给LDAP服务器发送4次请求。同样，你也可以让用户运行他们的测试2次。这样总的LDAP请求数量就是（4用户）*（4次请求）*（重复2次）=32。要构建这个测试计划，你将会用到下面的元件：线程组，LDAP请求，LDAP请求默认值，用表格查看结果。

	

这个例子假定你在你的个人机器上已经安装了LDAP服务器

9.1 添加用户

处理每个JMeter测试计划的第一步就是添加线程组元件。这个线程组会告诉JMeter你想要模拟的用户数量，用户应该发送请求的频率和应该发送的数量。

进一步来添加一个线程组：首先选择这个测试计划，用鼠标右键点击然后在得到的菜单中选择添加--> 线程组。这时你应该看到这个线程组已经在测试计划下面了，如果没有看到，就点击测试计划元件展开这个测试计划树。

Figure 9.1. Thread Group with DefaultValues

9.2添加Login Config Element

首先选择Siptech Users元件，右键点击，在弹出的菜单中选择Add --> ConfigElement --> Login Config Element。然后，选择这个新建的元件使它的控制面板显示出来。
像所有的JMeter元件一样，这个Login ConfigElement控制面板有一个名字域需要你来修改，在这个例子，我们取它的默认值。

Figure 9.2 Login Config Element for ourTest Plan

	

在UserName域中输入你的服务器用户名
在password域中输入你的服务器密码
LDAP请求的值为默认值。

9.3添加LDAP请求默认值

首先选择Siptech Users元件，右键点击，在弹出的菜单中选择Add --> Config Element --> LDAP Request Defaults。然后，选择这个新的元件使它的控制面板显示出来。
像所有的JMeter元件一样，这个Login ConfigElement控制面板有一个名字域需要你来修改，在这个例子，我们取它的默认值。


Figure 9.3 LDAP Defaults for our Test Plan

	

在DN域中输入你的服务器Root Dn
在LDAP Server's Servername域中输入"localhost"
端口设为389。
LDAP请求的值为默认值。

9.4添加LDAP请求

在我们这个测试计划， 我们需要创建4个LDAP请求。

1. Inbuilt添加测试

2. Inbuilt修改测试

3. Inbuilt删除测试

4. Inbuilt搜索测试

	

JMeter发送请求的次序就是你向树中添加它们的次序。

首先给Siptech Users添加第一个LDAP请求(Add --> Sampler --> LDAPRequest)。然后，在树型结构中选择这个LDAP请求元件修改下面的属性。

1. 修改名字Name为"Inbuilt-Add Test"。

2. 选择Serch Test单行框。

Figure 9.4.1LDAP Request for Inbuilt Add test

你不必需设置Server Name域,port 域，Username,Password和DN域，因为你已经在Login Config Element和LDAP请求默念值中确认了这些值。

下一步，添加第二个LDAP请求，并修改下面的属性值。

1. 修改名字Name为"Inbuilt-Modify Test"。

2. 选择Serch Test单行框。

Figure 9.4.2LDAP Request for Inbuilt Modify test

1. 修改名字Name为"Inbuilt-Delete Test"。

2. 选择Serch Test单行框。

Figure 9.4.3LDAP Request for Inbuilt Delete test

1. 修改名字Name为"Inbuilt-Serch Test"。

2. 选择Serch Test单行框。

Figure 9.4.4LDAP Request for Inbuilt Search test

9.5添加一个监听器浏览/保存测试结果

你需要添加到你测试计划的最后元件是一个监听器。这个元件责任是储存所有你的LDAP请求结果到文件，并且展示一个可视数据模型。

选择Siptech Users元件，添加一个Graph Results监听器（Add --> Listener -->View Results in Table）。

Figure 9.5 View result in Table Listener

9.6保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从File菜单选择Save Test Plan（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"Save"。或者，选择合适测试计划元件，然后从Edit菜单选择Save。

9.7运行测试计划

从Run菜单，选择Run。

	

如果你测试正在运行，JMeter在右手上方的角落点燃一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"stop"，绿光依然会继续停留，知道所有测试都已经停止。

10构建一个Web服务测试计划

在这章，你将学习如何创建一个测试web服务的测试计划。你将创建五个发送请求到一个页面的用户。同时，你将告诉用户运行他们的测试两次。所以整个请求是（5用户）*（1请求）*（重复2次）=10HTTP请求。为了构造测试计划，你将需要使用以下元件：测试计划、Web服务（SOAP）请求（beta版代码）和图表结果。

General notes on the webservices sampler.现在实现使用Apache SOAP驱动程序，需要来自sun的activation.jar和mail.jar包。由于协议限制，JMeter没有包含这些jar文件到二进制版本。请查阅SOAP文档的未来细节。

如果取样器表现出从web服务中得到一个错误，仔细检查SOAP消息，确认格式正确。细节方面，确认xmlns属性和WSDL是一样的。如果xml命名空间是不同的，web服务将会可能返回一个错误。Xmethods为那些想要测试他们的测试计划的人包含了一系列公用的web服务。

10.1添加用户

你想处理每个JMeter测试计划的第一步是添加线程组元件。线程组告诉JMeter你想模拟的用户数，用户发送请求的频率，和发送请求的数量。

顺便说一下，首先选择测试计划，右键点击得到Add菜单，并且选择Add->ThreadGroup，通过这种方式添加线程组。

现在你应该看到了测试计划下的线程组元件了。如果你看不到这个元件，单击测试计划元件展开测试计划树。

下一步，你需要修改默认配置。如果你还没有选择线程组元件，在树里选择它。现在在JMeter窗口右部你应该可以看到线程组控制面板。

（见下10.1）

图10.1 使用默认值的线程组

首先给线程组起一个更加有意义的名字。在name文本域，输入O'Reilly Users。

先一步，增加用户数（调用线程）到四个。

在下一个文本域——Ramp-UP Period，使用默认值0秒。这个属性告诉JMeter启动每个用户之间的时间间隔。例如，你输入Ramp-Up Period 为五秒，JMeter将会在最后5秒结束前启动所有你的用户。所以，如果我们有5个用户和一个5秒的Ramp-Up Period，那么启动用户的延迟就是1秒(5用户/5秒=1用户每秒）。如果你设置为那个值为零，那么JMeter将会立刻启动所以你的用户。

最后，清除标为"Forever"的复选框，并且在循环次数文本域中输入2。这个属性告诉JMeter重复你的测试的次数。如果你输入循环次数为0，那么JMeter将会运行你的测试一次。为了让JMeter重复运行你的测试计划，选择Forever复选框。

	

在大部分应用程序中，你必须在控制面板中手工改变。然而，在JMeter中，控制面板中自动接受你做的改变。如果你修改元件名，这个树会在你离开控制面板前自动使用新的文本更新这个树（例如，当你选择另一个树元件时）。

见图10.2 完整的Jakarta Users线程组。

图10.2 Jakarta Users线程组

10.2添加web服务请求

在我们的测试计划，我们将使用一个.NET web服务。自从你在使用web服务取样器，我们将不用深究写一个web服务的细节。如果你不知道如何写一个web服务，使用google搜索web服务并自己去熟悉写java和.NET的web服务。

构建一个JMS点对点测试计划

在本节中，你将学会如何创建一个测试计划来测试JMS点对点的解决方案。测试的建立是一个有五个线程的线程组，通过每个请求队列发送4个消息。一个固定的回复队列将用来监听应答消息。每个1到10次迭代。构建测试计划，你将使用下列元件：线程组，JMS点对点和图形结果。

大概介绍一下JMS。现在有两种JMS取样器。一个使用JMS主题，另一个使用队列。主题消息通常被称作发布/订阅消息。它一般使用的情况是一个生产者发布消息，多个订阅者来消费。

添加一个线程组

你想使用JMeter测试计划的第一步是添加一个线程组元件。线程组告诉JMeter你想要模拟的用户数，用户多长时间发送一次请求，和它们发送多少个请求。

继续进行，通过初次的选择测试计划添加线程组，单击鼠标右键得到一个菜单，然后选择添加-->线程组来添加一个线程组。

你现在应该在测试计划下看到了线程组。如果你没有看到这个元件，然后通过单击测试计划元件展开测试计划树。

下一步，你需要修改默认属性。如果你还没有选择线程组元件，那么在这个树中选择它。你现在应该在JMeter窗口的右边部分看到了线程组控制面板。（见下图：11.1）


图11.1使用默认值的线程组

开始，为我们的线程组提供一个更加有描述性的名字。在name域，输入Point-to-Point。

下一步，增加用户数（即线程）到5。

在下一个域中，Ramp-Up周期，保持默认值0秒。这个属性告诉JMeter启动每个用户之间有多长延迟。例如，如果你输入Ramp-up周期为5秒，JMeter会到5秒末完成启动所有你的用户。所以如果我们有五个用户和一个5秒的Ramp-up周期，那么启动用户之间的延迟将会是1秒（5用户/5秒=1用户每秒）。如果你设置为那个值为零，那么JMeter将会立刻启动所以你的用户。

最后，清除标为"Forever"的复选框，并且在循环次数域中输入4。这个属性告诉JMeter重复你的测试的次数。如果你输入循环次数为0，那么JMeter将会运行你的测试一次。为了让JMeter重复运行你的测试计划，可以选择Forever复选框。

	

在大部分应用程序中，你必须在控制面板中手工改变。然而，在JMeter中，控制面板中自动接受你做的改变。如果你修改元件名，这个树会在你离开控制面板前自动使用新的文本更新这个树（例如，当你选择另一个树元件时）。

11.2添加点对点取样器

确认你需要的jar文件在JMeter的lib目录下。如果它们不在，停止JMeter，拷贝jar文件过去，然后重启JMeter。

开始添加JMS点对点取样器到Jakarta用户元件（添加-->JMS点对点）。然后，在树中选择JMS点对点取样器元件。在构建例子中将提供一个使用ActiveMQ3.0工作的配置。

11.3添加一个监听器浏览/保存测试结果

你需要添加到你测试计划的最后元件是一个监听器。这个元件责任是保存所有你的HTTP请求结果到一个文件，并且显示一个可视化数据模型。

选择Jakarta Users元件，添加一个图形结果监听器（添加-->图形结果）。下一步，你需要指定一个目录和一个输出文件名。你可以，选择浏览按钮，浏览一个目录，然后输入一个文件名。

图11.2图形结果监听器

11.4保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从文件菜单选择保存测试计划（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者仅仅其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"保存"。或者，选择合适测试计划元件，然后从编辑菜单选择保存。

11.5运行测试计划

从运行菜单，选择运行。

	

如果你测试正在运行，JMeter在右手上方的角落点亮一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"停止"，绿光依然会继续持续，直到所有测试都已经退出。

一旦JMeter完成你的测试计划，从运行菜单选择停止。

如果你在监听器中选择一个文件保存结果，那么你将会有一个能够在任何visualizer中打开的文件。每个visualizer以它们自己的风格显示结果。

	

有可能会在多于一个的visualizer中打开同一个文件。这是没有问题的。JMeter会确保在测试运行时没有取样器记录到同一文件多于一次。

11.6ActiveMQ3.0的类库

下面是必须在JMeterlib\ext目录提供的类库。

1. activation.jar

2. activeio-1.0-SNAPSHOT.jar

3. activemq-3.0.jar

4. activemq-core-3.0.jar

5. commons-logging-1.0.3.jar

6. concurrent-1.3.4.jar

7. geronimo-spec-j2ee-jacc-1.0-rc4.jar

8. geronimo-spec-j2ee-management-1.0-rc4.jar

9. geronimo-spec-jms-1.1-rc4.jar

10.geronimo-spec-jta-1.0.1B-rc4.jar

11.jms.jar

12.jndi.jar

13.log4j-1.2.8.jar

14.spring-1.1.jar

12.创建JMS主题测试计划

在这章，你将学习如何创建一个测试计划去测试JMS提供者。你将创建五个订阅者和一个发布者。你将创建两个线程组并且设置一个为重复10次。消息总数是（6线程）x（1消息）x（重复10次）=60个消息。为了构造测试计划,你将使用以下元件：线程组、JMS发布者、JMS订阅者和图标结果。

一般在。当前有两个JMS取样器。一个使用JMS主题，另一个是使用JMS队列。主题消息是通常说的发布/订阅消息。在案例里它一般用在一个被生产者发布消息和多个订阅者接收消息的地方。队列消息一般被用在发送者期望得到一个响应时的事务。消息系统和普通的HTTP请求有很大不同。在HTTP中，单个用户发送一个请求并且得到一个响应。消息系统可以工作在同步和异步模式。

12.1添加用户

第一步是添加线程组元件。线程组告诉JMeter你想要模拟的用户数，用户多久发送一次请求，它们发送多少请求。

接着首先选择测试计划添加线程组元件，单击鼠标右键得到Add菜单，并且选择Add --> ThreadGroup。

你现在可以在测试计划下看到线程组元件。如果看不到这个元件，然后通过单击测试计划元件"展开"测试计划树。

下一步，你需要修改默认属性。如果你没有选择在树中的线程组，就选择它。你现在可以在JMeter窗口右部分看到线程组控制面板（见下12.1）。


图12.1 具有默认值的线程组

开始为线程组提供一个更有描述性的名字。在这个name文本域，输入Subscribers。

下一步，增加用户数（叫做线程）到5.

在下一个文本域——Ramp-UP Period，使用默认值0秒。这个属性告诉JMeter启动每个用户之间的时间间隔。例如，你输入Ramp-Up Period 为五秒，JMeter将会在最后5秒结束前启动所有你的用户。所以，如果我们有5个用户和一个5秒的Ramp-Up Period，那么启动用户的延迟就是1秒(5用户/5秒=1用户每秒）。如果你设置为那个值为零，那么JMeter将会立刻启动所以你的用户。

最后，清除标为"Forever"的复选框，并且在循环次数文本域中输入2。这个属性告诉JMeter重复你的测试的次数。如果你输入循环次数为0，那么JMeter将会运行你的测试一次。为了让JMeter重复运行你的测试计划，选择Forever复选框。

	

在大部分应用程序中，你必须在控制面板中手工改变。然而，在JMeter中，控制面板中自动接受你做的改变。如果你修改元件名，这个树会在你离开控制面板前自动使用新的文本更新这个树（例如，当你选择另一个树元件时）。

见图8.2 完整的O'Reilly Users线程组。

Unable to render embedded object: File(threadgroup2.png) not found.

12.2添加JMS订阅者和发布者

确认在JMeter的lib文件夹下有需要的jar包。如果没有，关闭JMeter，拷贝jar文件过去，重启JMeter。

开始添加JMS Subscriber取样器到Jakarta Users元件（Add --> Sampler -->JMS Subscriber）。然后，在树中选择JMS Subscriber元件，并且编辑下列属性：
#改变Name域为"samplesubscriber"
#如果JMS提供者使用jndi.properties，选择这个复选框
#输入InitialContextFactory的类名
#输入提供者URL，
#输入连接工厂名。请参考JMS提供者的文档信息
#输入消息主题名
#如果JMS提供者需要认证，选择"required"并且输入用户名和密码。例如，Orion JMS需要认证，然而ActiveMQ和MQSeries不需要
#"ActiveMQ and MQSeries"中输入10.因为性能原因，the sampler will aggregate messages, since small messages willarrive very quickly. If the sampler didn't aggregate the messages, JMeterwouldn't be able to keep up.
#如果你需要读取响应，选择这个复选框
#There are two client implementations for subscribers. If the JMS providerexhibits zombie threads with one client, try the other.

图12.2 JMS Subscriber

#改变Name域为"sample publisher"
#如果JMS提供者使用jndi.properties，选择这个复选框
#输入InitialContextFactory的类名
#输入提供者URL，
#输入连接工厂名。请参考JMS提供者的文档信息
#输入消息主题名
#如果JMS提供者需要认证，选择"required"并且输入用户名和密码。例如，Orion JMS需要认证，然而ActiveMQ和MQSeries不需要
#"ActiveMQ and MQSeries"中输入10.因为性能原因，the sampler will aggregate messages, since small messages willarrive very quickly. If the sampler didn't aggregate the messages, JMeterwouldn't be able to keep up.
#Select the appropriate configuration for getting the message to publish. Ifyou want the sampler to randomly select the message, place the messages in adirectory and select the directory using browse.
#Select the message type. If the message is in object format, make sure themessage is generated correctly.

图12.3. JMS Publisher

12.3添加一个监听器浏览/保存测试结果

你需要添加到你测试计划的最后元件是一个监听器。这个元件责任是储存所有你的HTTP请求结果到文件，并且展示一个可视数据模型。

选择Jakarta Users元件，添加一个Graph Resultsr监听器（Add --> Listener -->Graph Results）。 Next, you need to specify a directoryand filename of the output file. You can either type it into the filenamefield, or select the Browse button and browse to a directory and then enter afilename.

图12.4 Graph Results监听器

12.4保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从File菜单选择Save Test Plan（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"Save"。或者，选择合适测试计划元件，然后从Edit菜单选择Save。

12.5运行测试计划

从Run菜单，选择Run。

	

如果你测试正在运行，JMeter在右手上方的角落点燃一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"stop"，绿光依然会继续停留，知道所有测试都已经停止。

一旦JMeter完成你的测试计划，从Run菜单选择Stop。

如果你在你的监听器中选择一个文件保存结果，然后你将有一个能够在任何可视化工具下打开的文件。
每一可视化工具会使用它自己的风格去显示结果。

	

 

如果可能在多个可视化工具中打开同一个文件。这是不是问题。JMeter会保证在测试运行期间没有取样会再次被记录于同一文件。

13构建一个监视器测试计划

在这一节，你讲学习如何创建一个测试计划来监视web服务器。监视器对一个压力测试和系统管理很有用。使用压力测试，监视器可以提供一些关于服务器性能的附加信息。它也会使看出服务器性能和在客户端响应时间直接的关系更加容易。作为一个系统管理员工具，监视器提供很容易的方法从一个控制台监视多个服务器。监视器设计使用运行在Tomcat 5下

13.1

13.2HTTP认证管理

13.3添加HTTP请求

添加HTTP请求到线程组元件（添加-->HTTP请求）。然后，在树中选择HTTp请求元件，并编辑下列属性：

1.  修改名称域为"ServerStatus"

2.  输入IP地址和主机名

3.  输入端口号

4.  如果使用Tomcat，设置Path域为"/manager/status"

5.  添加名为大写的"XML"请求参数，给它一个小写的"true"值

6.  选择取样器的底部"Use asMonitor"

13.4添加固定定时器

添加一个定时器到这个线程组（添加-->固定定时器）。在"线程延迟"方框输入5000毫秒。一般使用间隔少于5秒会给你服务器添加压力。在你在你的产品环境部署监视器前找出一个可接受的间隔。

13.5添加一个监听器保存测试结果

如果你想保存来自服务器的结果，添加一个简单的数据监听器。如果你想保存计算的统计表，在监听器输入一个文件名。如果你想保存产生数据和统计表，确认你使用不同的文件名。

选择线程组元件，添加一个简单数据记录器监听器（添加-->简单数据记录器）。下一步，你需要指定一个目录和一个输出文件文件名。你可以在文件名域输入它，也可以选择浏览按钮，浏览一个目录，然后加入一个文件名。

13.6添加监视器结果

通过选择测试计划元件添加监听器（添加-->监视器结果）。在监视器结果监听器中有两个tab。第一个是"健康"，它显示了监视器受到的最后取样的状态。第二个tab是"性能"，它显示了服务器性能的历史视图。

Unable to render embedded object: File(monitor_health.png) not found.

一个关于健康情况的快速注释会被计算出来。典型地，一个服务器内存用完或者达到最大线程数，它就要崩溃。如果是Tomcat 5，一旦线程到达最大，请求将被放置到一个队列直到一个线程可用。在容器之间线程关系的重要性改变很大，所以现在使用50/50的实现更加保守。一个更加有效管理线程的容器可能看不到任何性能的下降，但是使用的内存也肯定会显示一些影响。

Unable to render embedded object: File(monitor_screencap.png) not found.

性能图像显示为不同的线条。空闲内存线显示在当前已分配存储块剩余多少空闲内存。Tomcat 5返回最大内存，但是它没有被绘制。在一个调试好的环境，服务器应该从不达到最大内存。

注意在图形的两边都有标题。在左边是百分比，右边是死亡/健康。如果内存线尖峰上升和下降迅速，它可能指示memory thrashing。在其它情况，使用Borland OptimizeIt或者JProbe是一个好方法。你想看到的是对于负载，内存和线程的一个规则的图案。任何不确定路线的状态常常都预示了不良的性能或者某个种类的一个bug。

13.7保存测试计划

虽然它不是需要的，但是我们推荐你在运行前保存测试计划到一个文件。为了保存测试计划，从文件菜单选择保存测试计划（使用最新版本，它不再需要首先选择测试计划元件）。

	

JMeter允许你保存这个测试计划树或者仅仅其中一部分。为了仅保存在测试计划树上的特殊"分支"，选择在树中用来启动"分支"的测试计划元件，然后右击在菜单项中选择"保存"。或者，选择合适测试计划元件，然后从编辑菜单选择保存。

13.8运行测试计划

从运行菜单，选择运行。

	

如果你测试正在运行，JMeter在右手上方的角落点亮一个绿正方形显示。当所有测试停止，那个方块变成灰色。即使你选择了"停止"，绿光依然会继续持续，直到所有测试都已经退出。

一旦JMeter完成你的测试计划，从运行菜单选择停止。

如果你在监听器中选择一个文件保存结果，那么你将会有一个能够在任何visualizer中打开的文件。每个visualizer以它们自己的风格显示结果。

	

有可能会在多于一个的visualizer中打开同一个文件。这是没有问题的。JMeter会确保在测试运行时没有取样器记录到同一文件多于一次。

14.监听器介绍

监听器是显示取样器结果的组件。结果可以显示在树、表格、图表或者简单的写入一个日志文件。为了观察来自提供的取样器的响应内容，可以添加"观察结果树"或者"在表格观察结果"监听器到测试计划。为了图形化观察响应时间，可以添加图形结果

	

不同的监听器使用不同的方法显示响应信息。然而，如果他们其中一个被指点，他们所有使用相同的原始数据写入到输出文件。

"配置"按钮可以指定那些域被写入文件，和是否把它作为一个CSV或者XML文件。CSV文件比XML文件小得多，所有如果产生大量的取样建议使用CSV文件。

如果你仅期望记录某几个取样，可以添加监听器作为取样器的一个子节点。或者你可以使用简单控制器去组织取样器集，并且添加监听器到那个控制器。相同的文件可以被多个取样器使用-但是确定它们都使用相同的配置！

14.1屏幕捕获

JMeter能够保存任何监听器作为一个PNG文件。在左边的面板选择监听器。单击edit -> Save As Image


图1-Edit -> Save As Image

14.2非GUI测试运行

当在非GUI模式运行时，使用-l标志为测试运行创建一个顶级监听器。

14.3资源使用

监听器。为了最小的资源使用，删除所有的监听器，并且使用-l标志运行测试在非GUI模式来定义仅一个监听器。这样在测试完成之后日志文件可以被重新读取到一个监听器。

14.4CSV日志格式

CSV日志格式依赖于在配置中被选择的数据项。仅那些指定的数据项被记录在文件。列的表现顺序是固定的，如下：

*时间标志-自从1970-1-1的毫秒数
*用时-毫秒
*标签-取样器标签
*响应代码-例如200、404
*响应消息-例如OK
*线程名
*数据类型
*成功与否-true或者false
*失败消息-如果要的话
*字节数-在取样中的字节数
*URL

XML文件格式如下：

14.6XML日志格式2.0

原始XML（2.0）格式如下（转行可以不相同）：

<?xml version="1.0" encoding="UTF-8"?>

<testResults version="1.2">

<sampleResult timeStamp="1144365463297" dataType="text" threadName="Listen 1-1" label="HTTP Request" time="1502" responseMessage="OK" responseCode="200" success="true">

 <sampleResult timeStamp="1144365464238" dataType="text" threadName="Listen 1-1" label="http://www.apache.org/style/style.css" time="171" responseMessage="OK" responseCode="200" success="true">

 <property xml:space="preserve" name="samplerData">

 GEThttp://www.apache.org/style/style.css

 </property>

 <binary>

 body, td, th {

   font-size: 95%;

   font-family: Arial, Geneva,Helvetica, sans-serif;

   color: black;

   background-color: white;

 }

 ...

 </binary>

 </sampleResult>

</sampleResult>

...

</testResults>

14.6XML日志格式2.1

更新的XML（2.1）格式如下（转行可以不相同）：

<?xml version="1.0" encoding="UTF-8"?>

<testResults version="1.2">

-- HTTP Sample, with nested samples

 

<httpSample t="1392" lt="351" ts="1144371014619" s="true" lb="HTTP Request" rc="200" rm="OK" tn="Listen 1-1" dt="text" de="iso-8859-1" by="12407">

  <httpSample t="170" lt="170" ts="1144371015471" s="true" lb="http://www.apache.org/style/style.css" rc="200" rm="OK" tn="Listen 1-1" dt="text" de="ISO-8859-1" by="1002">

    <responseHeader class="java.lang.String">HTTP/1.1 200 OK

Date: Fri, 07 Apr 2006 00:50:14 GMT

...

Content-Type: text/css

</responseHeader>

    <requestHeader class="java.lang.String">MyHeader: MyValue</requestHeader>

    <responseData class="java.lang.String">body, td, th {

   font-size: 95%;

   font-family: Arial, Geneva,Helvetica, sans-serif;

   color: black;

   background-color: white;

}

...

</responseData>

    <cookies class="java.lang.String"></cookies>

    <method class="java.lang.String">GET</method>

    <queryString class="java.lang.String"></queryString>

    <url>http://www.apache.org/style/style.css</url>

  </httpSample>

  <httpSample t="200" lt="180" ts="1144371015641" s="true" lb="http://www.apache.org/images/asf_logo_wide.gif" rc="200" rm="OK" tn="Listen 1-1" dt="bin" de="ISO-8859-1" by="5866">

    <responseHeader class="java.lang.String">HTTP/1.1 200 OK

Date: Fri, 07 Apr 2006 00:50:14 GMT

...

Content-Type: image/gif

</responseHeader>

    <requestHeader class="java.lang.String">MyHeader: MyValue</requestHeader>

    <responseData class="java.lang.String">http://www.apache.org/images/asf_logo_wide.gif</responseData>

     <responseFile class="java.lang.String">Mixed1.html</responseFile>

    <cookies class="java.lang.String"></cookies>

    <method class="java.lang.String">GET</method>

    <queryString class="java.lang.String"></queryString>

    <url>http://www.apache.org/images/asf_logo_wide.gif</url>

  </httpSample>

  <responseHeader class="java.lang.String">HTTP/1.1 200 OK

Date: Fri, 07 Apr 2006 00:50:13 GMT

...

Content-Type: text/html;charset=ISO-8859-1

</responseHeader>

  <requestHeader class="java.lang.String">MyHeader: MyValue</requestHeader>

  <responseData class="java.lang.String">

...

 

&lt;html&gt;

 &lt;head&gt;

...

 &lt;/head&gt;

 &lt;body&gt;       

...

 &lt;/body&gt;

&lt;/html&gt;

</responseData>

  <cookies class="java.lang.String"></cookies>

  <method class="java.lang.String">GET</method>

  <queryString class="java.lang.String"></queryString>

  <url>http://www.apache.org/</url>

</httpSample>

-- nonHTTPP Sample

<sample t="0" lt="0" ts="1144372616082" s="true" lb="Example Sampler" rc="200" rm="OK" tn="Listen 1-1" dt="text" de="ISO-8859-1" by="10">

  <responseHeader class="java.lang.String"></responseHeader>

  <requestHeader class="java.lang.String"></requestHeader>

  <responseData class="java.lang.String">Listen 1-1</responseData>

  <responseFile class="java.lang.String">Mixed2.unknown</responseFile>

  <samplerData class="java.lang.String">ssssss</samplerData>

</sample>

</testResults>

	

取样节点名字可以是"sample"或者"httpSample"。

取样器属性意义如下：

属性
	

内容

t
	

用时（ms）

lt
	

延时（ms）-不是所有的取样器支持这个

ts
	

时间标志

s
	

是否成功

lb
	

标签

rc
	

响应代码

rm
	

响应消息

tn
	

线程名

dt
	

数据类型

de
	

数据编码

by
	

字节数

ng
	

在这个线程组中活跃的线程数

na
	

所有线程组中的活跃线程数

JMeter2.1和2.1.1版本保存响应代码为"rs"，但是读取它期望是"rc"。这个bug已经被修复，所以为"rc"；"rc"或者"rs"都可以被读取。

14.7保存响应数据

像上面展示的那样，如果需要响应数据可以被保存为XML日志文件。然而，这将使文件相当大，并且文本必须被编码才可以被安静的验证XML。同样图片不会被包括。

另一个解决方案是使用后置处理器保存响应结果到文件。这样为每个取样产生一个新的文件，并且保存文件为取样器名。文件名会被包含在一个取样日志输入。当取样日志文件被加载时如果需要数据将从文件从新得到。












