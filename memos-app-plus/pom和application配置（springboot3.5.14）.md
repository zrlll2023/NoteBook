#### MySQL配置
```
<!-- MySQL依赖 -->  
<dependency>  
    <groupId>com.mysql</groupId>  
    <artifactId>mysql-connector-j</artifactId>  
    <scope>runtime</scope>  
</dependency>
```
然后在application.yml：
```
spring:  
  datasource:  
    url: jdbc:mysql://127.0.0.1:3306/memosplus_db?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai  
    username: root  
    password: root  
    driver-class-name: com.mysql.cj.jdbc.Driver
```
#### mybatis-plus配置
springboot3.5.13开始就要用这个依赖了
```
<!-- mybatis-plus依赖 -->  
<dependency>  
    <groupId>com.baomidou</groupId>  
    <artifactId>mybatis-plus-spring-boot4-starter</artifactId>  
    <version>3.5.15</version>  
</dependency>
```
#### Redis配置
```
<!-- Redis依赖 -->
<dependency>
	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
然后在application.yml：
```
spring:
  data:
    redis:
      host: 127.0.0.1
      port: 6379
```
// properties 格式:
```
spring.data.redis.host=127.0.0.1
spring.data.redis.port=6379
```
#### JWT配置
```
<!-- JWT依赖 -->
<dependency>
    <groupId>com.auth0</groupId>
    <artifactId>java-jwt</artifactId>
    <version>4.4.0</version>
</dependency>
```
#### Knife4j配置
```
<!-- Knife4j依赖 -->
<dependency>
	<groupId>com.github.xiaoymin</groupId>
		<artifactId>knife4j-openapi3-jakarta-spring-boot-starter</artifactId>
	<version>4.4.0</version>
</dependency>
```
然后在application.yml：
```
knife4j:
	spring:
		profile: dev 
		open-api:
		version: 3 
```