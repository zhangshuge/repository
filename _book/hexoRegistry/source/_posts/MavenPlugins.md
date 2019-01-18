---
title: MavenPlugins
date: 2018-09-04 21:49:03
categories:
tags:
---
Maven的Assembly Plugin主要用于允许用户将项目输出及其依赖项，模块，站点文档和其他文件集中到一个可分发的归档文件中。

目前支持的格式:

 * jar
 * zip
 * tar
 * tar.gz
 * tar.bz2
 * dir
 * war

默认情况下，打jar包时，只有在类路径上的文件资源会被打包到jar中，并且文件名是`${artifactId}-${version}.jar`，下面看看怎么用maven-assembly-plugin插件来定制化打包。

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>2.5.5</version>
    <executions>
        <execution>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

自定义Assembly Descriptor

```xml
    <build>
        <resources>
            <resource>
                <!--指定配置文件路径-->
                <directory>src/resources</directory>
            </resource>
        </resources>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <configuration>
                    <!--指定assembly打包描述文件-->
                    <descriptor>src/assembly/gorges-app-assembly.xml</descriptor>
                    <!--最终打包的名称-->
                    <finalName>gorges-app-${project.version}</finalName>
                </configuration>
                <executions>
                    <!--execution的设置是为了将maven-assembly-plugin继承到标准的maven打包过程中，这样在运行maven-package时就会执行maven-                             assembly-plugin的操作，从而实现我们需要的自定义打包。-->
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                        <configuration>
                            <tarLongFileMode>posix</tarLongFileMode>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```

gorges-app-assembly.xml

```xml
<assembly xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2 http://maven.apache.org/xsd/assembly-1.1.2.xsd">
    <id>assembly</id>
    <!--最终的打包格式-->
    <formats>
        <format>jar</format>
    </formats>
    <!--在最终归档中包含一个基本目录。例如，如果您正在创建名为“your-app”的程序集，则将includeBaseDirectory设置为true将创建一个包含此基本目录的归档文         件。如果此选项设置为false，则创建的存档将其内容解压缩到当前目录。-->
    <includeBaseDirectory>false</includeBaseDirectory>
    <!--指定要包含在程序集中的哪些依赖项。-->
    <dependencySets>
        <dependencySet>
            <!--设置输出目录相对于程序集根目录的根目录。-->
            <outputDirectory>/</outputDirectory>
            <!--当前项目构件是否包含在这个依赖集合里。-->
            <useProjectArtifact>false</useProjectArtifact>
            <!--如果设置为true，则此属性将所有依赖项解包到指定的输出目录中。当设置为false时，依赖关系将包含为归档（jar）。只能解压缩jar，zip，tar.gz和                 tar.bz压缩文件。-->
            <unpack>true</unpack>
            <!--为这个依赖集设置依赖性范围。-->
            <scope>runtime</scope>
            <!--指定包含/排除/过滤从归档中提取的项目的选项。-->
            <unpackOptions>
                <excludes>
                    <exclude>**/application.conf</exclude>
                    <exclude>**/defaults.yaml</exclude>
                    <exclude>**/*storm.yaml</exclude>
                    <exclude>**/*storm.yaml.1</exclude>
                    <exclude>**/log4j.properties</exclude>
                    <exclude>**/log4j2.xml</exclude>
                    <exclude>**/com.nucc.channel.gorges.app.ApplicationProvider</exclude>
                    <exclude>**/com.nucc.channel.gorges.evaluator.EvaluatorProvider</exclude>
                    <exclude>**/com.nucc.channel.gorges.runtime.ExecutionRuntimeProvider</exclude>
                </excludes>
            </unpackOptions>
            <excludes>
                <exclude>org.slf4j:slf4j-api</exclude>
                <exclude>org.slf4j:slf4j-log4j12</exclude>
                <exclude>io.dropwizard:**</exclude>
                <exclude>org.apache.storm:storm-core</exclude>
                <exclude>org.springframework:**</exclude>
                <exclude>org.springframework.*:**</exclude>
            </excludes>
        </dependencySet>
    </dependencySets>

    <fileSets>
        <fileSet>
            <directory>${project.build.outputDirectory}</directory>
            <outputDirectory>/</outputDirectory>
            <excludes>
                <exclude>**/application.conf</exclude>
                <exclude>**/log4j.properties</exclude>
                <exclude>**/storm.yaml.1</exclude>
            </excludes>
            <includes>
                <include>META-INF/services/</include>
            </includes>
        </fileSet>
    </fileSets>
</assembly>
```

## templating-maven-plugin

?	模板化maven插件处理将文件从源文件复制到给定的输出目录，同时对它们进行过滤。如果您需要例如将代码中的内容替换为某些属性值，则此插件可用于过滤Java源代码。

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>templating-maven-plugin</artifactId>
    <executions>
        <execution>
            <id>filtering-java-templates</id>
            <phase>generate-sources</phase>
            <goals>
                <goal>filter-sources</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

![e5c5ecd8cceeaea142757](http://oy48q6kwm.bkt.clouddn.com/e5c5ecd8cceeaea142757cc9f31fda6d.png)
