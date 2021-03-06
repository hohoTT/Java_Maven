# Java_Maven

## 用于JAVA的MAVEN练习

## 以下介绍的为 MAVEN 工程的基本目录结构

	src 
		-main
			-java
				-package
		-test
			-java
				-package
		resources
		
	groupId 就是项目的包名
	artifactId 是模块名



## MAVEN 中的常用命令

----  maven 中常用到的命令

mvn -v				查看 maven 版本
	compile			编译
	test			测试
	package			打包
	
	clean			删除 target
	install 		安装 jar 包到本地仓库中
	
	创建目录的两种方式：
		1. archetype:generate		自动安装搭建maven的项目结构骨架，但是之后要输入一些有关 pom.xml 中的内容
		
		2. archetype:generate -DgroupId=com.wt.mavenAutoCreate 			组织名，公司网址的反写+项目名
							  -DartifactId=mavenAutoCreate-service 		项目名-模块名
							  -Dversion=1.0.0-SNAPSHOT 					版本号
							  -Dpackage=com.wt.mavenAutoCreate			代码所存在的包

archetype 插件
	用于创建符合 maven 规定的目录结构 
	
	
	坐标
		构件
	
	仓库
		本地仓库和远程仓库
		
	镜像仓库
	
	
配置 -Dmaven.multiModuleProjectDirectory=$M2_HOME  注意此时的 JDK 版本需要设置为1.7的版本，1.8的版本会报错 


## MAVEN 工程依赖部分的讲述

依赖的第一部分讲解：
maven-a、maven-b、maven-c  三个项目的一开关系为：

1. maven-a 依赖于 maven-b
2. maven-c 依赖于maven-a

所以 
3. maven-c 依赖于 maven-b


依赖的第二部分讲解：（越接近依赖与哪一个）
c - >  a - > b
2.0   2.0   2.4

maven-b 中使用的版本为 2.4
maven-a 中使用的版本为 2.0
因为maven-c离maven-a近，所以版本为2.0
maven-c 中使用的版本为 2.0


依赖的第三部分讲解：（距离相同时，依赖与加载的顺序，先加载先依赖）


依赖的继承：
实现maven项目中的依赖继承关系，创建一个父maven项目maven-parent，使得maven-b继承与maven-parent，实现代码的复用


## 创建maven的web项目工程所出现的错误

1. Could not calculate build plan: Plugin 

解决方法 \org\apache\maven\plugins目录下的文件夹全部删除，重新下载。


2. Failure to transfer org.codehaus.plexus:plexus-archiver:jar:

解决方法 网址 -----    http://blog.csdn.net/gao36951/article/details/46491405
plexus相关jar包


## 使用  tomcat  作为maven的服务器容器

第一种方式

<build>
	<finalName>maven-webDemo</finalName>

	<plugins>
		<!-- 以下为嵌入Tomcat服务器   -->
		<plugin>
			<groupId>org.apache.tomcat.maven</groupId>
			<artifactId>tomcat7-maven-plugin</artifactId>
			<version>2.1</version>
			<configuration>
				<port>8080</port>
				<path>/maven-webDemo</path>
				<uriEncoding>UTF-8</uriEncoding>
				<finalName>maven-webDemo</finalName>
				<server>tomcat7</server>
			</configuration>
			
			<!-- 以下的配置为在打包成功后使用tomcat:run来运行tomcat服务 -->
			<executions>
				<execution>
					<phase>package</phase>
					<goals>
						<goal>run</goal>
					</goals>
				</execution>
			</executions>
		</plugin>

	</plugins>
</build>



第二种方式


<build>
	<finalName>maven-webDemo</finalName>

	<plugins>

		<!-- 以下为嵌入Tomcat服务器 -->
		<plugin>
			<groupId>org.apache.tomcat.maven</groupId>
			<artifactId>tomcat7-maven-plugin</artifactId>
			<version>2.2</version>

			<!-- 以下的配置为在打包成功后使用tomcat:run来运行tomcat服务 -->
			<executions>
				<execution>
					<phase>package</phase>
					<goals>
						<goal>run</goal>
					</goals>
				</execution>
			</executions>
		</plugin>

	</plugins>
</build>


## maven 创建的web工程需要修改 web.xml中的 servlet的版本

修改 maven web 工程默认的jdk版本

<profile>
	
	  <id>jdk-1.7</id>

	  <activation>

			 <activeByDefault>true</activeByDefault>

			 <jdk>1.7</jdk>

	  </activation>

	  <properties>

			 <maven.compiler.source>1.7</maven.compiler.source>

			 <maven.compiler.target>1.7</maven.compiler.target>

			 <maven.compiler.compilerVersion>1.7</maven.compiler.compilerVersion>

	  </properties>

</profile>


## maven 配置文件中修改仓库的位置，修改为英国的仓库

<mirror>

  <id>UK</id>

  <name>UK Central</name>

  <url>http://uk.maven.org/maven2</url>

  <mirrorOf>central</mirrorOf>

</mirror>

