# Quick Cognition v2

> ⚠️ **半成品**——核心机制已可用，报告质量仍在迭代中。欢迎 Issue 讨论。

对具体技术/概念建立有事实溯源的认知地图。

输入一个具体技术/概念/工具/方法/算法/协议/框架/模型，输出一份 HTML 报告，包含 4 维结构（历史/结构/功能/本质）+ 横纵交汇 + 回到本质。

## 🎯 适用场景

| ✅ 适用 | ❌ 不适用 |
|--------|----------|
| 想深入了解一个具体技术（如 Docker、Transformer、RAG）| 简单查询（"X 是什么"）→ 直接问 |
| 想深入理解一个抽象概念（如 自由、爱、熵、正义、美）|  |
| 想对比多个相似事物（如 PostgreSQL vs MySQL、Vue vs React）|  |

> 💡 本 skill 的目标是**能认识任何事物**——具体技术用 4 维结构，抽象概念自动路由到 essay 模式生成散文认知，对比研究走多维对照分析。

## 🚀 快速开始

### 触发词

对 Claude 说：
- 「帮我认知一下 XX」（XX 是具体技术）
- 「了解一下 XX」
- 「深度研究 XX」

### 示例

> 「帮我认知一下 RAG」

Claude 会自动：
1. 识别为概念/技术模式 → 加载 `modes/concept.md`
2. 联网搜索 5+ 次
3. 填双层预收集卡（A 段事实 + B 段推断）
4. 生成 8000+ 字的 HTML 报告
5. 用浏览器自动打开

## 📦 安装

### 方式 1：从 GitHub 安装（推荐）

```bash
claude plugin install https://github.com/Foggy-liu/quickCG
```

### 方式 2：从 .skill 包安装

1. 下载最新 [Release](https://github.com/Foggy-liu/quickCG/releases) 的 `.skill` 文件
2. 解压到 Claude Code skills 目录：

```bash
# Windows 全局
Expand-Archive -Path "quick-cognition-v2.skill" -DestinationPath "C:\Users\Liu\.claude\skills\quick-cognition-v2" -Force

# Mac/Linux 全局
mkdir -p ~/.claude/skills/quick-cognition-v2
unzip quick-cognition-v2.skill -d ~/.claude/skills/quick-cognition-v2
```

## 🏗️ 项目结构

```
quickCG/
├── SKILL.md            # 路由器（Claude 加载入口）
├── README.md           # 本文件（GitHub 主页）
├── DEVELOPER.md        # 开发者文档（迭代历史、设计原则）
├── LICENSE             # MIT 许可证
├── modes/              # 4 个模式文件
│   ├── concept.md      # 默认模式（技术/概念）
│   ├── event.md        # 事件/现象
│   ├── person.md       # 人物/公司
│   └── abstract.md     # 抽象概念引导
└── templates/
    └── report.html     # HTML 报告模板
```

## 🎨 核心机制：双层预收集卡

为防止 AI "凭印象写"导致事实错误，**写报告前必须先填双层卡**：

```markdown
### A. 事实地基（必须可追溯，标 [N]）
| # | 类型 | 拟用事实 | 来源 [N] | 可信度 |
|---|------|---------|---------|--------|
| 1 | 数字 | 28.4 BLEU | [1] | [✓ 可靠] |
| 2 | 日期 | 2017-06-12 论文提交 | [1] | [✓ 可靠] |

### B. 推断上层（基于 A 段，标"推断"无需 [N]）
| # | 拟写推断 | 引用的事实（来自 A 段）|
|---|---------|---------------------|
| 1 | "Transformer 是范式重构而非更好模型" | 引用 A-#1 + A-#2 |
```

**规则**：
- A 段事实必须有 `[N]` 来源；不确定的标 `[? 未知]`
- B 段推断必须引用 A 段事实编号；不能含具体数字/日期/人名
- B 段占总字数 ≤ 50%

详见 `SKILL.md` 第二步.5。

## 📊 质检报告（5 个硬关卡）

报告末尾必须包含：

- [ ] 联网搜索次数 ≥ 5
- [ ] ≥ 1 处 `[? 未知]` 标签
- [ ] AI 味词 grep ≤ 3
- [ ] ≥ 3 条来源 URL
- [ ] 报告末尾有"质检报告"小节

## 📝 v2.4.3 起：AI 生成免责声明

每份报告自动包含：
> 📝 本报告由 AI 辅助生成，**仅供参考**。涉及具体事实、数字、版本号、日期等信息，请以原始来源为准。

## 🤝 贡献

欢迎 Issue 和 PR！这是个人项目但希望保持开放讨论。

主要讨论方向：
- 报告质量的评估标准
- 新模式（如企业架构、开源项目评估）
- 双层卡机制的改进

## 📜 许可证

MIT — 详见 [LICENSE](LICENSE) 文件。

## 🙏 灵感来源

本 skill 在设计时**深度借鉴**了以下项目，感谢老师的参考和启发：

- **[quick-cognition（v1，原版）](https://github.com/)** — 单 SKILL.md 版本，本 skill 是其模块化重构（按事物类型分发到专属 mode）
- **[hv-analysis](https://github.com/)** — 多事物对比研究，启发了本 skill 的多维对照分析维度
- **[khazix-writer](https://github.com/)** — 散文写作，启发了本 skill 抽象概念模式的 essay 风格

如果你熟悉这些 skill，会发现本 skill 吸收了它们的设计精华，但走的是**单一入口、按类型分发**的路线——一套 skill 覆盖所有事物类型，而不是按类型切分多个 skill。
