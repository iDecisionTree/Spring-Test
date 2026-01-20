# Spring-Test

### 题目1：简单的接口 - 输出"Hello, Spring Boot!"
#### 题目描述
实现一个简单的接口。当通过`GET`请求访问`/api/hello`时，接口直接返回纯文本 `Hello, Spring Boot!`。
#### 具体要求
1. 克隆本仓库；
2. 编写`Controller`层和`Service`层代码；
3. 接口路径：`/api/hello`；
4. 请求方式：`GET`；
5. 仅需返回固定字符串；
6. 项目结构和变量名需符合规范。

---

### 题目2：实现用户登录接口
#### 题目描述
实现一个用户登录接口。当通过`Post`请求携带`Json表单`的用户名和密码参数访问`/api/user/login`时，接口查询数据库中的用户信息完成验证，并返回对应的登录结果提示。
#### 具体要求
1. 克隆本仓库；
1. 数据库：配置数据库连接；
2. 实体层（Entity）：直接粘贴以下User类到entity文件夹下；
```java
package com.gjyyk.springtest.entity;

import jakarta.persistence.*;
import lombok.Data;

@Data
@Entity
@Table(name = "user")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private long id;  // 用户 Id

    @Column(nullable = false, unique = true)
    private String username;  // 用户名

    @Column(nullable = false)
    private String password;  // 密码

}
```
3. 数据访问层（Repository）：编写JPA Repository接口，提供“根据用户名查询用户”的自定义方法；
4. 业务层（Service）：封装登录核心逻辑（查询用户是否存在 → 验证密码是否正确），返回对应提示；
5. 控制层（Controller）：编写`POST`类型的登录接口，接收`JSON表单`的用户名和密码参数，调用Service完成验证；
6. 接口路径：`/api/user/login`；
7. 请求方式：`POST`；
8. 返回规则：
   - 用户名不存在 → 返回“用户不存在”；
   - 密码不匹配 → 返回“密码不正确”；
   - 验证通过 → 返回“登录成功”。

#### 数据库内容
目前数据库已有的数据为：
| username | password |
| ---- | ---- |
| 张三 | 12345678 |
| Peter | asdfghjkl |

#### 测试用例
输入：
```json
{
    "username": "张三",
    "password": "12345678"
}
```
输出：
```
登录成功
```
\
输入：
```json
{
    "username": "李四",
    "password": "12345678"
}
```
输出：
```
用户不存在
```
\
输入：
```json
{
    "username": "Peter",
    "password": "abcdefgh"
}
```
输出：
```
密码错误
```

---

### 注意
1. 每道题分别克隆仓库，答题结束后分别打包，不要向本仓库提交代码；
2. 第二题可以适度使用AI工具辅助，要理解写下的每一行代码；
3. 使用`postman`等工具辅助调试接口；
4. SpringBoot项目默认端口为`8080`;
5. 传入Json表单时需确保请求头中的`Content-Type`为`application/json`；
6. 本仓库代码使用`Gradle`构建系统，项目配置文件为`application.properties`，不同构建系统和配置文件间有差异。
