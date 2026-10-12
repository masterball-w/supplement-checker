<p align="center"><img src="docs/images/banner.png" alt="supplement-checker banner" width="100%"></p>

# supplement-checker · 保健品核查 Agent Skill

拍一张保健品的照片或宣传图，让 AI agent 按固定流程查三件事：

1. **成分功效证据**：动物研究、人体 RCT、Meta 分析，按证据等级分级，并和产品剂量对比
2. **品牌合规与资质**：美国 FDA/DSLD、澳洲 TGA、加拿大 NPN、日本消費者庁、欧盟/英国，以及中国蓝帽子 / 跨境渠道；第三方认证（USP、NSF、Informed Sport 等）到认证方数据库核实
3. **价格对比**：同款多渠道比价，同成分其他品牌按有效日剂量折算，并记录核查时间

最后输出一份每条结论都附来源链接的报告。

> ⚠️ **这是一个研究辅助工具，不是医疗建议，也不是法律意见。** 报告内容取决于检索时能访问到的数据库与网页，可能不完整或已过时。是否服用、服用多少，请咨询医生或药师。

<!-- DEMO VIDEO / GIF PLACEHOLDER：演示视频（B站链接或 docs/images/demo.gif）制作完成后放在这里 -->

## 快速开始

### 1. 安装

```bash
git clone https://github.com/masterball-w/supplement-checker.git

# Cursor（全局）：~/.cursor/skills/；也可放项目内 .cursor/skills/
mkdir -p ~/.cursor/skills && cp -r supplement-checker ~/.cursor/skills/

# Claude Code（全局）：~/.claude/skills/；也可放项目内 .claude/skills/
mkdir -p ~/.claude/skills && cp -r supplement-checker ~/.claude/skills/
```

- 文件夹名保持 `supplement-checker`，与 `SKILL.md` 里的 `name` 一致。
- 其他支持 Agent Skills（`SKILL.md`）的工具：把整个文件夹放进它的 skills 目录。Cursor 也会读取 `.agents/skills/` 和 `~/.claude/skills/`。
- 不支持 Skills 的 agent：把 `docs/skill-plain.txt` 的内容作为系统提示词或项目说明粘贴进去，需要时再把 `references/` 里的文件一起提供给它。

### 2. 使用

agent 需要能读图，并且能联网检索、打开网页。上传一张保健品的商品图或宣传图，然后输入：

```text
帮我查一下这个保健品：成分有没有研究支持、品牌在当地有没有注册、同成分哪里买更划算。
我在中国大陆，主要在京东和天猫买。
```

也可以输入 `/supplement-checker` 显式调用。图片看不清时，agent 会追问品牌、成分表或文号。报告格式见 [`references/report-template.md`](references/report-template.md)，完整示例见下方「示例报告」。

## 工作流程

```mermaid
flowchart TD
    A["📷 用户上传保健品图片<br/>Photo / promo image"] --> B["Step 0 识别产品<br/>品牌·成分·剂量·文号·认证标志"]
    B -->|看不清| B2["追问用户 / 搜索标签文字"]
    B2 --> B
    B --> C["Step 1 功效证据<br/>PubMed · Cochrane · ODS · EFSA · CNKI"]
    B --> D["Step 2 合规资质<br/>FDA/DSLD · TGA · NPN · 消費者庁 · SAMR 蓝帽子 · USP/NSF"]
    B --> E["Step 3 价格对比<br/>官网 · 京东 · 天猫 · 拼多多 · iHerb"]
    C --> C1["核验 PMID / DOI<br/>证据分级 + 剂量对比"]
    D --> D1["官方数据库逐项查询<br/>红旗清单"]
    E --> E1["按有效日剂量折算<br/>记录核查时间"]
    C1 --> F["📄 报告<br/>结论速览 · 三部分 · 来源 · 免责声明"]
    D1 --> F
    E1 --> F
```

<p align="center"><img src="docs/images/workflow.png" alt="workflow" width="90%"></p>

## 设计原则

- **不编造**：引用的每篇文献都要有 PMID / DOI / URL，并且在本次会话中实际访问核验过（PubMed E-utilities、Crossref）。
- **查不到就说查不到**：数据库打不开、需要登录或验证码时，标注"未能核验"并给出查询入口，不猜结果。
- **价格不估算**：每个价格都记录核查时间（含时区）；取不到实时价格时只给搜索链接。
- **结论与证据匹配**：按"结局 + 人群"分级，例如"纠正缺乏：证据强；不缺乏人群预防骨折：证据反对"。
- **区分事实与推断**："数据库未查到记录"不等于"违法"，报告会写明怎么查的。

