#### IOC:
用一个例子来理解。

---
假设你开一家餐厅，需要一个厨师：

**没有 IOC 的方式：**

```java
// 餐厅自己去找厨师、培训厨师
厨师 chef = new 厨师();
chef.做菜();
```

**有 IOC 的方式：**

```java
// 餐厅只说「我需要一个厨师」
// 劳务公司（Spring）自动把厨师派过来
@Autowired
厨师 chef;  // Spring 自动注入，不用 new
```

---

IOC 的全称是 **控制反转**——

原来是**你自己**控制对象的创建（`new 厨师()`），现在把这个控制权**反转**给 Spring，让 Spring 来创建和管理对象。

Spring 管理的这些对象叫做 **Bean**。

---

所以 `@Service` 的作用就是：

> 告诉 Spring「这个类是一个 Bean，请你来管理它」。

Spring 启动的时候会扫描所有加了 `@Service`、`@Controller`、`@Mapper` 等注解的类，把它们都纳入管理——需要用的时候直接注入，不用自己 `new`。

---

现在明白了吗？`@Service` 就是在跟 Spring 说「我要被你管理」。

那 `@Mapper` 和 `@Controller` 是不是也是同样的道理？

#### Bean：

继续用劳务公司的比喻：

> **Bean 就是劳务公司登记在册的员工。**

每一个被 Spring 管理的对象，都叫做 Bean。

- 加了 `@Service` → 这个类的对象被 Spring 创建并登记 → 它就是一个 Bean
- 加了 `@Mapper` → 同上
- 加了 `@Controller` → 同上

你需要用某个 Bean 的时候，加 `@Autowired`，Spring 就从「员工名册」里找到它，直接给你用。

---

一句话总结：

> **Bean = 被 Spring 管理的对象。**

记住这一句就够了，以后面试被问到 IOC，就说：

> 「IOC 是控制反转，把对象的创建和管理交给 Spring，这些被 Spring 管理的对象叫 Bean，需要用的时候通过 @Autowired 注入。」

#### AOP: