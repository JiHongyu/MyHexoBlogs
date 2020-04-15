---
title: springboot_1
date: 2020-04-14 23:40:03
tags: springboot 
---


## 命令行创建 Springboot 应用

需要借助 Maven archetype 插件，从模板原型构建应用。

```bash
mvn archetype:generate -B -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.1 -DgroupId=com.company -DartifactId=project -Dversion=1.0-SNAPSHOT -Dpackage=com.company.project
```

查看依赖树

```bash
mvn dependency:tree -Dincludes=xxx
```

Maven spring-boot 插件在 spring-boot-starter-parent Pom 文件中。需要通过 `mvn spring-boot:run` 启动 sprinboot 应用需要在 pom 文件引入该 parent。

通过 `mvn spring-boot:run` 启动的话 Pom 文件里面不需要构建脚本。

springboot 应用打包成 jar 包需要 `spring-boot-maven-plugin` 插件。

编译的目录结构：

+ BOOT-INF/classes 存放编译后的 class 文件

+ BOOT-INF/lib 存放依赖的 jar 包

+ META-INF 存放应用相关元信息，例如 `MANIFEST.MF`

+ org/ 存放 springboot 相关的 class 文件

springboot 既可以打包成 Jar 包，也可以打包成 War 包运行。打成 war 包的时候需要手动在 POM 文件添加 `spring-boot-loader`


（未完待续）