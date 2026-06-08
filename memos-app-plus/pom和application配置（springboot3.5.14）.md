#### MySQL配置
```xml
<!-- MySQL依赖 -->  
<dependency>  
    <groupId>com.mysql</groupId>  
    <artifactId>mysql-connector-j</artifactId>  
    <scope>runtime</scope>  
</dependency>
```
然后在application.yml：
```yml
spring:  
  datasource:  
    url: jdbc:mysql://127.0.0.1:3306/memosplus_db?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai  
    username: root  
    password: root  
    driver-class-name: com.mysql.cj.jdbc.Driver
```
#### mybatis-plus配置
springboot3.5.13开始就要用这个依赖了
```xml
<!-- mybatis-plus依赖 -->  
<dependency>  
    <groupId>com.baomidou</groupId>  
    <artifactId>mybatis-plus-spring-boot4-starter</artifactId>  
    <version>3.5.15</version>  
</dependency>
```
#### Redis配置
```xml
<!-- Redis依赖 -->
<dependency>
	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
然后在application.yml：
```yml
spring:
  data:
    redis:
      host: 127.0.0.1
      port: 6379
```
// properties 格式:
```properties
spring.data.redis.host=127.0.0.1
spring.data.redis.port=6379
```
#### JWT配置
```xml
<!-- JWT依赖 -->
<dependency>
    <groupId>com.auth0</groupId>
    <artifactId>java-jwt</artifactId>
    <version>4.4.0</version>
</dependency>
```
#### Knife4j配置
```xml
<!-- Knife4j依赖 -->
<dependency>
	<groupId>com.github.xiaoymin</groupId>
		<artifactId>knife4j-openapi3-jakarta-spring-boot-starter</artifactId>
	<version>4.4.0</version>
</dependency>
```
然后在application.yml：
```yml
knife4j:
	spring:
		profile: dev 
		open-api:
		version: 3 
```
#### 独立的 BCrypt 库
```xml
<!--    其实 BCrypt 不一定非要引入整个 Security，
		所以可以引入独立的 BCrypt 库，不依赖 Spring Security          -->
<dependency>  
    <groupId>org.mindrot</groupId>  
    <artifactId>jbcrypt</artifactId>  
    <version>0.4</version>  
</dependency>
```

