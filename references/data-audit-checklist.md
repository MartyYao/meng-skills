# 研究设计数据审计清单

> 用途：研究设计完成后、开始实证分析前，逐项对照检查 working data
> 来源：论文1 v2.0 数据审计过程（2026-07-08）

---

## 一、审计流程

```
研究设计 v2.0
  → 逐模块提取变量需求
    → 对照 working data 检查覆盖
      → 标记：✅ 已有 / ⚠️ 可自算 / ✗ 需外部
        → 优先级排序
```

---

## 二、检查维度

### A. 处理变量

| 检查项 | 具体内容 |
|--------|---------|
| binary 存在 | post / d_bureau |
| 级别分层 | d_zhengting, d_futing, level_yr |
| 性质分层 | d_admin_gov, d_admin, nature_yr |
| 连续强度 | treat_score1 (0-5), treat_score2 (0-3) |
| 动态演变 | 升格/转性省份的时间序列变化 |
| province scope | 排除非境内注册实体（开曼、香港） |
| year range | 按设计截取（如 2015-2023） |

### B. 被解释变量

| 检查项 | 具体内容 |
|--------|---------|
| 研发补贴 V1 | dummy + 金额 + 对数 |
| 研发补贴 V2 | dummy + 金额 + 对数 |
| 研发补贴 V3 | 年报文本标记 |
| 三版一致性 | any_rd_subsidy, V1∩V3 子样本 |
| 非研发补贴 | 总额 - 研发 = 非研发（能否拆分为具体类别？） |
| 补贴条目数 | n_subsidy_v1/v2, n_total |

### C. R&D 与专利

| 检查项 | 具体内容 |
|--------|---------|
| 研发投入 | rd_spending, ln_rd, rd_intensity |
| 滞后项 | lag_ln_rd |
| 专利 | patent_inv, patent_total |
| 研发效率 | patent_eff（可从专利/R&D 构造） |

### D. 机制变量

| 机制 | 变量 | 检查 |
|------|------|------|
| 政治关联 | pc_any, pc_npc, pc_cppcc, pc_gov | 缺失率？匹配方式？ |
| 研发操纵（A） | suspect_a, near_threshold, n_near | 阈值定义是否与设计一致？ |
| 研发操纵（B） | suspect_b, patent_eff, p33_eff | 效率分组是否与设计一致？ |
| 综合嫌疑 | suspect_rd | 覆盖 suspect_a ∪ suspect_b？ |
| 备选 | Bper, RDIN | 与 suspect_rd 的重叠度？ |

### E. 控制变量

| 类别 | 变量 | 来源 |
|------|------|------|
| 企业财务 | Size, Lev, ROA, TobinQ, Board, Indep, Top1, SOE, Dual, Mshare, Growth, FirmAge, ListAge | CSMAR |
| 省份宏观 | Structure_pt（二产/GDP）, Market_pt（樊纲指数） | 通常不在 working data 中 |
| 竞争性政策 | 金税三期、信息惠民、数据开放平台、留抵退税 | 通常不在 working data 中 |

### F. 内生性变量

| 变量 | 来源 |
|------|------|
| Peer IV | 可从省级面板自算 |
| 省级领导特征 | CSMAR 地方官员数据库 |

### G. 进一步研究变量

| 方向 | 需要的额外数据 |
|------|---------------|
| TFP 经济后果 | 营业收入、员工数、固定资产净值、中间投入 |
| 地级市双层 DID | 地级市大数据局成立时间 |

---

## 三、常见缺口

以下变量在首次合并的 working data 中通常缺失：

1. **省份宏观控制变量**：二产占比、市场化指数 —— P0 主回归必需
2. **竞争性政策时间线**：金税三期、信息惠民等 —— P0 稳健性必需
3. **非研发补贴拆分**：稳岗 vs 出口 —— P1 Falsification 必需
4. **TFP 组分**：营收、员工、固定资产 —— P2 进一步研究
5. **地方官员特征**：任期、年龄 —— P3 内生性补充
