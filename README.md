<div align="center">
  <a href="https://github.com/Kumampet/Aqours5thaniv">
    <img src="https://raw.githubusercontent.com/Kumampet/Aqours5thaniv/master/img/top_mamber.png" width="760" alt="Aqours" />
  </a>

  <h1>你好，我是谭开文</h1>

  <p>
    桂林电子科技大学硕士研究生<br />
    Linux 网络 · eBPF/XDP · 虚拟化数据面 · C++ 系统
  </p>

  <p>
    <img src="https://img.shields.io/badge/Focus-Linux%20Dataplanes-0f766e?style=flat-square" alt="Linux 数据面" />
    <img src="https://img.shields.io/badge/Research-eBPF%20%2F%20XDP-111827?style=flat-square" alt="eBPF 与 XDP" />
    <img src="https://img.shields.io/badge/Engineering-Reproducible-2563eb?style=flat-square" alt="可复现工程" />
  </p>

  <p>
    <b>中文</b> · <a href="./README_EN.md">English</a>
  </p>
</div>

## 关于我

我来自四川成都，目前是桂林电子科技大学研一学生，关注内核网络、云原生基础设施和系统性能工程。

我目前主要研究 Linux 虚拟化网络和 eBPF/XDP，平时会用 C/C++、Go 写一些数据面程序，分析数据包在 `veth`、`tap`、Linux Bridge 和 OVS 之间的转发过程，也会尝试做一些性能优化。

做项目时，我更在意它能不能真正跑起来、测试结果能不能复现，以及出了问题能不能定位和回退。

## 研究方向

- 面向容器与虚拟化网络的 **eBPF/XDP 数据面**。
- KVM、OpenStack 和 Kubernetes 环境中跨 `veth`、`tap`、Linux Bridge 与 OVS 的**数据包路径观测**。
- **Kubernetes CNI 快速路径**，包括 Pod 本地与跨节点转发、IPIP 封装、Service 负载均衡、SNAT 和连接跟踪。
- **C++20 用户态数据包处理**以及用于理解内核收发路径的最小 Linux 虚拟网卡驱动。
- 能够呈现正确性、时延和回退行为的**可复现网络基准测试**。
- 小型关系型数据库的存储、索引和查询执行机制。

## 项目

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

`vnet-dataplane` 是一个面向虚拟化网络路径观测与轻量服务加速的 Linux eBPF Agent。

- 发现跨 `veth`、`tap`、Linux Bridge 和 OVS 的数据包路径与候选挂载点。
- 观测 DNS、gRPC、TCP 和 UDP 流量，输出路径、时延、服务分类和挂载状态。
- 提供受控的 DNS XDP Cache 与 gRPC Fast Cache 原型。
- 包含可复现的 `netns + bridge + veth` 基准、C++20 用户态数据面和最小虚拟网卡驱动。

### [MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase)

`MiniRedBase` 是一个正在开发中的现代 C++ 教学关系型数据库，架构参考 Stanford RedBase，工程组织参考 OceanBase MiniOB。

- 使用 C++20、CMake 和跨平台 CI，保持核心实现小而清晰。
- 计划实现 Page、Buffer Pool、LRU、Heap File、Tuple、RID、B+ Tree 和 Catalog。
- 计划使用简化 SQL Parser 与 Volcano 执行模型支持基础增删改查。
- 核心代码目标控制在 10,000 至 15,000 行，并选择 WAL 崩溃恢复或 LRU-K 基准作为扩展方向。
- 当前状态：工程骨架、命令行入口和冒烟测试已经建立，数据库核心模块尚未实现。

## 技术栈

<div align="center">

![C++](https://img.shields.io/badge/C++20-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=111827)
![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=111827)
![eBPF](https://img.shields.io/badge/eBPF%20%2F%20XDP-111827?style=for-the-badge&logo=linux&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![CMake](https://img.shields.io/badge/CMake-064F8C?style=for-the-badge&logo=cmake&logoColor=white)

</div>

## 当前目标

我希望继续走系统与基础设施工程方向，深入 Linux 内核、网络数据面和性能敏感的 C++ 系统。现阶段最重要的事情，是持续构建、测量，并把底层实验整理成边界清晰、能够解释和重复验证的软件。

<div align="center">
  <sub>我喜欢 Aqours。真正有意义的进步，往往也是一步一步积累出来的。</sub>
</div>
