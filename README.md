# Job Market Data — 德国数据工程师求职市场数据

> 德国 Python / 数据工程师职位市场结构化数据集：职位列表、薪资水平、签证政策、市场需求与技能要求，含配套分析报告。

从原 `Germany_job` 求职项目中提取市场数据部分，独立为纯数据仓库，便于长期更新与复用。

---

## 📁 目录结构

```
job-market-data/
├── README.md                        # 本文件
├── index.html                       # GitHub Pages 数据展示页
├── .gitignore
├── .nojekyll
│
├── data/                            # 结构化数据（核心）
│   ├── jobs.csv                     # 德国数据工程师职位列表（89 条，2026-08 刷新）
│   ├── market_data_2026.csv         # 2026 市场数据（CSV，49 条记录）
│   ├── market_data_2026.json        # 2026 市场数据（JSON，结构化层级）
│   └── market_data_2026.xlsx        # 2026 市场数据（Excel，综合查看）
│
└── reports/                         # 数据采集与分析报告
    ├── jobs_analysis.md             # Python 数据工程师职位市场分析
    ├── job_report.md                # 89 个职位机会完整清单（含链接）
    ├── data_acquisition_2026.md     # 2026 数据获取报告（来源与方法）
    ├── data_file_assessment.md      # 数据文件评估报告
    └── info_fetch_test.md           # 信息获取渠道测试报告
```

---

## 📊 数据集说明

### 1. `data/jobs.csv` — 职位列表

德国数据工程师职位汇总，采集自 arbeitnow.com（2026-08-26 刷新，89 条）。

| 字段 | 说明 |
|------|------|
| Job Title | 职位名称 |
| Company | 公司 |
| Location | 工作地点（柏林 / 慕尼黑 / 远程等） |
| Level | 级别（Junior / Mid / Senior / Lead / Staff-Principal 等） |
| Remote | 是否远程（Yes / 空） |
| Link | 职位链接 |

### 2. `data/market_data_2026.*` — 市场数据（同一数据的三种格式）

覆盖 7 大类别、49 条记录：

| 类别 | 内容概要 |
|------|----------|
| 薪资数据 | 全国平均年薪 / 中位数、柏林·慕尼黑·法兰克福·斯图加特城市对比、数据工程师分级薪资 |
| 签证政策 | 机会卡（Chancenkarte）条件与评分系统、欧盟蓝卡薪资门槛 |
| 市场需求 | IT 人才缺口、AWS 投资与岗位创造、企业数据增长 |
| 技能需求 | 核心技能（Python / SQL / 云平台）与工具栈要求 |
| 机会卡评分 | Chancenkarte 积分制逐项评分标准 |
| 城市对比 | 主要城市薪资与生活成本 |
| 行业趋势 | 2025–2026 市场走向 |

**CSV 字段**：`数据类别, 数据项, 数值/内容, 单位, 年份, 数据来源, 更新时间, 备注`

**JSON 结构**：`metadata` / `salary_data` / `visa_policy` / `market_demand` / `skills_demand`（键名双语标注 zh-CN/de-DE）

**数据时间范围**：2025–2026 年；采集日期 2026-06-01。

---

## 🛠 使用方法

```python
import pandas as pd
import json

# 职位列表
jobs = pd.read_csv("data/jobs.csv")

# 市场数据（CSV）
market = pd.read_csv("data/market_data_2026.csv")

# 市场数据（JSON，含层级结构）
with open("data/market_data_2026.json", encoding="utf-8") as f:
    market_json = json.load(f)

print(market_json["salary_data"]["data_engineer"]["salary_range"])
```

- 表格分析 → 用 CSV
- 程序处理 → 用 JSON（保留层级与双语标注）
- 人工浏览 → 用 Excel

---

## 📈 报告导读

| 想了解 | 读这份 |
|--------|--------|
| 市场行情结论、Python 职位推荐梯度 | `reports/jobs_analysis.md` |
| 89 个职位完整清单与链接 | `reports/job_report.md` |
| 数据从哪来、怎么采的 | `reports/data_acquisition_2026.md` |
| 数据质量与文件评估 | `reports/data_file_assessment.md` |
| 采集渠道有效性验证 | `reports/info_fetch_test.md` |

---

## 🔄 更新维护

1. 重新采集后更新 `data/` 下对应文件（三种格式保持同步）
2. 同步更新 `reports/` 中的分析报告
3. 数据来源以网络搜索（中 / 英 / 德三语）为主，关键数值在 CSV `数据来源` 列注明

## ⚠️ 时效说明

薪资与签证政策数据随时间变化，引用前请核对 `年份` 与 `更新时间` 字段，并以官方来源（如 Make it in Germany、Bundesagentur für Arbeit）为最终依据。

---

## 🧰 技术栈

- **数据格式**：CSV / JSON / Excel（零依赖，任意工具可读）
- **展示**：GitHub Pages（`index.html`）

## 📦 仓库

`Wadesha/job-market-data`（公开）
