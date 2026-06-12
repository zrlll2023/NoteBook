MyBatis-Plus > 通用 Service 层 > IService<T> 接口
IService<T> 是 MyBatis-Plus 在 BaseMapper 之上封装的 Service层接口,内置了单表的增删改查、批量操作、分页等通用方法,泛型 T 是你的实体类。
BaseMapper是贴着数据库的那层(insert/selectById),IService是包在外面给业务用的那层(save/getById),后者内部其实就是调前者。你的两个空文件之所以能直接用,就是因为它们分别接上了这两条继承链

`IService` 是 **MyBatis-Plus 提供的一个通用 Service 接口**，里面封装了大量常用的 CRUD 方法，让你不用自己写增删改查。

|层|作用|
|---|---|
|BaseMapper|直接操作数据库|
|IService|给业务层提供通用 CRUD|
|ServiceImpl|实现 IService|
|Controller|调用 Service|

