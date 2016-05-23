---
layout:     post
title:      "Eclipse 中 Maven 整合 querydsl"
subtitle:   "spring data JPA 更高级的用法"
date:       2016-05-22
author:     "ZhangBilly"
header-img: "img/in-post/querydsl/jean-cocteau-museum-menton.png"
tags:
    - querydsl
    - Eclipse
---



# Eclipse 中 Maven 整合 querydsl

## 引入依赖


	<dependency>
	  <groupId>com.querydsl</groupId>
	  <artifactId>querydsl-apt</artifactId>
	  <version>${querydsl.version}</version>
	  <scope>provided</scope>
	</dependency>
	
	<dependency>
	  <groupId>com.querydsl</groupId>
	  <artifactId>querydsl-jpa</artifactId>
	  <version>${querydsl.version}</version>
	</dependency>


从4.0后groupId从com.mysema.querydsl变为了com.queryds

## 引入maven插件


	<project>
	  <build>
	  <plugins>
	    ...
	    <plugin>
	      <groupId>com.mysema.maven</groupId>
	      <artifactId>apt-maven-plugin</artifactId>
	      <version>1.1.3</version>
	      <executions>
	        <execution>
	          <goals>
	            <goal>process</goal>
	          </goals>
	          <configuration>
	            <outputDirectory>target/generated-sources/java</outputDirectory>
	            <processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
	          </configuration>
	        </execution>
	      </executions>
	    </plugin>
	    ...
	  </plugins>
	  </build>
	</project>


但是如果是在eclipse中，需要改为


	<plugin>
		<groupId>com.mysema.maven</groupId>
		<artifactId>apt-maven-plugin</artifactId>
		<version>1.1.3</version>
		<executions>
			<execution>
				<goals>
					<goal>process</goal>
				</goals>
				<configuration>
					<outputDirectory>target/generated-sources/java</outputDirectory>
					<processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
				</configuration>
			</execution>
		</executions>
		<dependencies>
			<dependency>
				<groupId>com.querydsl</groupId>
				<artifactId>querydsl-apt</artifactId>
				<version>${querydsl.version}</version>
			</dependency>
			<dependency>
				<groupId>com.querydsl</groupId>
				<artifactId>querydsl-jpa</artifactId>
				<classifier>apt</classifier>
				<version>${querydsl.version}</version>
			</dependency>
		</dependencies>
	</plugin>


### 参考

[querydsl 官方文档](http://www.querydsl.com/static/querydsl/latest/reference/html/ch02.html#jpa_integration)

[apt-maven-plugin 插件说明](https://github.com/querydsl/apt-maven-plugin/wiki/m2e-usage)





