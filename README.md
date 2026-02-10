# Rule Repository

这是一个集中管理各种开发规范和配置规则的仓库，方便在不同项目中引用和复用。

## 📁 目录结构

```
rule-repo/
├── cursor/              # Cursor AI 助手规则
│   ├── .cursorrules     # Cursor 主配置文件
│   ├── GIT_COMMIT_GUIDE.md      # Git 提交规范
│   └── JAVA_CODE_GUIDE.md       # Java 代码规范
└── README.md
```

## 🚀 Cursor 规则使用指南

### 方式一：直接引用 GitHub 文件（推荐）

在你的项目根目录创建 `.cursorrules` 文件，内容如下：

```
# 引用远程规则文件
@https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/.cursorrules
```

### 方式二：下载到本地

```bash
# 下载 .cursorrules 文件到项目根目录
curl -o .cursorrules https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/.cursorrules
```

### 方式三：Git Submodule（团队协作推荐）

```bash
# 在项目根目录添加 submodule
git submodule add https://github.com/haixiangZhang/rule-repo.git .rules

# 创建软链接
ln -s .rules/cursor/.cursorrules .cursorrules
```

## 📖 规则文件说明

### Cursor 目录

#### `.cursorrules`
Cursor AI 助手的核心配置文件，包含：
- Java 后端开发规范
- Spring Boot 项目最佳实践
- 代码质量要求（命名、注释、结构）
- 异常处理和日志规范
- 数据库操作规范
- 安全编码要求
- Git 提交规范
- 测试规范

#### `GIT_COMMIT_GUIDE.md`
详细的 Git 提交规范文档，包含：
- Commit Message 标准格式
- 提交类型说明（feat/fix/docs/refactor等）
- 分支管理策略
- Git 工作流程
- 完整示例和最佳实践

#### `JAVA_CODE_GUIDE.md`
完整的 Java 代码规范手册，包含：
- 命名规范（包/类/方法/变量/常量）
- 代码格式和结构
- 注释规范
- 异常处理
- 集合使用
- 并发编程
- 数据库操作
- 日志规范
- 安全编码
- 性能优化

## 🎯 适用场景

### Java 后端开发项目
- Spring Boot / Spring Cloud 项目
- MyBatis / MyBatis-Plus 项目
- 微服务架构项目
- RESTful API 项目

### 技术栈
- **框架**: Spring Boot, Spring Cloud, MyBatis
- **构建工具**: Maven, Gradle
- **数据库**: MySQL, Redis, MongoDB
- **消息队列**: RabbitMQ, Kafka
- **JDK**: Java 11+

## 💡 使用建议

1. **个人项目**: 使用方式一或方式二，快速应用规范
2. **团队项目**: 使用方式三（Submodule），保持团队规范统一
3. **定制化**: Fork 本仓库后根据团队需求调整规则

## 🔄 更新规则

### 本地更新（使用 Submodule 时）

```bash
# 进入 submodule 目录
cd .rules

# 拉取最新规则
git pull origin main

# 回到项目根目录
cd ..

# 提交 submodule 更新
git add .rules
git commit -m "chore: 更新开发规范"
```

### 直接引用更新

如果使用方式一（直接引用），Cursor 会自动获取最新规则，无需手动更新。

## 📝 贡献指南

欢迎提交 Issue 或 Pull Request 来改进规则！

### 贡献流程

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/improve-rules`)
3. 提交更改 (`git commit -m 'docs: 改进 Java 命名规范'`)
4. 推送到分支 (`git push origin feature/improve-rules`)
5. 创建 Pull Request

## 📄 许可证

MIT License

## 🙋 问题反馈

如有问题或建议，请提交 [Issue](https://github.com/haixiangZhang/rule-repo/issues)

---

**注意**: `.cursorrules` 文件需要放在项目根目录才能被 Cursor 识别。
