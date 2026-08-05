<div align="center">
  <a href="https://github.com/Kumampet/Aqours5thaniv">
    <img src="https://raw.githubusercontent.com/Kumampet/Aqours5thaniv/master/img/top_mamber.png" width="760" alt="Aqours" />
  </a>

  <h1>你好，我是谭开文</h1>

  <p>
    桂林电子科技大学硕士研究生<br />
    Linux 内核网络 · eBPF/XDP · Native 网卡驱动 · 云原生数据面 · C++ 系统
  </p>

  <p>
    <img src="https://img.shields.io/badge/Focus-Linux%20Dataplanes-0f766e?style=flat-square" alt="Linux 数据面" />
    <img src="https://img.shields.io/badge/Research-eBPF%20%2F%20XDP-111827?style=flat-square" alt="eBPF 与 XDP" />
    <img src="https://img.shields.io/badge/Driver-r8169%20Native%20XDP-b91c1c?style=flat-square" alt="r8169 Native XDP" />
    <img src="https://img.shields.io/badge/Engineering-Reproducible-2563eb?style=flat-square" alt="可复现工程" />
  </p>

  <p>
    <b>中文</b> · <a href="./README_EN.md">English</a>
  </p>
</div>

## 关于我

我来自四川成都，目前是桂林电子科技大学研二学生，关注 Linux 内核网络、
真实网卡数据面、云原生基础设施和性能工程。

我喜欢追踪一个数据包的完整生命周期：它如何从虚拟机或容器出来，经过
`virtio`、`tap`、`veth`、Linux Bridge、OVS、VXLAN/Geneve，最后到达真实
网卡；以及在什么位置可以观测、验证或安全地加速它。

最近的工作从 eBPF 程序和 `vnet-dataplane` 的虚拟路径观测，推进到了
`r8169` Native XDP 外置驱动：自己处理 RX buffer 所有权、page-pool、DMA
同步、TX completion 和 `XDP_TX`，并在物理网卡上完成了 DNS cache 的
`1024/1024` 外部流量验收。

我重视三件事：边界清楚、结果可测量、实验可复现。对于会中断管理链路的
驱动和数据面实验，也会把构建输入、回滚边界和失败模式记录下来。

## 最近在做

- **Native XDP 网卡驱动**：把 `r8169` 改造成可编译的外置 `r8169_xdp.ko`，
  支持 `XDP_PASS`、`DROP`、`ABORTED`、非法 action、`adjust_tail(+16)` 和
  同设备 `XDP_TX`。
- **DNS eBPF 加速**：实现服务端/客户端缓存、pending flow、TTL、可信 DNS
  server 和 ringbuf 事件，比较 tc、generic XDP 与 native XDP 的路径差异。
- **虚拟化网络路径**：在 OpenStack、KVM、Kubernetes、OVS 环境中分析
  `virtio-net`、`tap`、`veth`、Bridge、Geneve/VXLAN 和 qrouter 的转发关系。
- **可复现验收**：用外部 peer、驱动计数器、链路状态和普通连通性测试，
  验证真实物理 RX/TX，而不是只在 veth 或 VM 里得到一个“看起来成功”的结果。

## 项目

### [r8169-native-xdp](https://github.com/Yukinoshita03/r8169-native-xdp)

面向 Linux `r8169` 的 Native XDP 外置驱动补丁和源码仓库。

- 基于 Linux 7.2-rc6 提供 Native XDP RX/TX 核心补丁；
- 提供 Ubuntu 7.0 目标 ABI 的兼容、显式 PCI/BDF 保护和故障注入补丁；
- 处理 page-pool、DMA ownership、RX replacement、共享 TX ring 和 completion；
- 发布展开后的 `r8169_main.c` 等驱动源码、可复现构建脚本和验证记录；
- 在一张 RTL8168H/8111H 类物理网卡上完成 DNS cache `1024/1024` Native-XDP
  回包验收。

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

面向虚拟化网络路径观测和轻量服务加速的 Linux eBPF Agent。

- 发现并记录 `veth`、`tap`、Bridge、OVS 等虚拟路径和候选挂载点；
- 观测 DNS、gRPC、TCP、UDP 的路径、时延、服务分类和 attach 状态；
- 提供 DNS XDP cache、客户端/服务端缓存和 gRPC fast-cache 原型；
- 包含 `netns + bridge + veth` 可复现实验、C++20 用户态数据面和虚拟网卡
  驱动原型；
- 配套 OpenStack/Kubernetes/OVS 的路径探测、tc attach 和数据面实验文档。

### [MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase)

正在开发中的现代 C++ 教学关系型数据库，架构参考 Stanford RedBase，工程
组织参考 OceanBase MiniOB。

- 使用 C++20、CMake 和跨平台 CI；
- 计划实现 Page、Buffer Pool、LRU、Heap File、Tuple、RID、B+ Tree 和 Catalog；
- 计划通过简化 SQL Parser 与 Volcano 执行模型支持基础 CRUD；
- 当前工程骨架、CLI 入口和冒烟测试已建立，数据库核心模块仍在实现中。

## 技术栈

<div align="center">

![C++](https://img.shields.io/badge/C++20-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=111827)
![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=111827)
![eBPF](https://img.shields.io/badge/eBPF%20%2F%20XDP-111827?style=for-the-badge&logo=linux&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![OpenStack](https://img.shields.io/badge/OpenStack-EF3B2D?style=for-the-badge&logo=openstack&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![CMake](https://img.shields.io/badge/CMake-064F8C?style=for-the-badge&logo=cmake&logoColor=white)

</div>

## 当前方向

我希望继续走系统与基础设施工程方向，深入 Linux 网络栈、网卡驱动、eBPF/
XDP、OpenStack/Kubernetes 数据面和性能敏感的 C++ 系统。

下一阶段会继续完善：

- `r8169_xdp` 的多轮 attach/detach、reset、link flap 和长时间压力验证；
- TX ring 满、RX refill 失败、DROP/ABORTED/invalid action 等故障路径；
- 物理网卡 Native XDP 与 OVS/tap/veth 观测面的边界；
- 可公开复现的构建、测试和性能数据。

<div align="center">
  <sub>我喜欢 Aqours。真正有意义的进步，往往也是一步一步积累出来的。</sub>
</div>
