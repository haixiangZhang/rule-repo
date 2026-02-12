# Cursor Rules

这个目录包含了 Cursor AI 助手的配置规则，专为 Java 后端开发优化。

## 📁 文件说明

- **`.cursorrules`**: Cursor 主配置文件（放在项目根目录使用）
- **`JAVA_CODE_GUIDE.md`**: Java 代码规范详细文档（✨ 已优化）
- **`GIT_COMMIT_GUIDE.md`**: Git 提交规范详细文档
- **`JAVA_TEST_GUIDE.md`**: Java 测试规范详细文档
- **`MYSQL_GUIDE.md`**: MySQL 数据库规范详细文档

## 🚀 快速开始

### 在 Cursor 中使用

#### 方法 1: 直接引用（推荐）

在你的项目根目录创建 `.cursorrules` 文件：

```
@https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/.cursorrules
```

#### 方法 2: 下载使用

```bash
curl -o .cursorrules https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/.cursorrules
```

#### 方法 3: 复制内容

直接复制 `.cursorrules` 文件内容到你的项目根目录的 `.cursorrules` 文件中。

## 📖 规范内容

### Java 代码规范 (JAVA_CODE_GUIDE.md)

#### 基础规范
- ✅ **命名规范**: 包、类、方法、变量、常量、枚举
- ✅ **代码格式**: 缩进、空行、行长度、大括号
- ✅ **注释规范**: 类注释、方法注释、字段注释、复杂逻辑注释

#### 接口层面规范 ⭐
- ✅ **Controller 规范**: 注解使用、接口文档
- ✅ **URL 命名规范**: RESTful 路径设计
- ✅ **参数验证规范**: @Validated、业务校验
- ✅ **RO/VO 规范**: 请求对象和返回对象设计
- ✅ **认证鉴权规范**: @ApiCode 配置
- ✅ **数据安全规范**: 加密传输、字段权限控制

#### 分页规范 ⭐
- ✅ **分页参数注解**: @PageableDefault、@MaxPageSize
- ✅ **分页常量定义**: PAGE_SIZE_1K、PAGE_SIZE_2K
- ✅ **分页返回规范**: PageResponse 包装
- ✅ **分页场景使用**: 人员查询、组织查询、ID查询

#### 异常处理规范 ⭐
- ✅ **异常抛出规范**: BizException 使用
- ✅ **错误码配置**: message.properties
- ✅ **常见业务异常**: 参数校验、权限认证
- ✅ **统一异常处理**: @RestControllerAdvice
- ✅ **返回值规范**: JsonResponse、PageResponse

#### 高级规范
- ✅ **类和方法设计**: 单一职责、Dubbo 接口规范
- ✅ **集合使用**: 初始化、遍历、并发集合
- ✅ **并发编程**: 线程安全、线程池、分布式锁
- ✅ **数据库操作**: SQL 编写、分页查询、批量操作、事务管理
- ✅ **日志规范**: 日志级别、日志格式、Controller 日志
- ✅ **安全编码**: SQL 注入防护、XSS 防护、密码加密
- ✅ **性能优化**: 空指针处理、对象创建、字符串拼接
- ✅ **工具推荐**: Lombok、Hutool

### Git 提交规范 (GIT_COMMIT_GUIDE.md)
- ✅ Commit Message 格式
- ✅ 分支管理策略
- ✅ 代码审查要求

### 测试规范 (JAVA_TEST_GUIDE.md)
- ✅ 单元测试规范
- ✅ 集成测试规范
- ✅ 测试用例设计

### 数据库规范 (MYSQL_GUIDE.md)
- ✅ 表设计规范
- ✅ 索引使用规范
- ✅ SQL 优化建议

## 🎯 适用项目

- Spring Boot / Spring Cloud 项目
- MyBatis / MyBatis-Plus 项目
- RESTful API 项目
- 微服务架构项目
- Dubbo 分布式服务项目

## 💡 使用提示

1. 将 `.cursorrules` 放在**项目根目录**
2. Cursor 会自动识别并应用这些规则
3. AI 助手会按照规范生成和审查代码
4. 查看具体规范文档了解详细要求

## 📚 详细文档

### 核心规范文档

| 文档 | 说明 | 更新时间 |
|------|------|----------|
| [JAVA_CODE_GUIDE.md](./JAVA_CODE_GUIDE.md) | Java 代码规范（接口、分页、异常处理等） | 2026-02-12 ✨ 已优化 |
| [GIT_COMMIT_GUIDE.md](./GIT_COMMIT_GUIDE.md) | Git 提交规范 | - |
| [JAVA_TEST_GUIDE.md](./JAVA_TEST_GUIDE.md) | Java 测试规范 | - |
| [MYSQL_GUIDE.md](./MYSQL_GUIDE.md) | MySQL 数据库规范 | - |

### 规范亮点

#### 接口层面规范
从实际项目 `open-basic` 模块提取的最佳实践：
- 完整的 Controller 注解配置
- RESTful URL 设计规范（下划线命名）
- 参数验证和业务校验结合
- 字段权限控制和数据加密

#### 分页规范
明确的分页场景使用规则：
- 人员查询：最大 1000 条
- 组织/岗位查询：最大 2000 条
- 批量 GET 接口：最大 200 条

#### 异常处理规范
统一的异常处理机制：
- BizException 业务异常
- 错误码国际化配置
- 敏感信息保护
- 统一异常拦截

## 🔄 更新日志

### 2026-02-12
- ✨ 重构 JAVA_CODE_GUIDE.md，优化章节结构
- ✨ 新增接口层面规范（Controller、URL、参数验证、RO/VO）
- ✨ 新增分页规范（分页参数、常量定义、场景使用）
- ✨ 新增异常处理规范（BizException、错误码、统一处理）
- ✨ 新增 Dubbo 接口规范
- ✨ 新增 Controller 日志规范
- 🐛 修复格式问题和代码块缩进

## 🤝 贡献

欢迎提交 Issue 或 Pull Request 来改进这些规范。

## 📞 联系

如有问题或建议，请通过以下方式联系：
- 提交 Issue
- Pull Request

---

**技术栈**: Java 11+, Spring Boot, MyBatis, MySQL, Redis, Dubbo, Maven/Gradle

**最后更新**: 2026-02-12
