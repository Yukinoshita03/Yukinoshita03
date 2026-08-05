<div align="center">
  <a href="https://github.com/Yukinoshita03/Yukinoshita03">
    <img src="./assets/yukino-code-hero-4k.png" width="760" alt="雪之下雪乃在深夜写代码" />
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

我来自四川成都，现在在桂林电子科技大学读研二。主要做 Linux 网络、
eBPF/XDP、虚拟化数据面和性能敏感的 C++ 系统。

我平时最关心的是一个很具体的问题：**一个数据包从虚拟机或容器出来以后，
究竟经过了哪些设备？** 它可能先走 `virtio`、`tap`、`veth`、Bridge 和
OVS，再套上 VXLAN/Geneve，最后才到物理网卡。我喜欢顺着这条路径查下去，
弄清楚每一层做了什么、哪里出了问题，以及哪些位置真的值得加速。

最近我把 `vnet-dataplane` 里的 eBPF/XDP 实验继续往物理网卡推进，单独做了
`r8169-native-xdp`。从 RX buffer 的生命周期、page-pool、DMA 同步，到 TX
completion 和 `XDP_TX`，这些细节都要自己弄明白；最后也确实在真实网卡上把
DNS cache 的 `1024/1024` 个外部请求跑通了。

我不太喜欢只写一句“已经跑通”。通常会把数据包路径、测试命令、驱动计数器
和失败场景一起记下来，确认它为什么能跑、什么时候会停，以及出了问题该从
哪里恢复。

## 研究方向

我现在主要在看三条线：

- **Linux 内核网络和网卡驱动**：关注 RX/TX、DMA、page-pool、NAPI、驱动
  生命周期，以及 Native XDP 在真实网卡上到底怎样工作；
- **eBPF/XDP 数据面**：做 DNS cache、流量观测和窄范围的快速路径，比较
  tc、generic XDP 和 native XDP 在不同挂载点上的差别；
- **虚拟化和云原生网络**：分析 KVM、OpenStack、Kubernetes、OVS 里的
  `virtio`、`tap`、`veth`、VXLAN/Geneve、qrouter 等路径。

另外我也在用 C++ 学习数据库的存储、索引和查询执行，这就是
[MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase) 这条线。

## 想找的工作

我希望找 Linux 内核网络、eBPF/XDP、网卡驱动、云原生基础设施或高性能
C++ 系统研发相关的岗位。

我更偏向底层和基础设施方向：能接触真实机器和数据面，能写代码，也能花
时间测量性能、分析故障和把问题讲清楚。如果工作内容既有工程落地，也有
一点系统研究和实验空间，就很适合我。

## 语言和技术栈

- **最常用的语言**：C/C++（主要写 C++20）、Go、Python；
- **正在学习**：Rust，希望以后用它补充系统工具和基础设施开发；
- **系统与网络**：Linux、KVM、eBPF/XDP、TC、NAPI、网卡驱动、OVS、
  OpenStack、Kubernetes、Docker；
- **工程工具**：CMake、Make、Git、GDB、Clang/GCC、Shell，以及可复现的
  netns/bridge/veth 测试环境。

## 最近在做

最近主要在做几件事：

- 把 `r8169` 改造成可编译的外置 `r8169_xdp.ko`，把 `XDP_PASS`、`DROP`、
  `ABORTED`、非法 action、`adjust_tail(+16)` 和同设备 `XDP_TX` 这些路径
  真正跑到物理网卡上；
- 做 DNS eBPF cache，包括客户端/服务端缓存、pending flow、TTL、可信 DNS
  server 和 ringbuf 事件，并比较 tc、generic XDP 和 native XDP 的差异；
- 在 OpenStack、KVM、Kubernetes、OVS 环境里追踪 `virtio-net`、`tap`、`veth`、
  Bridge、Geneve/VXLAN 和 qrouter 的转发关系；
- 用外部 peer、驱动计数器、carrier 和普通连通性确认流量确实经过了物理
  RX/TX，而不是只在 veth 或虚拟机里得到一个“看起来成功”的结果。

## 项目

### [r8169-native-xdp](https://github.com/Yukinoshita03/r8169-native-xdp)

这是我最近单独拆出来的仓库，放的是 Linux `r8169` 的 Native XDP 外置驱动
补丁和源码。最开始只是想验证 XDP 能不能在物理网卡上真正跑起来，做到后面
才发现最费时间的是 buffer ownership、DMA、TX ring 和 reset 这些细节。

- 基于 Linux 7.2-rc6 提供 Native XDP RX/TX 核心补丁；
- 提供 Ubuntu 7.0 目标 ABI 的兼容、显式 PCI/BDF 保护和故障注入补丁；
- 处理 page-pool、DMA ownership、RX replacement、共享 TX ring 和 completion；
- 发布展开后的 `r8169_main.c` 等驱动源码、可复现构建脚本和验证记录；
- 在一张 RTL8168H/8111H 类物理网卡上完成 DNS cache `1024/1024` Native-XDP
  回包验收。

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

这是我的主线项目，也是很多实验的起点：一个面向虚拟化网络路径观测和轻量
服务加速的 Linux eBPF Agent。

- 发现并记录 `veth`、`tap`、Bridge、OVS 等虚拟路径和候选挂载点；
- 观测 DNS、gRPC、TCP、UDP 的路径、时延、服务分类和 attach 状态；
- 提供 DNS XDP cache、客户端/服务端缓存和 gRPC fast-cache 原型；
- 包含 `netns + bridge + veth` 可复现实验、C++20 用户态数据面和虚拟网卡
  驱动原型；
- 配套 OpenStack/Kubernetes/OVS 的路径探测、tc attach 和数据面实验文档。

### [MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase)

这是另一条线，一个正在开发中的现代 C++ 教学关系型数据库，架构参考
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

接下来还会继续做：

- `r8169_xdp` 的多轮 attach/detach、reset、link flap 和长时间压力验证；
- TX ring 满、RX refill 失败、DROP/ABORTED/invalid action 等故障路径；
- 物理网卡 Native XDP 与 OVS/tap/veth 观测面的边界；
- 可公开复现的构建、测试和性能数据。以后别人 clone 下来，至少能看懂我
  当时测了什么，而不是只能看到一张结果截图。

## 喜欢的动漫

我喜欢《Re:从零开始的异世界生活》（Re:Zero）和《我的青春恋爱物语果然有
问题》（春物），尤其喜欢雪之下雪乃。写代码写累了会看几集，或者把它们
当作深夜调试时的背景音。

<div align="center">
  <sub>慢一点没关系，先把问题弄明白，再把它做出来。</sub>
</div>
