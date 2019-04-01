## Sins of Java Logging
1. Logging plain user input - 
   a. This can lead to Log Forging where a malicious user might right some external data into the log file and thereby corrupting the data in the file with falsified
information.
   b. A way to overcome this is by using a tool like Enterprise Security API from OWASP which encodes the data before it is written to the logs, this is an open-source
library.

2. Excessive Logging -
   a. This can lead to heavy log files and also difficulty in reading them and finding relevant info.
   b. If you want to log entry and exit of every method then make use of @Aspect.

3. Not enough logging information -
   a. A log entry should contain the timestamp, log level, thread name and the fully qualified class name.
   b. Make sure you configure all these.

4. Using a single log file -
   a. If you use a single log file then over a period of time it becomes quite heavy and difficult to read.
   b. Instead, configure your logging framework in such a way that you write a file per day and also if the file exceeeds a certain size create a new file for the same day.

5. Not logging with JSON -
   a. If you log using the JSON format then the data will be a much better structured format which is also very beneficial for a log management system or a tool like
Retrace which can provide stats out-of-your-logs.

6. Performance -
   a. I/O ops are expensive hence you should try and minimize the no.of calls that happen.
   b. Consider using logger frameworks which uses asynchronous logging, as these create separate threads for logging and doesn't block application threads.


## SLF4J
1. Simple Logging Framework for Java is the Java Logging facade which provides basic functionalities for implementing a Logging framework.
2. You can just use SLF4J but the general practice is to use SLF4J as the foundation and extend it with other frameworks like Log4j2 or Logback.
3. Basically, SLf4J provides an api and on top of which you need a convertor which acts as a bridge b/w SLf4J and your library like a Log4j2 or Logback.
4. So, you need slf4j, the bridge and the actual library that of a log4j2 or logback.
5. Whether you use Log4j2 or Logback on top of SLf4J, the only that changes when you decide to change your logging framework, is the configuration, everything else
remains same. That is the power of using slf4j as a foundation.

## Logback
1. Spring Boot by default supports logback.
2. When using spring boot, you can configure spring-boot-starter-logging to get going.
3. Levels in Logback are : ERROR, WARN, INFO, DEBUG and TRACE. There is no FATAL in logback, which is actually mapped to ERROR.
4. While using spring boot, most of the logback configurations like the maxfilesize, filepath, format, archival days etc., can be set in the application.properties fileitself but if you need to set advanced configuration like specifying a SizeAndTimeBasedRollingPolicy then you need to configure these in the logback-spring.xml because the default logback.xml loads too quickly and these advanced configurations can't be made in it.
5. In advanced config, you can config to specify log archival rules based on size, time or both.
6. You can also have separate log config for dev and prod mentioned in the logback-spring.xml using spring profiles and mention the appropriate spring profile either as env variable or as a jvm arg.
7. logback-classic module is the improved version of log4j and also natively implements slf4j but you need not worry about all these when using sprig boot, just use spring boot starter logging.
8. You can create separate logs for different types of events like separate server logs, app logs and similarly other separate logs. DO NOT KNOW how to do it yet.
9. And SiftingAppender in logback is something using which you can create separate log files for separate sessions. for e.g., you can create separate files for each user. DO NOT KNOW yet how to do it.
10. Logback basically has 3 modules - logback-core (which does all the ground work for the other 2), logback-classic (which natively implements slf4j) an logback-access (which connects to servlet containers like tomcat, jetty etc.).
11. Logback is built on 3 main classes - Logger, Appender and Layouts.
12. The Appenders speak about the output destination of the log. Logbacks allows outputs to various destinations - console, files, rmeote socket servers, mysql, postgresql, oracle and other dbs, and jms. It is possible to attach multiple appenders to a single logger.
13. Parameterized Logging - is  a feature where you can pass dynamic log messages as params rather than perform string concat. Also, logback first checks whether the log levels will have to be printed and only then it creates the necessary objects for the params.
14.If you do no want the acnestor logs to be written/maintained then use additivty=false.
15. The Layout class is about formatting, it determines how the log output should be presented.

 	  
