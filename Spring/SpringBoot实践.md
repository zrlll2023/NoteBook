
```
├── controller # 控制层：负责接收前端请求，返回数据 
├── service # 业务逻辑层接口：定义业务规矩 
│      └── impl # 业务逻辑层实现类：真正写业务代码的地方 
├── mapper # 数据持久层：跟数据库打交道（MyBatis/MP 的地方） 
├── entity # 实体类包：对应数据库里的表结构 
└── dto # 数据传输对象包：前端传进来的数据（输入） 
└── vo # 视图对象包：返回给前端看的数据（输出）
```

#### 在controller包中：

```java
@RestController
@RequestMapping("/api/user")
public class UserController {

    @Autowired
    private UserService userService;

    @PostMapping("/register")
    public Object register(@RequestBody @Valid UserRegisterDTO dto) {
        // 业务逻辑后面写
        return null;
    }
}
```

其中的：
1：@RestController其实是两个注解合体：
	- @Controller → 告诉 Spring 这是一个控制器 Bean
	- @ResponseBody → 方法返回值自动转成 JSON 返回给前端
2：@RequestMapping("/api/user")：
	- 这是这个 Controller 里**所有接口**的公共前缀，所以注册接口完整地址是：localhost:8080/api/user/register
3：@PostMapping("/register")为什么用 POST 而不是 GET？：
	- GET → 获取数据，比如查文章列表
	- POST → 提交数据，比如注册、登录
	- 注册要把用户名密码提交给后端，所以用 POST
4：@RequestBody：
	- @RequestBody 的作用就是把这段 JSON 自动转换成 UserRegisterDTO 对象
	- 前端发请求的时候，用户名和密码是放在请求体里的（JSON 格式）：
```json
{"username": "zhangsan", "password": "123456"}
```
5：@Valid：
	- 作用是**触发校验**——没有它，你在 DTO 上写的 `@NotBlank`、`@Size` 都不会生效，加了它 Spring 才会去执行那些校验规则

---
#### 在entity包中：
@Data //用作 getter 和 setter
@TableName("users") //对应users表
@TableId(type = IdType.AUTO) //告诉 MyBatis-Plus 这个字段是主键，且自动递增

---

#### 在ServiceImpl包中：

```java
// 第一步：检查用户名是否已存在  
User existUser = this.lambdaQuery()  
        .eq(User::getUsername, dto.getUsername())  
        .one();
```

`.one()` 的返回值是什么？
- 如果数据库里**找到了**这个用户名 → 返回一个 `User` 对象
- 如果数据库里**没有**这个用户名 → 返回 `null`

