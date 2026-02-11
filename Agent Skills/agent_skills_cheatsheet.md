# 🚀 Agent Skills 速查表（Cheat Sheet）

> 快速查阅，5分钟上手

---

## 📋 核心概念（30秒理解）

```
┌─────────────────────────────────────────────────────────────┐
│  Agent Skills = AI的"工作说明书"                             │
│  MCP = AI的"工具箱"                                         │
├─────────────────────────────────────────────────────────────┤
│  比喻：                                                       │
│  - Skills = 菜谱（宫保鸡丁怎么做）                            │
│  - MCP = 厨具（锅、刀、炉灶）                                 │
│  - Agent = 厨师                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 🛠️ 安装Skills（1分钟上手）

### 方法1：npx skills（推荐⭐）

```bash
# 安装Vercel官方Skills
npx skills add vercel-labs/agent-skills

# 安装特定Skill
npx skills add 仓库地址 --skill skill名称

# 全局安装（所有项目可用）
npx skills add 仓库地址 -g

# 列出可用Skills
npx skills add 仓库地址 --list
```

### 方法2：add-skill（自动检测）

```bash
npx add-skill 仓库地址
```

### 方法3：手动安装

```bash
# 1. 克隆
git clone https://github.com/用户/仓库.git

# 2. 复制到Cursor目录
cp -r 仓库/skills/* ~/.cursor/skills/
# 或项目级
cp -r 仓库/skills/* .cursor/skills/
```

---

## 📁 Skills目录结构

```
技能名称/
├── SKILL.md           ← 必须！核心文件
├── scripts/           ← 可选：脚本
├── templates/         ← 可选：模板
└── resources/         ← 可选：资源
```

### 存放位置

| 范围 | Cursor路径 | Antigravity路径 |
|------|-----------|-----------------|
| 全局（所有项目） | `~/.cursor/skills/` | `~/.antigravity/skills/` |
| 项目级（当前项目） | `.cursor/skills/` | `.antigravity/skills/` |

**注意**：`~` = 用户主目录
- Windows: `C:\Users\用户名\`
- Mac/Linux: `~/`

---

## 📝 SKILL.md模板

```markdown
---
name: skill名称
description: 简短描述
---

# Skill标题

## 使用场景
什么时候使用这个Skill

## 步骤
1. 第一步
2. 第二步
3. 第三步

## 示例
```代码示例```

## 注意事项
- 注意点1
- 注意点2
```

---

## 🎯 常用Skills推荐（按场景）

### 🚀 开发类

| Skill | 用途 | 安装命令 |
|-------|------|----------|
| **Vercel官方** | 全栈开发 | `npx skills add vercel-labs/agent-skills` |
| **代码审查** | 自动Code Review | `npx skills add coderabbitai/skills` |
| **前端设计** | UI/UX规范 | `npx skills add anthropic/skills/frontend-design` |
| **Python开发** | Python最佳实践 | `npx skills add anthropic/skills/python` |

### 📱 移动端

| Skill | 用途 | 安装命令 |
|-------|------|----------|
| **Flutter** | Flutter开发 | `npx skills add awesome-flutter/skills` |
| **React Native** | RN开发 | `npx skills add vercel-labs/agent-skills:react-native` |

### 🎨 设计/内容

| Skill | 用途 | 安装命令 |
|-------|------|----------|
| **营销专家** | 营销文案 | `npx skills add coreyhaines31/marketingskills` |
| **内容创作** | 内容生成 | `npx skills add nicepkg/ai-workflow/workflows/content-creator-workflow` |
| **Product Hunt** | PH发布 | `npx skills add yoanbernabeu/producthunt-skills` |

### 🔧 DevOps

| Skill | 用途 | 安装命令 |
|-------|------|----------|
| **Docker** | 容器化 | `npx skills add devops-skills/docker` |
| **AWS部署** | AWS部署 | `npx skills add vercel-labs/agent-skills:aws` |

---

## 🔍 Skills市场

| 平台 | 网址 | 特点 |
|------|------|------|
| **skills.sh** | [skills.sh](https://skills.sh) | Vercel官方，可搜索 |
| **SkillzWave** | [skillzwave.ai](https://skillzwave.ai) | 44,000+ Skills |
| **GitHub** | github.com搜索`agent-skills` | 开源社区 |

---

## 🖥️ 平台支持

| 平台 | 支持状态 | 特点 |
|------|----------|------|
| **Cursor** | ✅ 完全支持 | 推荐，IDE体验好 |
| **Antigravity** | ✅ 完全支持 | 免费，多Agent |
| **Claude Code** | ✅ 原生支持 | 官方出品 |
| **GitHub Copilot** | ✅ 支持 | VS Code集成 |
| **Windsurf** | ✅ 支持 | 免费额度多 |
| **OpenAI Codex** | ✅ 支持 | OpenAI官方 |

---

## ⚡ 快速命令

```bash
# 安装CLI工具
npm install -g agent-skills-cli

# 搜索Skills
skills search react
skills search flutter
skills search -i    # 交互式

# 安装Skills
skills install skill名称

# 检查已安装
skills check

# 更新Skills
skills update --all

# 移除Skills
skills remove skill名称
```

---

## 🎮 使用技巧

### 自动触发
只需描述需求，AI自动选择Skill：
```
"创建一个Flutter登录页"
→ AI自动使用flutter skill
```

### 手动触发
```
/skill名称

# 或
"使用skill名称做xxx"
```

### 组合使用
```
"使用flutter-architecture skill创建首页，
 并用code-review skill审查代码"
```

---

## ⚠️ 安全提醒

| ❌ 不要做 | ✅ 应该做 |
|-----------|-----------|
| 安装来源不明的Skill | 只安装官方/知名社区Skill |
| 在Skill中硬编码密钥 | 使用环境变量 |
| 盲目运行scripts | 先审查脚本内容 |
| 安装过多Skill | 按需安装，精简使用 |

---

## 🔧 故障排除

| 问题 | 解决 |
|------|------|
| Skill不生效 | 重启Cursor/Antigravity |
| 找不到Skill | 检查目录结构（必须SKILL.md） |
| 权限错误 | `chmod +x scripts/*.sh` |
| 中文乱码 | 保存为UTF-8编码 |
| 未加载 | Settings中检查是否禁用 |

---

## 📊 Skills vs MCP 对比

| | Skills | MCP |
|--|--------|-----|
| **是什么** | 工作说明书 | 工具接口 |
| **格式** | Markdown | Server |
| **解决** | 怎么做 | 怎么连 |
| **举例** | 代码规范 | 文件系统、数据库 |
| **Token** | 低 | 高 |
| **最佳** | **两者结合使用** | |

---

## 🚀 5分钟快速开始

```bash
# 1. 确认Cursor/Antigravity已安装

# 2. 安装第一个Skill
npx skills add vercel-labs/agent-skills

# 3. 重启Cursor

# 4. 测试
# 在Chat中输入："创建一个React组件"

# 5. 创建自己的Skill
mkdir -p ~/.cursor/skills/my-style
cat > ~/.cursor/skills/my-style/SKILL.md << 'EOF'
---
name: my-style
description: 我的代码风格
---

# 我的代码规范

## 要求
1. 使用TypeScript
2. 函数式组件
3. 使用Tailwind CSS

## 示例
```tsx
const MyComponent: React.FC = () => {
  return <div className="p-4">Hello</div>;
};
```
EOF

# 6. 测试自己的Skill
# 在Chat中输入："使用my-style skill创建一个按钮组件"
```

---

## 📚 更多资源

- **官方文档**: cursor.com/docs/context/skills
- **Skills市场**: skills.sh
- **精选列表**: github.com/JackyST0/awesome-agent-skills
- **免费Skills**: github.com/chirag2653/free-ai-agent-skills

---

**💡 记住**: Skills让AI按你的规范工作，一次编写，永久复用！

**Happy Coding!** 🎉
