---
title: project note
auther: ahou
---


MySQL
<mysql.version>8.0.16</mysql.version>  
driverClassName = com.mysql.cj.jdbc.Driver  
url = jdbc:mysql://localhost:3306/testDb?serverTimezone=Asia.Shanghai  

云服务器在远程访问时需要开放访问端口，在线配置安全规则  


在IDEA在配置Modules编译JDK版本的时候会看到以下的提示，

Module xxx is imported from Maven.Any changes made in its ......  
[article](https://blog.csdn.net/wohiusdashi/article/details/88362799)  
修改pom.xml文件配置  
``` xml
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
</build>
```