# 实验环境说明

- 硬件：Intel Core Ultra 7 265K，32 GB DDR5，NVIDIA GeForce RTX 5070 Ti
- 软件：Python 3.11 / 3.12.14，Docker 24，PostgreSQL 15（可配置 MySQL）
- 组件微基准平台：macOS-14.8.1-arm64-arm-64bit
- 组件微基准 Python：3.12.14
- 网络调用：0（本测定不访问外部服务）
- 预热/重复：warmup=3, repeats=30
- 随机种子：20261024
- 模型配置（论文表3）：InsightEngine=Kimi K2.5；MediaEngine=Gemini 3.1 Pro（预览版）；QueryEngine=DeepSeek-V3.2；ForumEngine=Qwen3.5-397B-A17B；ReportEngine=Gemini 3.1 Pro（预览版）
- 论坛调度默认参数：η=5，Δ=120 s，ω=600 s
- 追踪开销（100 区间）：13.206±0.328 ms，中位数 13.135 ms，约 649.1 字节/区间
- 故障注入：15 个主题 × 3 类中断 × 2 次；30 个构造缺失结束事件全部识别
