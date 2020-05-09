# 从零开始学spring-boot

Spring Boot有优点:    

- 为所有Spring开发者更快的入门     
- 开箱即用，提供各种默认配置来简化项目配置     
- 内嵌式容器简化Web项目     
- 没有冗余代码生成和XML配置的要求     

## 准备事项    

Java 7及以上   
Spring Framework 4.1.5及以上    

## 使用Maven构建项目  

1. 通过SPRING INITIALIZR工具产生基础项目    
    - 访问：`http://start.spring.io/`  
    - 选择构建工具Maven Project、Spring Boot版本1.3.2以及一些工程基本信息
    - 点击Generate Project下载项目压缩包

2. 解压项目包，并用IDE以Maven项目导入，以IntelliJ IDEA 14为例：  
    - 菜单中选择File–>New–>Project from Existing Sources...
    - 选择解压后的项目文件夹，点击OK
    - 点击Import project from external model并选择Maven，点击Next   到底为止。
    - 若你的环境有多个版本的JDK，注意到选择Java SDK的时候请选择Java 7以上的版本  

## 项目结构解析

```
.
├── demo.iml
├── HELP.md
├── mvnw
├── mvnw.cmd
├── pom.xml
└── src

```

src目录:

```
.
├── main
│   ├── java        ==> 程序位置
│   └── resources   ==> 配置资源文件
└── test
    └── java    ==> 测试文件

```

## 引入Ｗｅｂ模块

当前的`pom.xml`内容如下，仅引入了两个模块:

- `spring-boot-starter`：核心模块，包括自动配置支持、日志和YAML

- `spring-boot-starter-test`：测试模块，包括JUnit、Hamcrest、Mockito

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```
