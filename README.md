# 舆情研判多智能体评测数据集（Public Opinion Multi-Agent Benchmark）


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

