---
title: spring-boot集成spring-session
category: spring
date: 2016-03-11
---
只需如下三步，就可利用redis实现分布式session。


1. 修改pom.xml，添加依赖：

	```
	<dependency>
	        <groupId>org.springframework.session</groupId>
	        <artifactId>spring-session</artifactId>
	</dependency>
	<dependency>
	        <groupId>org.springframework.boot</groupId>
	        <artifactId>spring-boot-starter-redis</artifactId>
	</dependency>
	```
2. 添加配置：

	```
	spring.redis.host=localhost
	spring.redis.password=yourpassword
	spring.redis.port=6379
	
	```

3. 添加类HttpSessionConfig
	
	```
	
	import org.springframework.session.data.redis.config.annotation.web.http.EnableRedisHttpSession;
	
	@EnableRedisHttpSession
	public class HttpSessionConfig {
	
	}
	```
	
