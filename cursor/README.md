# Cursor Rules

这个目录包含了 Cursor AI 助手的配置规则，专为 Java 后端开发优化。

## 📁 文件说明

- **`.cursorrules`**: Cursor 主配置文件（放在项目根目录使用）
- **`GIT_COMMIT_GUIDE.md`**: Git 提交规范详细文档
- **`JAVA_CODE_GUIDE.md`**: Java 代码规范详细文档

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

### 代码规范
- ✅ 命名规范（包、类、方法、变量、常量）
- ✅ 代码格式和结构
- ✅ 注释规范
- ✅ 异常处理
- ✅ 日志使用

### 技术规范
- ✅ Spring Boot 最佳实践
- ✅ MyBatis 使用规范
- ✅ 数据库操作规范
- ✅ Redis 缓存使用
- ✅ 并发编程规范

### 安全规范
- ✅ SQL 注入防护
- ✅ XSS 防护
- ✅ 密码加密
- ✅ 参数校验

### Git 规范
- ✅ Commit Message 格式
- ✅ 分支管理策略
- ✅ 代码审查要求

## 🎯 适用项目

- Spring Boot / Spring Cloud 项目
- MyBatis / MyBatis-Plus 项目
- RESTful API 项目
- 微服务架构项目

## 💡 使用提示

1. 将 `.cursorrules` 放在**项目根目录**
2. Cursor 会自动识别并应用这些规则
3. AI 助手会按照规范生成和审查代码

## 📚 扩展阅读

- [Git 提交规范详细文档](./GIT_COMMIT_GUIDE.md)
- [Java 代码规范详细文档](./JAVA_CODE_GUIDE.md)

## 🔄 更新

定期检查本仓库获取最新的规范更新。

---

**技术栈**: Java 11+, Spring Boot, MyBatis, MySQL, Redis, Maven/Gradle