## 示例报告

[`examples/nature-made-vitamin-d3-1000iu.md`](examples/nature-made-vitamin-d3-1000iu.md)：Nature Made 维生素 D3 1000 IU 软胶囊，核查于 2026-10-10（UTC+8）。

[`examples/ormior-nervonic-acid.md`](examples/ormior-nervonic-acid.md)：ORMIOR「澳大利亚神经酸」（磷脂酰丝氨酸 + 神经酸），核查于 2026-10-12（UTC+8），产地判定为【假洋牌】，证据截图见 [`examples/evidence/ormior/`](examples/evidence/ormior/)。该判定针对品牌产地身份，不涉及成分真伪。

<p align="center"><img src="docs/images/example-report.png" alt="example report screenshot" width="80%"></p>

## 目录结构

```
supplement-checker/
├── SKILL.md                         # Skill 主文件（frontmatter: name + description）
├── references/
│   ├── regulators-by-region.md      # 各地区监管机构与官方查询入口（已逐个访问检查）
│   ├── evidence-grading.md          # 证据来源、核验方法、分级标准、剂量对比
│   ├── price-comparison.md          # 比价渠道、折算公式、真伪风险
│   └── report-template.md           # 报告模板 + 免责声明
├── examples/
│   └── nature-made-vitamin-d3-1000iu.md
├── docs/
│   ├── workflow.mmd                 # Mermaid 源文件
│   ├── skill-plain.txt              # SKILL.md 纯文本版（name + description + 正文）
│   ├── src/                         # 生成图片用的 HTML
│   └── images/                      # banner.png · workflow.png · example-report.png
├── LICENSE
└── README.md
```

## 安装

见上方 [快速开始](#快速开始)。

## 已知局限

- 部分官方数据库对自动访问不友好：中国特殊食品信息查询平台可能超时；Cochrane、Examine 会限流；FDA 食品设施注册数据库不公开。遇到这些情况报告会标注"未能核验"。
- 国内电商平台价格大多需要登录或 App，通常只能给出搜索链接。
- 各国法规会更新。`references/regulators-by-region.md` 的链接检查日期为 2026-10-10。
- 证据分级由 agent 按规则判断，不能替代专业的系统评价。

## 免责声明

本项目及其生成的报告仅供信息参考，不构成医疗、营养或法律建议。保健品不能替代药物治疗。孕期或哺乳期、儿童、慢性病患者、正在服药或计划手术者，使用任何补充剂前请咨询医生或药师。

## 我的其他项目

- [A-writer-should-do](https://github.com/masterball-w/A-writer-should-do)：从一本书里蒸馏作者的写法，生成可直接调用的写作 Skill，仓库内附 7 个已蒸馏的作家实例

---

## English

**supplement-checker** is an Agent Skill. Give it a photo or promo image of a dietary supplement, and the agent produces a sourced report on:

1. **Ingredient evidence**: animal studies, RCTs and meta-analyses, graded Strong / Moderate / Limited / Animal-only / Evidence against, with the product dose compared to study doses and to RDA/UL.
2. **Compliance and registrations**: US (FDA does not approve supplements; DSLD, NDI, warning letters, recalls), Australia (ARTG), Canada (NPN), Japan (FFC / FOSHU), EU/UK claim registers, China (cross-border vs general-trade 蓝帽子 registration/filing), plus third-party certifications verified in each certifier's own database.
3. **Price comparison**: the same product across channels, and the same ingredient across brands normalized per effective daily dose, with the time of each check recorded.

**Principles:**
- No fabricated citations; every PMID/DOI/URL is fetched and verified.
- Unreachable sources are marked "not verified" instead of guessed.
- No invented prices.

**This is a research aid, not medical or legal advice.** Results depend on what the agent could access at the time of the check.

Install by copying this folder into your agent's skills directory (e.g. `~/.cursor/skills/supplement-checker/` or `~/.claude/skills/supplement-checker/`), then upload a supplement photo and ask the agent to check it. Licensed under MIT © 2026 masterball-w.
