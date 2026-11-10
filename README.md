# Ops 技术笔记

面向 Linux、Docker、Kubernetes 与 DevOps 的学习笔记。仓库配置了两个 Cursor 工作流：**笔记体例优化（Command）** 与 **自动提交推送（Skill）**。

请在 Cursor 中打开本仓库**根目录**（含 `.cursor/` 的那一层）。只打开子目录时，Command / Skill 可能不会出现。

## 目录结构

```text
Ops/
├── README.md
├── Linux/                   # 系统使用与运维基础
├── Docker/                  # 镜像、容器与编排入门
├── k8s/                     # Kubernetes
├── DevOps/                  # 协作与交付实践（含 CI/CD）
├── .cursor/
│   ├── commands/
│   │   └── optimize-note.md # 笔记体例优化
│   └── skills/
│       └── auto-commit/     # 自动提交并推送
└── .gitignore
```

建议阅读顺序：`Linux` → `Docker` → `k8s` → `DevOps`。各目录笔记待补充，写完后把条目加到下面对应表格。

### Linux

系统使用、文件与权限、进程、网络与常用运维操作。

| # | 笔记 |
|---|------|
|   |      |

### Docker

镜像、容器、网络、数据卷，以及 Compose 等编排入门。

| # | 笔记 |
|---|------|
|   |      |

### k8s

集群、工作负载、服务发现、配置与存储。

| # | 笔记 |
|---|------|
|   |      |

### DevOps

协作与持续交付实践。CI/CD 归在本目录，不放在 Docker。

| # | 笔记 |
|---|------|
|   |      |

---

## 1. 笔记体例优化（Command）

| 项 | 说明 |
|----|------|
| 类型 | Cursor **Command**（不是 Skill / Rule） |
| 文件 | `.cursor/commands/optimize-note.md` |
| 聊天触发 | `/optimize-note` |

### 做什么

优化指定笔记的体例与代码格式，并修正明确写错的内容：

- **不删代码与配图**；缺代码则停止，不凭记忆补写
- **书面语**：正文与结论去掉「吃」「收」等口语，改为规范术语
- **结构**：章节之间不用单独的 `---`；标题不带序号；文首不用一级标题，先写引言再分节
- **缩进为 2 空格**，去掉 Tab；正文与代码块内连续空行最多 1 个
- 围栏语言标签写准确；易错点用 `> **说明：**` 写在代码块外
- 可纠错、补本篇已涉及的缺口、调整段落位置；不换大纲、不扩成另一篇

### 怎么用

1. 打开 Agent / Chat
2. 输入 `/`，选择 `optimize-note`
3. `@` 要优化的笔记后回车，例如：

```text
/optimize-note @Linux/01. 文件与权限.md
```

可一次多个：

```text
/optimize-note @Docker/01. 镜像与容器.md @k8s/01. Pod.md
```

Agent 会**直接改文件**，不只输出 Diff。

### 改规范

编辑 `.cursor/commands/optimize-note.md`，保存后下次 `/optimize-note` 即生效。

---

## 2. 自动提交并推送（Skill）

| 项 | 说明 |
|----|------|
| 类型 | Cursor **Skill** |
| 文件 | `.cursor/skills/auto-commit/SKILL.md` |
| 触发话术 | `提交` / `commit` / `自动提交` / `帮我提交` |

### 做什么

用户明确要求提交时，Agent 会：

1. 查看 `git status` / `diff` / 近期 commit 风格
2. 按 **Conventional Commits** 起草中文说明并 `commit`
3. **默认 `git push` 到 `origin`**（首次分支用 `git push -u origin HEAD`）
4. 回报 commit message、涉及文件、push 结果

未明确要求提交时，**不会**自动 commit / push。

### Commit message 格式

```text
<type>(<scope>): <中文简述>

<可选正文：1～2 句说明 why，中文>
```

常用 `type`：

| type | 用途 |
|------|------|
| `docs` | 笔记、说明、示例（本仓库默认） |
| `fix` | 纠正错误内容或错误示例 |
| `refactor` | 结构调整、体例统一 |
| `chore` | `.cursor`、`.gitignore` 等配置 |
| `feat` | 新增一整篇笔记或新主题 |

`scope` 与目录对应：`linux`、`docker`、`k8s`、`devops`。

### 推送规则

- 提交成功后**默认 push**，不必再单独说 push
- 说「只提交不推送 / 不要 push」时跳过 push
- 不 force push；不改 git config；不提交 `.env` 等密钥文件

### 改行为

编辑 `.cursor/skills/auto-commit/SKILL.md` 即可。
