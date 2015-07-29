# Maven setup

AchternEngine is getting pushed to maven central for all releases (except nightly builds),
this allows you to get started easily.

Simply add this to your dependencies and you're set!

```xml
<dependency>
    <groupId>org.achtern</groupId>
    <artifactId>AchternEngine</artifactId>
    <version>0.4</version>
</dependency>
```

This allows you to develop your game in your favorite IDE or text editor, but if you want to run the
project directly within your IDE you have to have the native bindings in your classpath.

In your build process add this plugin to copy the native bindings into the target folder:

```xml
<plugin>
    <groupId>com.googlecode.mavennatives</groupId>
    <artifactId>maven-nativedependencies-plugin</artifactId>
    <version>0.0.7</version>
    <executions>
        <execution>
            <id>unpacknatives</id>
            <phase>generate-resources</phase>
            <goals>
                <goal>copy</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

In addition to that AchternEngine uses [slf4j](http://www.slf4j.org/) as logging framework, you need to provide the implementation for that.
You can use whatever you want and fits your project, but I recommend to use [logback](http://logback.qos.ch/)!

```xml
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.0.13</version>
</dependency>
```

And add the following basic configuration file `logback.xml` into your resource folder:

```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <!-- encoders are assigned the type
             ch.qos.logback.classic.encoder.PatternLayoutEncoder by default -->
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="info">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

Now you are all set and can [get started](../get_started)
