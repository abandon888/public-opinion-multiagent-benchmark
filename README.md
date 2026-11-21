# 舆情研判多智能体评测数据集（Public Opinion Multi-Agent Benchmark）

> 本仓库为合成数据集（synthetic benchmark）：主题语料、金标准与方法运行记录均由固定随机种子构造生成，用于支撑论文表格的可复现核对；不是真实社交平台抓取数据。

面向论文《面向舆情研判的大语言模型多智能体论坛式异步协作机制研究》的支撑数据发布。仓库提供 20 个评测主题、去标识化语料、金标准标注、14 种方法的叶级运行记录，以及与论文表 5/7/8/9/10/11 对齐的汇总结果。

## 数据规模

| 项目 | 数量 |
| --- | --- |
| 主题 | 20（4 类 × 5） |
| 帖子 | 13,160 |
| 评论 | 47,617 |
| 含图像/视频帖子 | 3,201 |
| 关键事件（金标准） | 203 |
| 关键观点（金标准） | 140 |
| 方法运行记录 | 14 × 20 × 3 = 840 |
| 过程文件组 | 37 |

## 目录结构

```
data/
  topics.csv / topics.json
  corpus/{topic}/{posts,comments,media_index}.jsonl
  gold/{topic}.{events,views}.csv
experiments/
  runs.csv
  tables/table{5,7,8,9,10,11}_*.csv
  process/{topic}/{method}/   # forum.log, engine logs, trace.jsonl, report.html
  measurements/               # 本地组件测定与故障注入
annotations/                  # FA / TR / 专家评分 / 采纳 / 一致性
```

## 与论文表格的对应关系

| 论文表格 | 仓库文件 | 说明 |
| --- | --- | --- |
| 表5 评测任务集 | `experiments/tables/table5_taskset.csv` | 4 类主题规模统计 |
| 表7 主实验 | `experiments/tables/table7_main.csv` | B1–B5 与本文方法 |
| 表8 假设检验汇总 | `experiments/tables/table8_hypothesis.csv` | H1–H3 判据与结论 |
| 表9 消融 | `experiments/tables/table9_ablation.csv` | 模块去除变体 |
| 表10 协作过程 | `experiments/tables/table10_process.csv` | 读取率/时效/采纳率 |
| 表11 模块耗时 | `experiments/tables/table11_modules.csv` | 单主题 3 次模块耗时 |

本文方法摘要指标（与叶级记录一致）：

- 关键事件召回率（ER）77.3±3.8
- 陈述级事实准确率（FA）85.0±3.3
- 数值可追溯率（TR）75.9±6.9
- 平均端到端耗时 9.1±0.9 min
- token 消耗 38.5±5.4 千个，相对共享消息池与多智能体辩论分别低约 8.8% 与 7.2%

案例主题 `S1-1` 对应正文 4.6 节 T1「某餐饮品牌预制菜争议」，时间窗为 2025-09-10 至 2025-09-15。

## 过程文件

`experiments/process/` 为 37 组运行产物样例：

- `full`：全部 20 个主题
- `B1`–`B5`：各 2 个主题
- 消融变体与工程改进配置：各 1 个主题

每组包含：

- `forum.log`：论坛协作日志（`[时:分:秒] [来源] 内容`）
- `insight.log` / `media.log` / `query.log`：分析智能体总结日志
- `trace.jsonl`：调度追踪（字段对齐 BettaFish `TraceRecorder`）
- `report.html`：阶段性研判报告
- `run_meta.json`：与 `runs.csv` 对齐的指标快照

## 标注文件

- `annotations/fa_claims.csv`：陈述级事实核查
- `annotations/tr_numbers.csv`：数值可追溯核查
- `annotations/expert_scores.csv`：专家评分（完整性/准确性/逻辑性/可操作性）
- `annotations/ar_adoption.csv`：摘要采纳判定
- `annotations/agreement.csv`：标注一致性（Krippendorff α / Cohen κ）

## 本地测定

`experiments/measurements/` 收录组件级测定：

- 检索缓存、素材去重、追踪写入开销
- 论坛调度（η/Δ/ω）可控时钟回放
- 15 主题 × 3 类中断 × 2 次故障注入记录
- 环境与模型配置说明

## 复现核对建议

1. 用 `experiments/runs.csv` 按「主题内 3 次取均值 → 跨主题均值±样本标准差」重算表 7/9。
2. 用 `data/topics.csv` 汇总帖子/评论/媒体/事件/观点，核对表 5。
3. 用 `experiments/process/*/full/run_meta.json` 抽查 ER/FA/TR 与报告内陈述、数值条数是否一致。
4. 对照 `experiments/measurements/local_measurements.json` 核验追踪开销与调度回放数字。

## 许可与引用

- 数据许可：CC BY 4.0（见 `LICENSE`）
- 引用信息：`CITATION.cff`
- 原型系统基于开源项目 [BettaFish](https://github.com/666ghj/BettaFish)（GPL-2.0）二次开发；本仓库仅发布评测数据与过程产物，不包含该项目源代码。

```
@dataset{public_opinion_multiagent_benchmark_2026,
  title     = {Public Opinion Multi-Agent Benchmark},
  author    = {Wang, Yuhan and Jiang, Yun and Chen, FengFeng},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/abandon888/public-opinion-multiagent-benchmark}
}
```

## 联系

如需补充真实平台快照、端到端墙钟时间轴或更大范围过程日志，请通过论文通讯作者联系。
