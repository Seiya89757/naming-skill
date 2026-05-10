# 中文起名顾问 · Chinese Baby Naming Skill

> A Claude Code Skill for generating Chinese personal names with bazi (eight-character) analysis, family-tradition constraints, parent aspirations, and **regional dialect homophone scanning** — the last being something virtually no naming app does.

> 一个 Claude Code Skill：综合**八字五行 + 家族字辈 + 父母期望 + 地域方言谐音**四个维度为孩子起中文名。最大差异化点是**方言谐音扫描** — 99% 的起名 app 不查这件事，但孩子被叫一辈子的是方言不是字典。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.3.0-green.svg)](CHANGELOG.md)
[![Skill Type](https://img.shields.io/badge/Claude%20Code-Skill-orange)](https://docs.claude.com/en/docs/claude-code/skills)

---

## ✨ 这个 Skill 解决什么问题

中国家长起名的真实痛点不是"想不出好字"，是这些：

1. **多约束冲突**：八字要补五行、家族要遵字辈、父母要意境、地域要避谐音 — 一般工具只解一个，把其他 3 个甩给你
2. **方言谐音盲区**：起名 app 普通话扫一遍就完事，但孩子要在粤语区/闽南/潮汕长大，"诗婷"在粤语近"尸亭"才是真坑
3. **家庭意见冲突**：起名从来不是一个人决定，夫妻 / 双方父母 / 爷爷奶奶各有诉求，没工具帮你梳理冲突 + 给沟通话术
4. **信息复用摩擦**：每次找新工具都要重新输入八字、字辈、籍贯 — 信息没法跨工具复用

本 skill 针对每一条都做了设计。

---

## 🎯 三种使用模式

### 1. 快速模式（30 秒找方向）

只要给：**姓氏 + 性别 + 一句期望**

例如："姓陈，女孩，希望温和坚韧、有书卷气"

输出 5 个覆盖不同气质方向的候选 + Top 1 推荐 + 仅参考免责声明。

### 2. 完整模式（正式定名）

引导式分批问 5-12 项信息（姓名、出生时间、出生地、字辈、家族避讳、方言、期望等），输出：

- 联网双源校验的八字推算（默认扶抑 + 调候派）
- 6-8 个完整候选（每个含字义/出处/五行/字辈/期望对应/方言检查/读感/隐患八字段）
- Top 3 排名 + 必出 #1 推荐
- 工作量量化总结（过了 N 候选 / M 方言层 / K 个避讳约束）
- 约束清单导出（下次直接粘贴复用）
- 分享卡片（紧凑表格 + 单候选深度卡片两种格式）

### 3. 协商模式（家庭意见冲突）

当夫妻 / 双方父母诉求不一时，专门处理：

- 区分**硬约束**（必须满足，否则关系破裂）vs **软偏好**（争取一下能让步）
- 输出 3 类候选：**公约数候选** / **让 A 方让步候选** / **让 B 方让步候选**
- 提供**可直接使用的家庭沟通话术**（如"如果想说服奶奶接受这个候选，可以这样讲：..."）
- 诚实点出无解情况（不强行撮合）

这是普通起名 app 完全做不到的差异化。

---

## 📐 四个维度

### 1. 八字五行
- 联网双源校验日柱（差一天五行就全变，不允许模型硬猜）
- 默认流派：扶抑 + 调候。用户可切换其他流派
- 模型推算结果**强烈建议命理师复核**

### 2. 家族传承
- 字辈作为硬约束
- 兄姐协调度测试（候选名跟兄姐名字放一起念）
- 三代以内避讳重字
- 父母同辈字辈冲突规则

### 3. 父母期望
- 引导用户用具体形容词而非抽象大词
- 典故出处可加分但不强求

### 4. 地域方言发音 ⚠️ 杀手锏
- 三层过滤：普通话 → 父/母方言 + 生活地方言 → 跨方言降权扫描
- 13 种方言深度雷区库（[references/dialect-pitfalls.md](references/dialect-pitfalls.md)）
- 不熟方言**主动承认能力边界，建议求证**

---

## 🚀 安装

### 用户级（所有项目可用，推荐）

```bash
git clone https://github.com/Seiya89757/naming-skill.git ~/.claude/skills/chinese-baby-naming
```

或一行装（不需要 git）：

```bash
mkdir -p ~/.claude/skills/chinese-baby-naming && \
curl -sL https://github.com/Seiya89757/naming-skill/archive/main.tar.gz | \
tar -xz --strip-components=1 -C ~/.claude/skills/chinese-baby-naming
```

### 项目级（只在某项目可用）

```bash
mkdir -p /path/to/project/.claude/skills
git clone https://github.com/Seiya89757/naming-skill.git /path/to/project/.claude/skills/chinese-baby-naming
```

### 卸载

```bash
rm -rf ~/.claude/skills/chinese-baby-naming
```

---

## 💡 使用示例

新开 claude 会话，直接说：

```
我家娃下个月出生，姓林，男孩，想取个名字
```

或

```
姓陈，女孩，想要温和有书卷气的名字
```

或

```
夫妻起名意见不一，我老婆要传统的"诗""雅"字，我妈要字辈"昭"
```

Skill 会按场景自动选模式开始问你。

---

## ⚠️ 免责声明（重要）

这个 skill 是 AI 起名**辅助工具**，不是命理决断工具。请理解：

1. **八字推算可能不准** — 模型推算的日柱和喜用神**强烈建议命理师过一遍**
2. **方言扫描有覆盖度差异** — 粤语 / 闽南语 / 吴语主流方言较准；潮汕话 / 客家话 / 温州话 / 晋语等小众方言低置信度，**必须向当地长辈求证**
3. **生肖宜忌不强加** — 用户提则采纳，不主动施加（这套主流命理界争议大）
4. **本 skill 不替代真人** — 起名最终决定要你和家人念出来感觉对了才算

详见 [LICENSE](LICENSE) 中的免责条款。

---

## 🛣️ 开发路线图

- [ ] **v1.4**：兄弟姐妹组合优化（接住"老大老二老三都要协调"场景）
- [ ] **v1.5**：起名故事生成（给家族保存的"为什么取这个名"完整文档）
- [ ] **v2.0**：包成 Claude Code Plugin，支持 `claude plugin install` 一键安装
- [ ] **未来**：网红字数据库自动每年更新

欢迎提 issue 或 PR 加方言雷区库 / 修网红字标签 / 加流派支持。

---

## 🤝 贡献

写这个 skill 缘起自己的需求。感叹现在"科技改变玄学"的节奏 —— 推荐的起名大师也开始用 AI。那咱们就结合得更紧密一些，直接搞一个更适合中国宝宝起名的 skill：融合主流子平派资料、兼顾当前父母期望和偏好、分析时代热词避免过于重复。最重要的是，会**结合普通话和方言读音**，防止出现宝宝有一个读音怪异的名字。

第一个发布版本可能会有遗漏，有意见 or 建议期待反馈：

- **方言问题**：例如某个方言的母语者，看了 [references/dialect-pitfalls.md](references/dialect-pitfalls.md) 觉得漏了什么
- **专业问题**：例如命理师 / 国学爱好者，觉得我的处理逻辑有专业问题
- **体验问题**：例如自己用了 skill 之后想吐槽哪个步骤别扭

直接 issue 或 PR 就好。我会尽量回，但不保证每条都能立刻处理（还要带娃、打工，期望理解）。

提 issue 时帮我标一下你觉得的优先级：

- 🔴 **可能影响真实孩子的事** — 比如方言谐音漏报错报、八字推算流程明显错误
- 🟡 **能改但不急** — UX 改进、新场景需求、文档可以更清楚的地方
- 🟢 **闲聊性质** — 错别字、想讨论某个起名哲学问题、单纯想分享你给娃起名的故事

闲聊探讨也欢迎，中国宝宝的名字是个很有意思的话题。一个时代有一个时代的印记，希望各位的宝宝们健康快乐成长、平安顺利一生。

> 发善愿、行好事、有前程

---

## 📦 文件结构

```
chinese-baby-naming/
├── SKILL.md                      # 主文档（600 行）
├── LICENSE                       # MIT + 起名场景特殊免责
├── README.md                     # 本文件
├── CHANGELOG.md                  # 版本历史
└── references/                   # 按需加载的参考文件
    ├── dialect-pitfalls.md       # 13 种方言深度雷区
    └── avoid-trendy-chars.md     # 时代标签字数据库
```

---

## 📜 License

MIT — 详见 [LICENSE](LICENSE)。

允许商用、修改、二次分发，唯一要求是保留原作者署名。

---

## 🙏 鸣谢

- 命理流派部分参考自主流子平派资料综合
- 方言雷区库初版来自网上公开方言资料
- 这个 skill 的协商模式是被宝妈提醒出来的 —— 宝宝的名字代表全家希望，不是一个人拍脑袋的事情
- 最感谢的还是宝宝妈妈。孕育灵魂和生命（生娃）真是宇宙里最伟大和神奇的事情。

---

## 📬 联系

- **Issues**：[GitHub Issues](https://github.com/Seiya89757/naming-skill/issues) — 优先这里，公开讨论可能对大家有帮助
- **想私聊**：chihexyw@gmail.com

> 名字是孩子接收的第一个礼物。慢慢来，我们一起想好。
