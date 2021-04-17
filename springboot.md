1.@EnableAutoConfiguration

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
```

他会根据我添加的jar包依赖去猜测我想要怎么配置spring。就像spring-boot-start-web添加了tomcat和springmvc，他会猜测我想要开发一个web应用，会帮我自动去配置。

2.运行方式

mvn spring-boot：run

```xml
<build>
    <plugins>
        <plugin>
           <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

这个是打jar包用的

3.parent的依赖问题

问题引出：在一些公司自己的研发环境中，有自己的版本控制。并不是通用的引入spring-boot-starter-parent，你可以用import进行导入

```xml
<dependencyManagement>
     <dependencies>
        <dependency>
            <!-- Import dependency management from Spring Boot -->
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.0.0.BUILD-SNAPSHOT</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

4.autowire注入final的bean对象（构造函数）

```java
package com.example.service;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;


@Service
public class DatabaseAccountService implements AccountService {
    
    private final RiskAssessor riskAssessor;
    @Autowired
    public DatabaseAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
    }
    // ...
}
```

5.开发者工具

```
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

当classpath中的文件修改时，使用spring-boot-devtools的应用会自动重启。当使用IDE开发时，这是一个很有用的功能，因为代码改变时它能快速的进行反馈。默认情况下，会监控classpath指向的文件夹中任何条目的变化。注意某些资源例如静态资源和视图模板不需要重启应用

