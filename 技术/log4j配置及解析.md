### log4j配置文件

**示例:**

```properties
# Set root category priority to INFO and its only appender to CONSOLE.
#log4j.rootCategory=INFO, CONSOLE            debug   info   warn error fatal
log4j.rootCategory=debug, CONSOLE, LOGFILE

# Set the enterprise logger category to FATAL and its only appender to CONSOLE.
log4j.logger.org.apache.axis.enterprise=FATAL, CONSOLE

# CONSOLE is set to be a ConsoleAppender using a PatternLayout.
log4j.appender.CONSOLE=org.apache.log4j.ConsoleAppender
log4j.appender.CONSOLE.layout=org.apache.log4j.PatternLayout
log4j.appender.CONSOLE.layout.ConversionPattern=%d{ISO8601} %-6r [%15.15t] %-5p %30.30c %x - %m%n

LOGFILE is set to be a File appender using a PatternLayout.
log4j.appender.LOGFILE=org.apache.log4j.FileAppender
log4j.appender.LOGFILE.File=d:\axis.log
log4j.appender.LOGFILE.Append=true
log4j.appender.LOGFILE.layout=org.apache.log4j.PatternLayout
log4j.appender.LOGFILE.layout.ConversionPattern=%d{ISO8601} %-6r [%15.15t] %-5p %30.30c %x - %m%n

```



**1、log4j.rootCategory=INFO, stdout , R ** `(重点)`

> 此句为将等级为INFO的日志信息输出到stdout和R这两个目的地，stdout和R的定义在下面的代码，`可以任意起名`。等级可分为OFF、FATAL、ERROR、WARN、INFO、[DEBUG](https://baike.baidu.com/item/DEBUG)、ALL，如果配置OFF则不打出任何信息，如果配置为[INFO](https://baike.baidu.com/item/INFO)这样只显示INFO、WARN、ERROR的[log](https://baike.baidu.com/item/log)信息，而DEBUG信息不会被显示，具体讲解可参照第三部分定义配置文件中的logger。



**2、log4j.appender.stdout=org.apache.log4j.ConsoleAppender**

> 此句为定义名为`[stdout]`的输出端是哪种类型，可以是
>
> org.apache.log4j.ConsoleAppender（控制台），
>
> org.apache.log4j.FileAppender（文件），
>
> org.apache.log4j.DailyRollingFileAppender（每天产生一个日志文件），
>
> org.apache.log4j.RollingFileAppender（文件大小到达指定尺寸的时候产生一个新的文件）
>
> org.apache.log4j.WriterAppender（将日志信息以流格式发送到任意指定的地方）



**3、log4j.appender.`stdout`.layout=org.apache.log4j.PatternLayout**

> 此句为定义名为stdout的输出端的layout是哪种类型，可以是
>
> org.apache.log4j.HTMLLayout（以[HTML](https://baike.baidu.com/item/HTML)表格形式布局），
>
> org.apache.log4j.PatternLayout（可以灵活地指定布局模式），
>
> org.apache.log4j.SimpleLayout（包含日志信息的级别和信息[字符串](https://baike.baidu.com/item/字符串)），
>
> org.apache.log4j.TTCCLayout（包含日志产生的时间、[线程](https://baike.baidu.com/item/线程)、类别等等信息）
>
> 具体讲解可参照第三部分定义配置文件中的Layout。



**4、log4j.appender.`stdout`.layout.ConversionPattern= [QC] %p [%t] %C.%M(%L) | %m%n**

> 如果使用pattern布局就要指定的打印信息的具体格式ConversionPattern，打印参数如下：
>
> %m 输出代码中指定的消息；
>
> %M 输出打印该条日志的方法名；
>
> %p 输出优先级，即DEBUG，[INFO](https://baike.baidu.com/item/INFO)，WARN，ERROR，FATAL；
>
> %r 输出自应用启动到输出该log信息耗费的毫秒数；
>
> %c 输出所属的类目，通常就是所在类的全名；
>
> %t 输出产生该日志事件的线程名；
>
> %n 输出一个回车换行符，Windows平台为"rn”，Unix平台为"n”；
>
> %d 输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如：%d{yyyy-MM-dd HH:mm:ss,SSS}，输出类似：2002-10-18 22:10:28,921；
>
> %l 输出日志事件的发生位置，及在代码中的行数；
>
> [QC]是log信息的开头，可以为任意字符，一般为项目简称。
>
> 输出的信息
>
> [TS] DEBUG [main] AbstractBeanFactory.getBean(189) | Returning cached instance of singleton bean 'MyAutoProxy'
>
> 具体讲解可参照第三部分定义配置文件中的格式化日志信息。



**5、log4j.appender.`R`=org.apache.log4j.DailyRollingFileAppender**

> 定义名为R的输出端的类型为每天产生一个日志文件。



**6、log4j.appender.`R`.File=D:\\Tomcat 5.5\\logs\\qc.log**

> 此句为定义名为R的输出端的文件名为D:\\Tomcat 5.5\\logs\\qc.log可以自行修改。



**7、log4j.appender.`R`.layout=org.apache.log4j.PatternLayout**

> 输出的日志布局



**8、log4j.appender.`R`.layout.ConversionPattern=%d-[TS] %p %t %c - %m%n**

> 自定义格式输出，参考4点的格式



**9、log4j.logger.com. neusoft =DEBUG**

> 指定com.neusoft包下的所有类的等级为DEBUG。



**10、log4j.logger.com.opensymphony.oscache=ERROR**

**11、log4j.logger.net.sf.navigator=ERROR**

> 这两句是把这两个包下出现的错误的等级设为ERROR，如果项目中没有配置EHCache(二级缓存)，则不需要这两句。



**12、log4j.logger.org.apache.commons=ERROR**

**13、log4j.logger.org.apache.struts=WARN**

> 这两句是struts的包。



**14、log4j.logger.org.displaytag=ERROR**

> 这句是displaytag的包。（QC问题列表页面所用）



**15、log4j.logger.org.springframework=DEBUG**

> 此句为Spring的包。



**16、log4j.logger.org.hibernate.ps.PreparedStatementCache=WARN**

**17、log4j.logger.org.hibernate=DEBUG**

> 此两句是hibernate的包。
>
> 以上这些包的设置可根据项目的实际情况而自行定制。