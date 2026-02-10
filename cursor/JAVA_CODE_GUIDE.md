# Java 代码规范指南

## 目录

1. [命名规范](#命名规范)
2. [代码格式](#代码格式)
3. [注释规范](#注释规范)
4. [类和方法设计](#类和方法设计)
5. [异常处理](#异常处理)
6. [集合使用](#集合使用)
7. [并发编程](#并发编程)
8. [数据库操作](#数据库操作)
9. [日志规范](#日志规范)
10. [安全编码](#安全编码)

---

## 命名规范

### 包名

- 全部小写，使用点分隔
- 避免使用复数形式
- 遵循域名倒序规则

```java
// 推荐
com.company.project.module.service
com.company.project.module.controller

// 不推荐
com.company.project.Module.Service
com.company.project.modules.services
```

### 类名

- 使用 UpperCamelCase（大驼峰）
- 名词或名词短语
- 见名知义

```java
// 推荐
public class UserService { }
public class OrderController { }
public class PaymentServiceImpl { }

// 不推荐
public class userservice { }
public class Order_Controller { }
public class PSImpl { }
```

**特殊类命名规范：**

| 类型 | 命名规则 | 示例 |
|------|---------|------|
| Controller | XxxController | UserController |
| Service 接口 | XxxService | UserService |
| Service 实现 | XxxServiceImpl | UserServiceImpl |
| DAO/Mapper | XxxMapper | UserMapper |
| Entity | Xxx | User, Order |
| DTO | XxxDTO | UserDTO, OrderDTO |
| VO | XxxVO | UserVO, OrderVO |
| 工具类 | XxxUtil 或 XxxUtils | StringUtil, DateUtils |
| 常量类 | XxxConstant | SystemConstant |
| 异常类 | XxxException | BusinessException |
| 配置类 | XxxConfig | RedisConfig |

### 方法名

- 使用 lowerCamelCase（小驼峰）
- 动词或动词短语

```java
// 推荐
public void getUserById(Long id) { }
public boolean isValid() { }
public void calculateTotal() { }

// 不推荐
public void Get_User_By_Id(Long id) { }
public boolean valid() { }
public void total() { }
```

**常用方法命名规范：**

| 方法类型 | 命名规则 | 示例 |
|---------|---------|------|
| 获取单个对象 | getXxx | getUser() |
| 获取多个对象 | listXxx 或 getXxxList | listUsers() |
| 统计 | countXxx | countUsers() |
| 插入 | save 或 insert | saveUser() |
| 删除 | remove 或 delete | removeUser() |
| 修改 | update | updateUser() |
| 判断存在 | exists | existsUser() |
| 布尔判断 | isXxx 或 hasXxx | isValid(), hasPermission() |

### 变量名

- 使用 lowerCamelCase
- 见名知义，避免单字母（除循环变量）
- 布尔变量使用 is/has/can 等前缀

```java
// 推荐
private String userName;
private int pageSize;
private boolean isValid;
private boolean hasPermission;

// 不推荐
private String un;
private int ps;
private boolean valid;
private boolean permission;

// 循环变量可以使用单字母
for (int i = 0; i < list.size(); i++) { }
```

### 常量名

- 全部大写，使用下划线分隔
- 语义清晰

```java
// 推荐
public static final int MAX_PAGE_SIZE = 100;
public static final String DEFAULT_ENCODING = "UTF-8";
private static final long CACHE_EXPIRE_TIME = 3600L;

// 不推荐
public static final int maxPageSize = 100;
public static final String de = "UTF-8";
```

### 枚举

- 类名使用 UpperCamelCase
- 成员名全部大写，使用下划线分隔

```java
// 推荐
public enum OrderStatus {
    PENDING,
    PAID,
    SHIPPED,
    COMPLETED,
    CANCELLED
}

// 不推荐
public enum orderStatus {
    pending,
    Paid,
    shipped
}
```

---

## 代码格式

### 缩进

- 使用 4 个空格缩进，禁止使用 Tab

### 行长度

- 每行不超过 120 个字符
- 超过时使用合理的换行

```java
// 推荐
public void someMethod(String param1, String param2,
                      String param3, String param4) {
    // 方法体
}

// 不推荐
public void someMethod(String param1, String param2, String param3, String param4, String param5, String param6) {
    // 方法体
}
```

### 空行

- 包声明后空一行
- import 分组之间空一行
- 类的成员之间空一行
- 方法之间空一行
- 方法内逻辑块之间空一行

```java
package com.company.project.service;

import java.util.List;
import java.util.Map;

import org.springframework.stereotype.Service;

import com.company.project.entity.User;
import com.company.project.mapper.UserMapper;

@Service
public class UserService {

    private final UserMapper userMapper;

    public UserService(UserMapper userMapper) {
        this.userMapper = userMapper;
    }

    public User getUser(Long id) {
        // 方法实现
    }
}
```

### 类成员顺序

```java
public class UserService {

    // 1. 常量
    private static final int MAX_RETRY_COUNT = 3;

    // 2. 静态变量
    private static UserCache cache;

    // 3. 成员变量
    private final UserMapper userMapper;
    private final RedisTemplate redisTemplate;

    // 4. 构造函数
    public UserService(UserMapper userMapper, RedisTemplate redisTemplate) {
        this.userMapper = userMapper;
        this.redisTemplate = redisTemplate;
    }

    // 5. 静态方法
    public static void clearCache() {
        cache.clear();
    }

    // 6. 公共方法
    public User getUserById(Long id) {
        return userMapper.selectById(id);
    }

    // 7. 受保护方法
    protected void validateUser(User user) {
        // 校验逻辑
    }

    // 8. 私有方法
    private boolean checkPermission(Long userId) {
        return true;
    }

    // 9. Getter/Setter（使用 Lombok 时可省略）
}
```

### 大括号

- 左大括号不换行
- 右大括号换行
- if/else/for/while/do 等语句必须使用大括号

```java
// 推荐
if (condition) {
    doSomething();
}

if (condition) {
    doSomething();
} else {
    doOtherthing();
}

// 不推荐
if (condition) doSomething();

if (condition)
{
    doSomething();
}
```

---

## 注释规范

### 类注释

```java
/**
 * 用户服务实现类
 * <p>
 * 提供用户相关的业务逻辑处理，包括：
 * <ul>
 *     <li>用户注册、登录</li>
 *     <li>用户信息查询、更新</li>
 *     <li>用户权限管理</li>
 * </ul>
 * </p>
 *
 * @author zhangsan
 * @since 2024-01-01
 */
@Service
public class UserServiceImpl implements UserService {
    // 类实现
}
```

### 方法注释

```java
/**
 * 根据用户ID查询用户信息
 * <p>
 * 优先从 Redis 缓存中获取，缓存未命中时查询数据库
 * </p>
 *
 * @param userId 用户ID，不能为 null
 * @return 用户信息，如果用户不存在返回 null
 * @throws IllegalArgumentException 当 userId 为 null 时抛出
 */
public User getUserById(Long userId) {
    if (userId == null) {
        throw new IllegalArgumentException("userId 不能为 null");
    }
    // 实现逻辑
}
```

### 字段注释

```java
public class User {

    /**
     * 用户ID，主键
     */
    private Long id;

    /**
     * 用户名，唯一索引
     */
    private String username;

    /**
     * 用户状态：0-禁用，1-正常，2-锁定
     */
    private Integer status;
}
```

### 复杂逻辑注释

```java
public void processOrder(Order order) {
    // 1. 校验订单状态
    validateOrderStatus(order);

    // 2. 扣减库存（使用分布式锁避免超卖）
    String lockKey = "order:lock:" + order.getProductId();
    try (RedisLock lock = redisLock.acquire(lockKey)) {
        deductStock(order);
    }

    // 3. 创建支付单
    PaymentOrder paymentOrder = createPaymentOrder(order);

    // 4. 发送 MQ 消息通知
    sendOrderMessage(order);
}
```

### 注释原则

1. **必须注释的情况**：
   - 所有的类、接口
   - 所有的公共方法
   - 复杂的业务逻辑
   - 特殊算法或优化
   - 临时方案或 TODO

2. **不需要注释的情况**：
   - 显而易见的代码
   - Getter/Setter 方法（使用 Lombok）

3. **注释质量要求**：
   - 使用中文注释
   - 说明"为什么"而不是"做什么"
   - 保持注释与代码同步
   - 避免废话注释

```java
// 不好的注释
// 循环遍历用户列表
for (User user : users) {
    // ...
}

// 好的注释
// 批量查询用户权限，避免 N+1 查询问题
for (User user : users) {
    // ...
}
```

---

## 类和方法设计

### 单一职责原则

每个类只负责一件事：

```java
// 推荐：职责分离
public class UserService {
    public User getUser(Long id) { }
    public void saveUser(User user) { }
}

public class UserValidator {
    public void validate(User user) { }
}

// 不推荐：职责混乱
public class UserService {
    public User getUser(Long id) { }
    public void saveUser(User user) { }
    public void sendEmail(User user) { }
    public void generateReport() { }
}
```

### dubbo 接口
分页查询接口定义规则：
- 方法签名：BasePageImpl<DTO类型> page(查询DTO queryDTO, Pageable pageable)
- 查询 DTO：包含业务查询条件，实现 Serializable
- 返回类型：BasePageImpl<T>（来自 pupu-plus-starter-constants 包）
- 分页参数：使用 org.springframework.data.domain.Pageable

举例如下：
```java
  import com.pphr.constants.dto.BasePageImpl;
  import org.springframework.data.domain.Pageable;

  public interface ITenantApi {
      /**
       * 分页查询租户列表
       *
       * @param queryDTO 查询条件
       * @param pageable 分页参数
       * @return 分页结果
       */
      BasePageImpl<TenantDTO> page(TenantQueryDTO queryDTO, Pageable pageable);
  }
```
查询参数 DTO：
```java
  import lombok.AllArgsConstructor;
  import lombok.Builder;
  import lombok.Data;
  import lombok.NoArgsConstructor;

  import java.io.Serializable;
  import java.util.List;

  @Data
  @Builder
  @NoArgsConstructor
  @AllArgsConstructor
  public class TenantQueryDTO implements Serializable {

      private static final long serialVersionUID = -1266578365212973258L;

      /**
       * 数据类型（如 VORG）
       */
      private String dataType;

      /**
       * 访问类型（如 USER、INNER_SYSTEM、OUTER_SYSTEM）
       */
      private String accessType;

      /**
       * 访问 ID 集合（支持按多个 accessId 查询）
       */
      private List<String> accessIds;
  }
```
返回结果类型：
- 来自 com.pphr.constants.dto.BasePageImpl（项目依赖：pupu-plus-starter-constants）
- 分页参数使用 Spring Data 的 org.springframework.data.domain.Pageable

### 方法长度

- 单个方法不超过 50 行
- 方法只做一件事
- 复杂逻辑拆分为多个私有方法

```java
// 推荐
public void processOrder(Order order) {
    validateOrder(order);
    deductStock(order);
    createPayment(order);
    sendNotification(order);
}

private void validateOrder(Order order) {
    // 校验逻辑
}

private void deductStock(Order order) {
    // 扣减库存
}

// 不推荐：方法过长
public void processOrder(Order order) {
    // 100+ 行代码混在一起
}
```

### 参数数量

- 方法参数不超过 5 个
- 参数过多时考虑使用对象封装

```java
// 推荐
public void createUser(UserDTO userDTO) {
    // userDTO 包含所有需要的参数
}

// 不推荐
public void createUser(String username, String password, String email,
                      String phone, Integer age, String address) {
    // 参数过多
}
```

### 返回值

- 避免返回 null，使用 Optional 或空集合
- 统一返回格式

```java
// 推荐
public Optional<User> getUserById(Long id) {
    User user = userMapper.selectById(id);
    return Optional.ofNullable(user);
}

public List<User> listUsers() {
    List<User> users = userMapper.selectList();
    return users != null ? users : Collections.emptyList();
}

// 不推荐
public User getUserById(Long id) {
    return userMapper.selectById(id); // 可能返回 null
}
```

---

## 异常处理

### 异常分类

```java
// 业务异常（继承 RuntimeException）
public class BusinessException extends RuntimeException {
    private final String code;

    public BusinessException(String code, String message) {
        super(message);
        this.code = code;
    }
}

// 系统异常
public class SystemException extends RuntimeException {
    public SystemException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

### 异常处理规范

```java
// 推荐：捕获特定异常
try {
    userService.createUser(userDTO);
} catch (DuplicateUserException e) {
    log.warn("用户已存在: {}", userDTO.getUsername(), e);
    throw new BusinessException("USER_EXISTS", "用户已存在");
} catch (DatabaseException e) {
    log.error("数据库操作失败: {}", userDTO, e);
    throw new SystemException("系统异常，请稍后重试", e);
}

// 不推荐：捕获 Exception
try {
    userService.createUser(userDTO);
} catch (Exception e) {
    // 不知道具体什么异常
}

// 不推荐：空 catch 块
try {
    userService.createUser(userDTO);
} catch (Exception e) {
    // 吞掉异常
}
```

### 统一异常处理

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    /**
     * 业务异常
     */
    @ExceptionHandler(BusinessException.class)
    public Result<Void> handleBusinessException(BusinessException e) {
        log.warn("业务异常: {}", e.getMessage());
        return Result.fail(e.getCode(), e.getMessage());
    }

    /**
     * 参数校验异常
     */
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public Result<Void> handleValidException(MethodArgumentNotValidException e) {
        String message = e.getBindingResult().getFieldError().getDefaultMessage();
        return Result.fail("INVALID_PARAM", message);
    }

    /**
     * 系统异常
     */
    @ExceptionHandler(Exception.class)
    public Result<Void> handleException(Exception e) {
        log.error("系统异常", e);
        return Result.fail("SYSTEM_ERROR", "系统异常，请稍后重试");
    }
}
```

### 异常抛出原则

1. 不要捕获后不处理
2. 不要过度使用异常（正常逻辑不用异常）
3. 异常信息要清晰
4. finally 块用于资源释放

```java
// 不推荐：用异常控制流程
try {
    Integer.parseInt(str);
    return true;
} catch (NumberFormatException e) {
    return false;
}

// 推荐：正常逻辑判断
return str.matches("\\d+");
```

---

## 集合使用

### 集合初始化

```java
// 推荐：指定初始容量
List<User> users = new ArrayList<>(100);
Map<Long, User> userMap = new HashMap<>(128);

// 不推荐：使用默认容量（可能导致多次扩容）
List<User> users = new ArrayList<>();
```

### 空集合处理

```java
// 推荐：返回空集合而不是 null
public List<User> listUsers() {
    List<User> users = userMapper.selectList();
    return users != null ? users : Collections.emptyList();
}

// 不推荐
public List<User> listUsers() {
    return userMapper.selectList(); // 可能返回 null
}
```

### 集合遍历

```java
// 推荐：使用增强 for 循环或 Stream
for (User user : users) {
    process(user);
}

users.forEach(this::process);

users.stream()
     .filter(user -> user.getAge() > 18)
     .forEach(this::process);

// 需要索引时使用普通 for 循环
for (int i = 0; i < users.size(); i++) {
    User user = users.get(i);
    // 使用索引
}
```

### 并发集合

```java
// 推荐：并发场景使用并发集合
private final Map<String, User> cache = new ConcurrentHashMap<>();

// 不推荐：并发场景使用普通集合
private final Map<String, User> cache = new HashMap<>(); // 线程不安全
```

---

## 并发编程

### 线程安全

```java
// 推荐：使用线程安全的类
private final AtomicInteger counter = new AtomicInteger(0);
private final ConcurrentHashMap<String, String> map = new ConcurrentHashMap<>();

// 不推荐：使用线程不安全的类
private int counter = 0; // 并发下不安全
private SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd"); // 线程不安全
```

### 线程池使用

```java
// 推荐：使用 ThreadPoolExecutor 自定义线程池
@Configuration
public class ThreadPoolConfig {

    @Bean("taskExecutor")
    public ThreadPoolExecutor taskExecutor() {
        return new ThreadPoolExecutor(
            10,  // 核心线程数
            20,  // 最大线程数
            60L, TimeUnit.SECONDS, // 空闲线程存活时间
            new LinkedBlockingQueue<>(1000), // 任务队列
            new ThreadFactoryBuilder().setNameFormat("task-pool-%d").build(),
            new ThreadPoolExecutor.CallerRunsPolicy() // 拒绝策略
        );
    }
}

// 不推荐：使用 Executors 创建线程池（可能导致 OOM）
ExecutorService executor = Executors.newFixedThreadPool(10);
```

### 锁的使用

```java
// 推荐：使用 Lock 接口
private final ReentrantLock lock = new ReentrantLock();

public void doSomething() {
    lock.lock();
    try {
        // 业务逻辑
    } finally {
        lock.unlock(); // 确保释放锁
    }
}

// 分布式锁
@Service
public class OrderService {

    public void createOrder(Order order) {
        String lockKey = "order:lock:" + order.getProductId();
        RLock lock = redissonClient.getLock(lockKey);

        try {
            if (lock.tryLock(10, 30, TimeUnit.SECONDS)) {
                try {
                    // 业务逻辑
                } finally {
                    lock.unlock();
                }
            } else {
                throw new BusinessException("系统繁忙，请稍后重试");
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            throw new SystemException("获取锁被中断", e);
        }
    }
}
```

---

## 数据库操作

### SQL 编写规范

```java
// 推荐：指定查询字段
@Select("SELECT id, username, email FROM user WHERE id = #{id}")
User selectById(Long id);

// 不推荐：使用 SELECT *
@Select("SELECT * FROM user WHERE id = #{id}")
User selectById(Long id);
```

### 分页查询

```java
// 推荐：使用分页插件
public PageResult<UserVO> pageUsers(UserQuery query) {
    Page<User> page = new Page<>(query.getPageNum(), query.getPageSize());
    IPage<User> userPage = userMapper.selectPage(page, query);

    List<UserVO> userVOs = userPage.getRecords().stream()
        .map(this::convertToVO)
        .collect(Collectors.toList());

    return new PageResult<>(userPage.getTotal(), userVOs);
}
```

### 批量操作

```java
// 推荐：批量插入
public void batchInsert(List<User> users) {
    if (CollectionUtils.isEmpty(users)) {
        return;
    }
    // 分批插入，每批 1000 条
    Lists.partition(users, 1000)
         .forEach(userMapper::batchInsert);
}

// 不推荐：循环单条插入
for (User user : users) {
    userMapper.insert(user); // N 次数据库访问
}
```

### 事务管理

```java
// 推荐：合理使用事务
@Transactional(rollbackFor = Exception.class)
public void createOrder(OrderDTO orderDTO) {
    // 1. 创建订单
    Order order = new Order();
    orderMapper.insert(order);

    // 2. 扣减库存
    productMapper.deductStock(orderDTO.getProductId(), orderDTO.getQuantity());

    // 3. 创建支付单
    paymentMapper.insert(payment);
}

// 注意：事务方法不要包含 RPC 调用或 MQ 发送
```

---

## 日志规范

### 日志级别

```java
@Slf4j
@Service
public class UserService {

    public User getUser(Long id) {
        // ERROR: 系统错误，需要立即处理
        try {
            return userMapper.selectById(id);
        } catch (Exception e) {
            log.error("查询用户失败, userId: {}", id, e);
            throw e;
        }

        // WARN: 警告信息，可能存在问题
        if (user == null) {
            log.warn("用户不存在, userId: {}", id);
        }

        // INFO: 重要业务流程
        log.info("用户登录成功, userId: {}, ip: {}", id, ip);

        // DEBUG: 调试信息（生产环境关闭）
        log.debug("查询用户详情, userId: {}, user: {}", id, user);
    }
}
```

### 日志格式

```java
// 推荐：使用占位符
log.info("用户注册成功, userId: {}, username: {}", userId, username);

// 不推荐：字符串拼接
log.info("用户注册成功, userId: " + userId + ", username: " + username);

// 推荐：记录异常堆栈
log.error("处理订单失败, orderId: {}", orderId, e);

// 不推荐：只记录异常信息
log.error("处理订单失败: " + e.getMessage());
```

### 日志原则

1. 不要在循环中打印日志
2. 生产环境关闭 DEBUG 日志
3. 敏感信息脱敏（密码、手机号等）
4. 日志要包含上下文信息

```java
// 推荐：关键信息脱敏
log.info("用户登录, username: {}, phone: {}",
         username,
         phone.replaceAll("(\\d{3})\\d{4}(\\d{4})", "$1****$2"));

// 不推荐：记录敏感信息
log.info("用户登录, password: {}", password);
```

---

## 安全编码

### SQL 注入防护

```java
// 推荐：使用参数化查询
@Select("SELECT * FROM user WHERE username = #{username}")
User findByUsername(String username);

// 不推荐：字符串拼接
@Select("SELECT * FROM user WHERE username = '" + username + "'")
User findByUsername(String username);
```

### XSS 防护

```java
// 推荐：对输出进行 HTML 转义
public String getUsername() {
    return HtmlUtils.htmlEscape(username);
}
```

### 密码加密

```java
// 推荐：使用 BCrypt
@Service
public class PasswordService {

    private final BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();

    public String encode(String rawPassword) {
        return encoder.encode(rawPassword);
    }

    public boolean matches(String rawPassword, String encodedPassword) {
        return encoder.matches(rawPassword, encodedPassword);
    }
}

// 不推荐：MD5（不安全）
String password = DigestUtils.md5Hex(rawPassword);
```

### 参数校验

```java
// 推荐：使用 Bean Validation
@Data
public class UserDTO {

    @NotBlank(message = "用户名不能为空")
    @Size(min = 3, max = 20, message = "用户名长度为 3-20 个字符")
    private String username;

    @NotBlank(message = "密码不能为空")
    @Pattern(regexp = "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d).{8,}$",
             message = "密码至少 8 位，包含大小写字母和数字")
    private String password;

    @Email(message = "邮箱格式不正确")
    private String email;
}

@PostMapping("/users")
public Result<Void> createUser(@Valid @RequestBody UserDTO userDTO) {
    userService.createUser(userDTO);
    return Result.success();
}
```

---

## 性能优化

### 避免空指针

```java
// 推荐：使用 Optional
public String getUserName(Long userId) {
    return Optional.ofNullable(userMapper.selectById(userId))
                   .map(User::getUsername)
                   .orElse("未知用户");
}

// 推荐：使用工具类
if (StringUtils.isNotBlank(username)) {
    // ...
}

if (CollectionUtils.isNotEmpty(users)) {
    // ...
}
```

### 对象创建

```java
// 推荐：使用 Builder 模式
User user = User.builder()
    .username("zhangsan")
    .email("zhangsan@example.com")
    .age(25)
    .build();

// 推荐：使用对象池（重量级对象）
private static final ObjectPool<Connection> pool = new GenericObjectPool<>(factory);
```

### 字符串拼接

```java
// 推荐：循环中使用 StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
String result = sb.toString();

// 不推荐：循环中使用 +
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i; // 每次都创建新对象
}
```

---

## 工具推荐

### Lombok

```java
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class User {
    private Long id;
    private String username;
    private String email;
}

@Slf4j
@Service
public class UserService {
    // 自动生成 log 字段
}
```

### Hutool

```java
// 集合操作
List<String> list = CollUtil.newArrayList("a", "b", "c");

// 字符串操作
String str = StrUtil.format("Hello {}", "World");

// 日期操作
DateTime now = DateUtil.date();
String dateStr = DateUtil.format(now, "yyyy-MM-dd HH:mm:ss");
```

---

遵循以上规范，编写高质量的 Java 代码！
