<div align="center">
  <a href="https://github.com/Yukinoshita03/Yukinoshita03">
    <img src="./assets/yukino-2.gif" width="760" alt="雪之下雪乃" />
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

我来自四川成都，现在是桂林电子科技大学研二。平时电脑上常年开着几台
虚拟机、几个终端和一堆抓包窗口，研究的东西基本都绕不开 Linux 网络、
云原生基础设施和性能敏感的 C++。

我很容易被一个问题拽住：**一个包到底是怎么走到目的地的？** 它可能先经过
`virtio`、`tap`、`veth`、Bridge、OVS，再套上一层 VXLAN/Geneve，最后才到
真实网卡。我喜欢把这条路径一段段拆开，找到可以观测、验证、也确实值得
加速的位置。

最近一段时间，我把 `vnet-dataplane` 里的 eBPF/XDP 实验往物理网卡推进，
单独做了 `r8169-native-xdp`：从 RX buffer 所有权、page-pool 和 DMA 同步，
一路写到 TX completion 和 `XDP_TX`，最后在真实网卡上把 DNS cache 的
`1024/1024` 外部请求跑通。

我不太满足于“程序能编译”或“veth 里能通”。我更想知道它在真实路径上是否
成立、哪里会断、断了之后能不能解释清楚，所以会把构建输入、测试命令、
计数器和失败边界一起留下来。

## 最近在做

- **最近最上头的是 Native XDP 网卡驱动**：把 `r8169` 改造成可编译的外置
  `r8169_xdp.ko`，一路处理 `XDP_PASS`、`DROP`、`ABORTED`、非法 action、
  `adjust_tail(+16)` 和同设备 `XDP_TX`。
- **DNS eBPF 加速**：服务端/客户端缓存、pending flow、TTL、可信 DNS server
  和 ringbuf 事件都在做，顺便比较 tc、generic XDP 和 native XDP 到底差在哪。
- **虚拟化网络路径**：在 OpenStack、KVM、Kubernetes、OVS 环境里追
  `virtio-net`、`tap`、`veth`、Bridge、Geneve/VXLAN 和 qrouter 的转发关系。
- **把验收做得像验收**：用外部 peer、驱动计数器、carrier 和普通连通性，
  确认流量真的走过物理 RX/TX，而不是只在 veth 或 VM 里“看起来成功”。

## 项目

### [r8169-native-xdp](https://github.com/Yukinoshita03/r8169-native-xdp)

这是我最近单独拆出来的仓库：面向 Linux `r8169` 的 Native XDP 外置驱动补丁
和源码。最开始只是想让 XDP 在物理网卡上真正跑起来，后来发现真正麻烦的
是 buffer ownership、DMA、TX ring 和 reset 这些细节。

- 基于 Linux 7.2-rc6 提供 Native XDP RX/TX 核心补丁；
- 提供 Ubuntu 7.0 目标 ABI 的兼容、显式 PCI/BDF 保护和故障注入补丁；
- 处理 page-pool、DMA ownership、RX replacement、共享 TX ring 和 completion；
- 发布展开后的 `r8169_main.c` 等驱动源码、可复现构建脚本和验证记录；
- 在一张 RTL8168H/8111H 类物理网卡上完成 DNS cache `1024/1024` Native-XDP
  回包验收。

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

这是主线项目，也是很多实验的起点。它是一个面向虚拟化网络路径观测和轻量
服务加速的 Linux eBPF Agent。

- 发现并记录 `veth`、`tap`、Bridge、OVS 等虚拟路径和候选挂载点；
- 观测 DNS、gRPC、TCP、UDP 的路径、时延、服务分类和 attach 状态；
- 提供 DNS XDP cache、客户端/服务端缓存和 gRPC fast-cache 原型；
- 包含 `netns + bridge + veth` 可复现实验、C++20 用户态数据面和虚拟网卡
  驱动原型；
- 配套 OpenStack/Kubernetes/OVS 的路径探测、tc attach 和数据面实验文档。

### [MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase)

这是另一条线：一个正在开发中的现代 C++ 教学关系型数据库，架构参考
Stanford RedBase，工程组织参考 OceanBase MiniOB。

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

我想继续沿着系统与基础设施这条路走下去，把 Linux 网络栈、网卡驱动、
eBPF/XDP、OpenStack/Kubernetes 数据面和 C++ 系统真正串起来。

接下来会继续折腾：

- `r8169_xdp` 的多轮 attach/detach、reset、link flap 和长时间压力验证；
- TX ring 满、RX refill 失败、DROP/ABORTED/invalid action 等故障路径；
- 物理网卡 Native XDP 与 OVS/tap/veth 观测面的边界；
- 可公开复现的构建、测试和性能数据。希望以后别人 clone 下来，也能知道我
  当时到底测了什么，而不是只能看一张漂亮的结果截图。

<div align="center">
  <sub>我喜欢 Aqours。真正有意义的进步，往往也是一步一步积累出来的。</sub>
</div>
