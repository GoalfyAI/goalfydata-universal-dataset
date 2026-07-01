# Claude Code 快速开始

3 分钟完成安装，让 Claude Code 帮你构建实时数据资产。

---

## 第 1 步 — 获取 API Token

到 [GoalfyData 控制台](https://goalfydata.ai/settings) 创建 API Key（形如 `gfk_xxx`）。

明文仅在创建时显示一次，请妥善保存。

## 第 2 步 — 安装 uds-cli

uds-cli 用于数据面操作（执行 SQL、导入数据、查看表结构）。

macOS / Linux:
```bash
curl -fsSL https://goalfyagent-public.s3.amazonaws.com/dataset-uds/install.sh | sh
source ~/.zshrc  # or source ~/.bashrc
uds-cli login --token gfk_你的token --api-url https://api.goalfydata.ai
```

Windows (PowerShell):
```powershell
irm https://goalfyagent-public.s3.amazonaws.com/dataset-uds/install.ps1 | iex
uds-cli login --token gfk_你的token --api-url https://api.goalfydata.ai
```

## 第 3 步 — 安装插件

### 推荐：通过 marketplace 安装

marketplace 安装会自动处理插件结构、MCP 配置和 Skill 加载，无需手动复制文件。

```bash
claude plugin marketplace add GoalfyAI/goalfydata
claude plugin install goalfydata@goalfydata
```

### 备选 A：下载 ZIP

下载 [goalfydata-claude-code.zip](https://github.com/GoalfyAI/goalfydata/raw/main/claude-code/goalfydata-claude-code.zip)，解压并复制到插件目录：

```bash
unzip goalfydata-claude-code.zip -d ~/.claude/skills/goalfydata
```

### 备选 B：Git clone

> **注意：必须复制整个 `claude-code/` 目录，不是只复制 `skills/` 子目录。** 缺少 `.claude-plugin/` 或 `.mcp.json` 会导致 MCP 无法加载。

```bash
git clone https://github.com/GoalfyAI/goalfydata.git
cp -r goalfydata/claude-code ~/.claude/skills/goalfydata
```

## 第 4 步 — 配置 Token

在 `~/.claude/settings.json` 的 `env` 中添加你的 Token：

```json
{
  "env": {
    "GOALFY_UDS_API_TOKEN": "gfk_你的token"
  }
}
```

> 这一步必须做，否则 MCP 连接会失败。从桌面应用或 IDE 启动 Claude Code 时不会读取 shell 环境变量，只能通过 settings.json 配置。

## 第 5 步 — 重启 Claude Code

完全退出并重新打开 Claude Code，让插件和 MCP 生效。

## 第 6 步 — 验证

在 Claude Code 中输入 `/mcp`，确认 `goalfydata-mcp` 状态为 connected + 20 tools。

如果显示失败：
- 确认 `~/.claude/settings.json` 中 `GOALFY_UDS_API_TOKEN` 已配置
- 确认 token 是有效的 `gfk_` 前缀
- 完全退出 Claude Code 重新启动

## 开始使用

验证通过后，直接告诉 Claude Code 你想做什么：

### 从文件创建数据集

```
帮我把这个 Excel 文件创建成一个数据集
```

### 从 API 拉取数据并定时同步

```
创建一个电商数据集，包含 3 张表：
- products：从 https://dummyjson.com/products 拉取
- users：从 https://dummyjson.com/users 拉取
- orders：从 https://dummyjson.com/carts 拉取
配置每天凌晨 2 点自动同步。
```

### 查询和分析已有数据集

```
列出我的数据集
```

```
帮我分析订单表的趋势，按月统计销售额
```

### 开发数据应用

```
基于这个电商数据集，帮我开发一个仪表盘应用并部署到公网
```

### 分享数据集

```
把这个数据集分享给 xxx@example.com
```

---

## 常见问题

### MCP 显示 Error / 未连接

1. 检查 `~/.claude/settings.json` 中是否有 `GOALFY_UDS_API_TOKEN`
2. 确认 token 有效（到控制台验证）
3. 完全退出并重启 Claude Code

### uds-cli 命令找不到

安装后需要重新打开终端（或 `source ~/.zshrc`），让 PATH 生效。

### 插件安装失败 "source type not supported"

执行 `claude plugin marketplace update goalfydata` 更新缓存后重试。

---

## 更新

### 插件更新

**marketplace 安装**：marketplace 插件在启动时自动检查更新。手动更新：

```bash
claude plugin update goalfydata@goalfydata
```

**手动安装**：重新下载最新 [ZIP](https://github.com/GoalfyAI/goalfydata/raw/main/claude-code/goalfydata-claude-code.zip) 并覆盖：

```bash
unzip -o goalfydata-claude-code.zip -d ~/.claude/skills/goalfydata
```

更新后执行 `/reload-plugins` 或重启 Claude Code。

### uds-cli 更新

```bash
uds-cli self-update
```

---

## 下一步

- [核心概念](./concepts.zh-CN.md) — 理解 Build / Run / Share 架构
- [完整 SKILL 文档](../claude-code/skills/goalfydata/SKILL.md) — 详细的工具和执行流程
- [常见问题](../FAQ.zh-CN.md) — 更多问题解答
