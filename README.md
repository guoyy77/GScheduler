# GScheduler
[![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PyPI version](https://badge.fury.io/py/gscheduler.svg)](https://badge.fury.io/py/gscheduler) <!-- 发布后替换为真实链接 -->
一个用于模拟和实验各种任务调度策略的 Python 沙盒。
> **"调度积木盒"** - 搭建框架，填充策略，模拟万物。
---
## 🌟 为什么需要 GScheduler？
在真实系统（如 K8s, YARN）上测试和调试调度策略，往往成本高昂、风险巨大且难以复现。
GScheduler 为开发者、学生和研究者提供了一个**轻量级、可控、可重复**的本地环境，让你可以：
- **快速验证**：在几分钟内测试你的新调度算法，而不是部署一个集群。
- **深度理解**：通过可视化，直观地看到不同策略（如 FIFO, 贪心）如何影响任务执行。
- **安全实验**：模拟极端场景（如任务依赖风暴、资源耗尽），而不用担心搞垮生产环境。
---
## 🚀 快速开始
### 安装
```bash
pip install gscheduler
```
### 你的第一个调度模拟
只需几行代码，即可模拟一个简单的调度场景：
```python
from gscheduler import Task, Resource, GreedyScheduler, Simulator
# 1. 定义一些任务
tasks = [
    Task(name="Data Loading",   duration=3, priority=2),
    Task(name="Model Training", duration=5, priority=1),
    Task(name="Result Saving",  duration=2, priority=3),
]
# 2. 定义你的资源池
resources = Resource(cpu=4)
# 3. 选择一个调度策略
scheduler = GreedyScheduler()
# 4. 运行模拟器
sim = Simulator(tasks, resources, scheduler)
sim.run()
# 5. 查看结果
sim.print_report()
sim.print_gantt_chart()
```
**输出示例：**
```
--- Simulation Report ---
Total Makespan: 10
Average Waiting Time: 1.33
Resource Utilization (CPU): 80.00%
-------------------------
--- Gantt Chart ---
Data Loading : [██████          ]
Model Training: [      ██████████]
Result Saving : [              ██]
-------------------------
```
---
## 🧠 项目缘起
这个项目的灵感，源自一道经典的 [LeetCode IPO 算法题](https://leetcode.cn/problems/ipo/description/)。
在用排序和优先队列解决它之后，一个问题在我脑中挥之不去：**这个模型，能否用于更复杂的系统任务调度？**
- 如果我要做 K 个推理任务，按所需资源排序，资源满足就执行... 但总资源是固定的，不能增加怎么办？
- 如果任务之间存在复杂的拓扑依赖关系呢？
- 如果多个任务可以并行执行呢？
一个又一个的“如果”，最终汇聚成了这个想法：**开发一个“调度积木盒”**。我把整个框架搭建好，写好通用接口，大家只需要往模块里填充自己的调度策略，就能轻松模拟各种复杂情况下的调度行为。
---
## 📋 路线图
我正在从一个最小可行产品（MVP）快速迭代。
### ✅ MVP 目标 (2025.10.15 - 2025.12.31)
- [x] 核心任务与资源模型
- [x] 至少两种调度策略 (`FIFO`, `Greedy`)
- [x] 文本形式的 Gantt 图输出
- [x] 基础性能报告 (总时长, 平均等待时间, 资源利用率)
- [x] 简单易用的 API
### 🚀 未来计划
- [ ] **更多调度策略**: `Shortest Job First (SJF)`, `Fair Share`, `Backfilling`
- [ ] **任务依赖**: 支持基于拓扑排序的复杂工作流调度
- [ ] **可视化增强**: 基于 `matplotlib`/`plotly` 的交互式图表
- [ ] **插件系统**: 更灵活的策略加载机制，支持外部文件定义策略
- [ ] **性能分析**: 更详细的统计指标和瓶颈分析工具
---
## 🤝 如何贡献
热烈欢迎任何形式的贡献！
1.  **Fork** 这个仓库。
2.  创建你的特性分支 (`git checkout -b feature/AmazingFeature`)。
3.  提交你的更改 (`git commit -m 'Add some AmazingFeature'`)。
4.  推送到分支 (`git push origin feature/AmazingFeature`)。
5.  开启一个 **Pull Request**。
查看 [CONTRIBUTING.md](CONTRIBUTING.md) 了解更多细节。
---
## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

---
## 💌 致谢
感谢每一位对这个想法感兴趣、提出建议或贡献代码的朋友。你们的参与，让这个“积木盒”变得越来越有趣。

