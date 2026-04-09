# Rule Repository

这是一个集中管理各种开发规范和配置规则的仓库，方便在不同 AI 编码工具中引用和复用。

## 📁 目录结构

```
rule-repo/
├── cursor/                      # 规则文件（适用于 Cursor / Codex / Copilot）
│   ├── .cursorrules             # Cursor 主配置文件
│   ├── JAVA_CODE_GUIDE.md       # Java 代码规范
│   ├── GIT_COMMIT_GUIDE.md      # Git 提交规范
│   ├── JAVA_TEST_GUIDE.md       # Java 测试规范
│   └── MYSQL_GUIDE.md           # MySQL 数据库规范
└── README.md
```

---

## 🚀 各工具使用指南

### 一、Cursor

Cursor 通过项目根目录的 `.cursorrules` 文件加载规则，AI 助手会自动遵循其中的编码规范。

#### 方式一：直接引用 GitHub 文件（推荐）

在项目根目录创建 `.cursorrules` 文件，写入以下内容：

```
@https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/.cursorrules
```

Cursor 会在每次对话时自动拉取最新规则，无需手动维护。

#### 方式二：下载到本地

```bash
curl -o .cursorrules https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/.cursorrules
```

#### 方式三：Git Submodule（团队协作推荐）

```bash
# 添加 submodule
git submodule add https://github.com/haixiangZhang/rule-repo.git .rules

# 创建软链接到项目根目录
ln -s .rules/cursor/.cursorrules .cursorrules
```

> **注意**：`.cursorrules` 文件必须放在**项目根目录**才能被 Cursor 识别。

---

### 二、OpenAI Codex（codex CLI）

Codex CLI 通过 `AGENTS.md` 文件加载项目规范，支持在项目根目录或 `~/.codex/` 全局目录放置说明文件。

#### 方式一：项目级配置（推荐）

在项目根目录创建 `AGENTS.md` 文件，引入本仓库规范：

```markdown
# 项目开发规范

请严格遵循以下规范文档中的所有要求：

## Java 代码规范
https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/JAVA_CODE_GUIDE.md

## Git 提交规范
https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/GIT_COMMIT_GUIDE.md

## MySQL 规范
https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/MYSQL_GUIDE.md

## 测试规范
https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/JAVA_TEST_GUIDE.md
```

#### 方式二：下载规范到本地并引用

```bash
# 在项目根目录创建规范目录
mkdir -p .codex

# 下载规范文件
curl -o .codex/JAVA_CODE_GUIDE.md https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/JAVA_CODE_GUIDE.md
curl -o .codex/GIT_COMMIT_GUIDE.md https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/GIT_COMMIT_GUIDE.md
curl -o .codex/MYSQL_GUIDE.md https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/MYSQL_GUIDE.md
curl -o .codex/JAVA_TEST_GUIDE.md https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/JAVA_TEST_GUIDE.md
```

然后在 `AGENTS.md` 中本地引用：

```markdown
# 项目开发规范

@.codex/JAVA_CODE_GUIDE.md
@.codex/GIT_COMMIT_GUIDE.md
@.codex/MYSQL_GUIDE.md
@.codex/JAVA_TEST_GUIDE.md
```

#### 方式三：全局配置（适用所有项目）

```bash
# 创建全局配置目录
mkdir -p ~/.codex

# 创建全局说明文件
cat > ~/.codex/instructions.md << 'EOF'
# 全局开发规范

请遵循以下 Java 后端开发规范：
- 命名规范、代码格式、注释规范
- Controller / Service / DAO 分层规范
- 异常处理使用 BizException
- 日志规范：使用 SLF4J，禁止 System.out
- Git 提交格式：feat/fix/docs/refactor/test/chore
- SQL 禁止 SELECT *，必须走索引
EOF
```

> **提示**：Codex CLI 会按照 `~/.codex/instructions.md` → 项目根目录 `AGENTS.md` 的顺序合并加载规则，项目级配置优先级更高。

---

### 三、GitHub Copilot

#### 在 VS Code 中使用

GitHub Copilot 在 VS Code 中通过 `.github/copilot-instructions.md` 文件加载自定义规范（需要 Copilot Chat 功能）。

**步骤：**

1. 在项目根目录创建 `.github/copilot-instructions.md` 文件：

```bash
mkdir -p .github
```

2. 写入规范引导内容（建议将核心规范内联进来，Copilot 不支持远程 URL 引用）：

```bash
# 下载规范内容到 copilot-instructions.md
curl -s https://raw.githubusercontent.com/haixiangZhang/rule-repo/main/cursor/JAVA_CODE_GUIDE.md >> .github/copilot-instructions.md
```

或手动创建 `.github/copilot-instructions.md`，内容示例：

