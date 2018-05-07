 # JMeter中文使用手册
## 1.简介

　　<p> Apache JMeter是100%纯java桌面应用程序，被设计用来测试C/S结构的软件（例如web应用程序）。它可以被用来测试包括基于静态和动态资源程序的性能，例如静态 文件，JavaServlets，Java 对象，数据库，FTP 服务器等等。JMeter可以用来模拟一个在服务器、网络或者对象上大的负载来测试或分析在不同的负载类型下全面性能.</P>

　<strong>　另外，JMeter能够通过让你们用断言创造测试脚本来验证我们的应用程序是否返回了我们期望的结果，从而帮助我们回归测试我们的程序。为了最大的灵活性，JMeter允许我们使用正则表达式创建断言。</strong>
- 1.1 历史

　　Apache软件组织的Stefano Mazzocchi是JMeter的创始人。他写出它起初是为了测试Apache JServ的性能（一个已经被Apache Tomcat工程所替代的工程）。我们重新设计JMeter来增强用户界面和增加功能测试的能力。
1.2 未来

　　我们希望看到作为开发者利用它的可插入架构使JMeter的功能快速扩展。未来发展的主要目标是在没有危机JMeter的负载测试能力的情况下尽可能使JMeter成为最实用的回归测试工具。
2 入门

　　开始使用JMeter最容易的方法是首先下载最新版并且安装它。这个版本包含所有你在构建和运行Web，FTP，JDBC，和JNDI测试时使用的所有文件。如果你想执行JDBC测试，你当然需要从厂商得到适当的JDBC驱动。JMeter没有提供任何JDBC驱动。

其它你可能需要下载的软件：

·　　BeanShell

·　　Java Activation Framework - JavaMail需要

·　　Java Mail - mail 显示 and SOAP 测试需要

·　　JMS - JMS 取样器

·　　General Java download page

详细参见安装的jar包中的 JMeter Classpath 一章

　　下一步, 开始使用JMeter并且参见用户手册构建测试计划一章使自己更加熟悉JMeter基础 (例如，添加和删除元素)。

　　最后, 参见如何构建一个明确类型的测试用例的适合章节。例如，如果你对Web应用测试感兴趣，那就参见构建一个Web测试计划。其他测试计划的细节是JDBC, FTP, and JNDI。

　　一旦你熟练构建和执行JMeter测试计划, 通过你的测试计划你会观察到给你更多帮助的各种元素的配置(定时器, 监听器, 断言, 和其他)。
2.1 需求

JMeter 需要运行环境匹配的最小需求。
2.1.1 Java 版本

　　JMeter 需要一个完整适当的JVM 1.3或更高的版本. 我们现在尽力与JVM 1.3保持兼容,然而JMeter在1.4或者更高运行的会最好。因为JMeter 仅使用Java标准API,请不要把因为JRE实现版本而无法运行JMeter的bug报告提交。 　　Java 1.3 不包括 SSL (HTTPS) 支持 - 你将需要下载 JSSE. 同样, 它不会像其他更高版本的Java那样好的运行。为了更好的结果使用Java1.4或者1.5。
2.1.2 操作系统

　　JMeter是100%纯Java应用程序并且能够正确的在任何有适当的Java实现的操作系统上运行。JMeter 在下列环境已经被测试:

·　　Unix (Solaris, Linux, 等)

·　　Windows (98, NT, 2000, xp)

·　　OpenVMS Alpha 7.3+
2.2 可选

如果你计划做JMeter开发或者想使用SUN的java标准扩展包，你将需要下列更多的可选包。
2.2.1 Java 编译器

如果你想编译JMeter源代码或者开发JMeter插件，你将需要一个完整的适当的JDK1.3或者更高。
2.2.2 SAX XML解析器

　　JMeter 使用 Apache's Xerces XML 解析器你可以选择告诉JMeter使用一个不同的XML 解析器。 这样做，把第三方的解析器的类包包含在JMeter的classpath 中， 并更新 jmeter.properties 文件里的解析器实现的全类名。
2.2.3 Email 支持

　　JMeter 有有限的 Email 能力。 它能够发送给你测试结果的email，并且支持POP/IMAP 取样器。它现在不支持 SMTP 取样。 为了能够支持 Email, 需要添加Sun 的JavaMail包和activation包到JMeter classpath 。
2.2.4 SSL 加密

　　为了测试一个使用SSL加密（HPPS）的web服务器， JMeter 需要一个提供SSL实现(例如 Sun的 Java Secure SocketsExtension - JSSE）。包含需要的加密包到JMeter的 classpath 。 同样,通过注册SSL提供者更新 jmeter.properties 。为了更好的管理证书，也要有一个SSL 管理器 。
注意

如果你在JDK1.4上运行，你将不需要下载JSSE，因为SUN已经集成它到JDK1.4中做为标准类库了。JMeter 代理服务器(见下)不支持记录SSL(https)。
2.2.5 JDBC 驱动

你需要添加你的厂商的JDBC驱动到classpath，如果你需要JDBC测试.确认文件是一个jar文件，而不是zip。
2.2.6 Apache SOAP

　　ApacheSOAP 需要 mail.jar 和 activation.jar. 你需要下载并拷贝两个jar文件到你jmeter/lib 目录.一旦文件放到那里，JMeter 会自动找到它们。 详细参见安装的jar包中的 JMeter Classpath 一章
2.3 安装

快速安装JMeter。细节依赖你下载的发布文件。
注意
