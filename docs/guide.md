# 使用指南

本页只说明各章节该用什么环境学。

## 先看结论

| 你的目标 | 推荐环境 | 备注 |
|---|---|---|
| 先入门 Chapter 0 / 1 | 在线 Notebook 或本地基础环境 | 主要是 Python、Jupyter、NumPy |
| 系统学习 Chapter 2 | 统一 Python 环境 + 本地 CPU；部分题再切 GPU | 大多数题可 CPU-first |
| 完整学习 Chapter 3 | Linux + NVIDIA GPU + CUDA / Triton | GPU-required |
| 想统一团队环境 | CNB / Docker / 云端 GPU | 适合一致性和复现 |

---

## 四层环境分层

### 1. 轻量学习层

适用章节：
- Chapter 0
- Chapter 1

环境特点：
- Python
- Jupyter / Notebook
- NumPy / 基础科学计算
- Colab / 在线 Notebook 可直接开始

这两章对部署要求低，重点是把基础概念和前置知识学稳，不需要一开始就上复杂容器或 GPU 工具链。

### 2. 主力学习层

适用章节：
- Chapter 2

环境特点：
- 统一 Python 环境
- PyTorch
- correctness 验证脚本
- 本地 CPU 足够覆盖大多数题

- Chapter 2 是 **CPU-first**
- 已确认至少 `21_Gradient_Checkpointing` 需要 NVIDIA GPU 才能测真实 CUDA 显存峰值
- 学习时建议尽量使用同一套 Python 依赖，保证练习和验证结果一致

### 3. 高门槛实验层

适用章节：
- Chapter 3

环境特点：
- Linux
- NVIDIA GPU
- CUDA
- Triton
- 编译工具链

- Chapter 3 是 **GPU-required**
- 少数页面可能有阅读路径或 CPU fallback，但不构成完整学习路径

### 4. 统一交付层

适用场景：
- 团队协作
- 统一实验镜像
- 云端开发
- 需要减少本地环境差异时

平台选项：
- Colab
- CNB
- Docker
- 云端 GPU 托管环境

这层主要服务 Chapter 2 后段和 Chapter 3，目标是把“能跑”变成“大家都按同一套环境跑”。

当前验证状态：
- **Colab**：已验证，可一键直达
- **Docker**：推荐以 **40 系 NVIDIA GPU** 作为主基线，30 系可作为兼容目标，但不默认承诺
- **CNB**：待仓库迁移后再做实机验证
- **ModelScope / 其他在线 Notebook**：待验证

### Notebook 使用

- 执行单元格：`Shift + Enter` 或 `Ctrl + Enter`
- 执行所有单元格：`Run -> Run All Cells`
- 刷题流程：先看导学，再填 TODO，再跑测试
- 如果 notebook 报 `name not defined`，通常是前面的 cell 没按顺序执行

---

## Chapter 2 / 3 的实际要求

### Chapter 2

- 整体定位：CPU-first
- 大多数 notebook：可在 CPU 环境下完成学习和 correctness 验证
- 已确认 GPU 题：`21_Gradient_Checkpointing`
- 推荐策略：统一 Python 环境，GPU 用于后段实验和真实性能验证
- 已验证：当前本机 `llm_algo` 环境下，Chapter 2 答案区全量通过

### Chapter 3

- 整体定位：GPU-required
- 完整体验：Linux + NVIDIA GPU + CUDA / Triton
- 代码审计结果：本章直接面向 GPU 内核、显存和通信行为
- 推荐策略：把 Linux 作为默认参考环境，其他系统只作为补充
- 已验证：当前本机 `llm_algo` 环境下，Chapter 3 答案区全量通过

### 本地平台备注

- **Linux 22.04**：已验证，是当前最稳的本地参考环境
- **WSL2**：理论上可作为过渡方案，但尚未作为主验证基线
- **macOS**：可能接近可用，但尚未完成逐项验证，不应默认承诺 Chapter 3 完整体验

---

## 怎么选

### 只想快速开始
- 用在线 Notebook
- 先学 Chapter 0 / 1

### 想系统学 Chapter 2
- 用本地基础环境
- 保持同一套 Python 依赖
- 需要真实显存或性能再切 GPU

### 想完整学 Chapter 3
- 用 Linux + NVIDIA GPU
- 先装好 CUDA / Triton / 编译工具链

### 想统一环境
- 优先 CNB / Docker / 云端 GPU
- 适合团队、课程和长期复现

---

## 环境文件怎么分

- `environment.yml`：本地主入口
- `requirements/base.txt`：基础依赖
- `requirements/dev.txt`：开发和测试依赖
- `requirements/gpu.txt`：Chapter 3 / Triton / GPU 扩展依赖
- `cnb/README.md`：未来云端统一环境说明
- `cnb/environment.yml`：未来云端环境骨架

---

## 相关阅读

- [维护与发布手册](./maintenance.md)
- [Chapter 2 导学](./02_PyTorch_Algorithms/intro.md)
- [Chapter 3 导学](./03_CUDA_and_Triton_Kernels/intro.md)