```markdown
# 项目开发规范

## 基本原则
- 使用 Java 11+，遵循 Spring Boot 开发规范
- 所有接口必须有 Swagger 注解和入参校验
- 异常统一使用 BizException，禁止直接抛出 RuntimeException
- 日志使用 SLF4J + @Slf4j，禁止 System.out.println
- SQL 禁止 SELECT *，更新必须带 WHERE 条件

## 命名规范
- 类名：UpperCamelCase（如 UserService）
- 方法/变量：lowerCamelCase（如 getUserById）
- 常量：UPPER_SNAKE_CASE（如 MAX_PAGE_SIZE）
- 数据库字段：snake_case（如 user_name）

## Git 提交格式
type(scope): subject
类型：feat / fix / docs / refactor / test / chore
```

3. 在 VS Code 设置中开启自定义指令（`settings.json`）：

```json
{
  "github.copilot.chat.codeGeneration.useInstructionFiles": true
}
```

> **注意**：此功能需要 VS Code 版本 ≥ 1.90 且安装了 GitHub Copilot Chat 扩展。

#### 在 IntelliJ IDEA 中使用

IDEA 插件版 Copilot 暂不支持自动加载 `.github/copilot-instructions.md`，但可以通过以下方式让 Copilot Chat 遵循规范：

**方式一：在 Copilot Chat 对话开头手动引入规范（临时生效）**

在 IDEA 的 Copilot Chat 窗口中，对话开始时粘贴以下 prompt：

```
请在本次对话中严格遵循以下开发规范：
1. Java 命名：类名 UpperCamelCase，方法/变量 lowerCamelCase，常量 UPPER_SNAKE_CASE
2. 异常处理：业务异常使用 BizException，禁止直接抛出 RuntimeException
3. 日志：使用 @Slf4j + SLF4J，禁止 System.out
4. SQL：禁止 SELECT *，UPDATE/DELETE 必须带 WHERE，禁止在循环中执行 SQL
5. 接口：Controller 必须有 @ApiOperation 注解，入参必须有 @Validated 校验
6. Git 提交：遵循 feat/fix/docs/refactor/test/chore 格式
完整规范参见：https://github.com/haixiangZhang/rule-repo
```

**方式二：创建 Live Template 快速注入规范（推荐）**

在 IDEA 中配置代码模板，快速插入规范 prompt：

1. 打开 `Settings` → `Editor` → `Live Templates`
2. 新建模板，缩写设为 `copilot-rule`
3. 内容填入规范 prompt（同方式一）
4. 在 Copilot Chat 输入框中输入 `copilot-rule` + Tab 即可快速展开

**方式三：通过 `.editorconfig` 约束代码风格（被动生效）**

在项目根目录创建 `.editorconfig`，Copilot 会参考此文件生成风格一致的代码：

```ini
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 4
end_of_line = lf
trim_trailing_whitespace = true
insert_final_newline = true

[*.java]
indent_size = 4

[*.{yml,yaml}]
indent_size = 2
```

---

## 📖 规则文件说明

| 文件 | 说明 |
|------|------|
| `cursor/.cursorrules` | AI 助手核心配置，涵盖 Java 开发全套规范 |
| `cursor/JAVA_CODE_GUIDE.md` | Java 代码规范（命名、接口、分页、异常、日志等） |
| `cursor/GIT_COMMIT_GUIDE.md` | Git 提交规范（格式、分支策略、工作流） |
| `cursor/JAVA_TEST_GUIDE.md` | Java 测试规范（单元测试、集成测试） |
| `cursor/MYSQL_GUIDE.md` | MySQL 规范（表设计、索引、SQL 优化） |

---

## 🎯 适用场景

- Spring Boot / Spring Cloud 项目
- MyBatis / MyBatis-Plus 项目
- 微服务架构项目
- RESTful API 项目
- Dubbo 分布式服务项目

**技术栈**: Java 11+, Spring Boot, MyBatis, MySQL, Redis, Dubbo, Maven/Gradle

---

## 💡 使用建议

| 场景 | 推荐方式 |
|------|--------|
| 个人 Cursor 项目 | 方式一：直接引用 GitHub URL |
| 团队 Cursor 项目 | 方式三：Git Submodule |
| Codex CLI 项目 | 项目根目录创建 `AGENTS.md` |
| VS Code + Copilot | `.github/copilot-instructions.md` |
| IDEA + Copilot | Live Template 快速注入 prompt |

---

## 🔄 更新规则

### 使用 Submodule 时

```bash
cd .rules
git pull origin main
cd ..
git add .rules
git commit -m "chore: 更新开发规范"
```

### 直接引用时

Cursor 和 Codex 直接引用远程 URL 的方式会自动获取最新规则，无需手动更新。

---

## 📝 贡献指南

欢迎提交 Issue 或 Pull Request 来改进规则！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/improve-rules`)
3. 提交更改 (`git commit -m 'docs: 改进 Java 命名规范'`)
4. 推送到分支 (`git push origin feature/improve-rules`)
5. 创建 Pull Request

---

## 📄 许可证

MIT License

## 🙋 问题反馈

如有问题或建议，请提交 [Issue](https://github.com/haixiangZhang/rule-repo/issues)
