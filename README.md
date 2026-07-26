# meng-skills

中文专业写作与去 AIGC 技能包。整合了五步闭环诊断工作流和五维质量评分体系，系统性地消除中文 AI 文本的结构性特征，使其通过 AIGC 检测。

## 适用场景

| 路由 | 场景 | 示例 |
|------|------|------|
| 实证论文 | 摘要、引言、理论分析、研究设计、回归结果、机制、异质性、稳健性、结论 | 经济学、管理学、金融学等实证研究 |
| 课题/项目申请 | 申报书、社科基金、自然基金、研究基础、技术路线、创新点 | 各类科研基金申报 |
| 公文/纪要/报告 | 会议纪要、座谈纪要、调研报告、工作汇报、政策建议 | 行政与政策文档 |
| 专业评论/阐释 | 读书笔记、学术评论、概念阐释、专业分析 | 专业知识输出 |

**不适用：** 英文写作（走 humanizer）、日常聊天、代码注释、数据表头、引号内原话。

## 核心能力

- **清除 AI 痕迹**：系统性消除四字套话、显性连接词、主语回避、绝对化断言、句长方差过低等五大结构性特征
- **差异化改写**：根据段落功能（事实陈述/论证/过渡）采用不同改写力度
- **自动路由**：按文本内容自动匹配到合适的文体规则，无需手动指定
- **五维自评**：具体性、节奏性、谨慎性、隐衔接、研究者语气，加权评分 ≥ 42 为通过
- **自动化验证**：内置 Python 脚本检测半角引号、否定句式、AI 高频词、破折号超标、句长方差过低

## 安装

### Hermes Agent

```bash
# 将 skills/ 目录复制到 Hermes 技能目录
cp -r meng-skills ~/.hermes/skills/writing/
# 或使用 Hermes 技能管理命令
```

Agent 自动读取 `SKILL.md`，当检测到中文专业写作任务时加载。

### 其他 Agent（Claude Code / Cursor / WindSurf）

```bash
# 复制到项目的 .claude/ 或 .cursor/ 目录
cp SKILL.md .claude/skills/meng-skills.md
```

## 使用方法

### 标准模式（默认）

直接提交中文专业文本，技能自动：
1. 冻结事实（数据、引用、人名、政策编号不改）
2. 判断文体并路由
3. 清除 AI 痕迹
4. 按对应文体规则润色
5. 交付终稿

### 深度模式（降 AIGC 检测率）

明确要求"降 AIGC"、"去 AI 味"、"过知网检测"时触发五步闭环：定位扫描 → 诊断分类 → 差异化改写 → 五维自评 → 二次复查。

## 项目结构

```
meng-skills/
├── SKILL.md                  ← 主技能文件
├── README.md                 ← 本文件
└── references/
    ├── professional-voice.md           ← 专业风格参考
    ├── official-doc-example.md         ← 公文范例
    ├── data-audit-checklist.md         ← 数据审核清单
    ├── jjgl-style-guide.md             ← 管理世界格式指南
    └── subsidy-allocation-methodology.md  ← 补贴配置效率研究方法论
```

## 依赖

独立使用，不依赖其他技能。Python 自动化验证依赖标准库（`zipfile`, `re`）。

## 维护

两个副本需同步更新：

| 位置 | 用途 | 路径 |
|------|------|------|
| Hermes 技能系统 | Agent 运行时加载 | `~/.hermes/skills/writing/meng-skills/SKILL.md` |
| 本地项目仓库 | 版本控制 + GitHub 发布 | `~/hermes/技能/meng skills v2/SKILL.md` |

修改流程：先改 Hermes 版本（`skill_manage`），再 `cp` 到本地仓库。

## 许可

MIT
