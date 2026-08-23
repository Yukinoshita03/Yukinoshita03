<div align="center">
  <a href="https://github.com/Yukinoshita03/Yukinoshita03">
    <img src="./assets/yukino-code-hero-4k.png" width="760" alt="雪之下雪乃在深夜写代码" />
  </a>

  <h1>你好，我是谭开文 👋</h1>

  <p>
    四川成都人，现在在桂林电子科技大学读研二。<br />
    最近基本都在折腾 Linux 网络、eBPF/XDP、网卡驱动和云平台数据面。
  </p>

  <p>
    <b>中文</b> · <a href="./README_EN.md">English</a>
  </p>
</div>

## 我最近在折腾什么

我最想弄明白的问题一直很直接：**一个包到底从哪里进来，经过了什么，为什么会慢，
又能不能在不破坏原路径的情况下把它加速。**

所以我最近做的东西，基本都围绕下面这条路径展开：

```text
物理网卡 → 驱动 / NAPI → XDP → Linux 网络栈
       → tap / veth → OVS → VM / Pod → 后端服务
```

我不太满足于“代码能编译”或者“在 veth 里跑通”。功能写完以后，我一般还会把它放到
真实网卡、OpenStack 虚拟机或者 Kubernetes Pod 里继续跑，看看 QPS、p95/p99、CPU、
丢包和失败路径到底怎么样。结果不对，就继续往 softirq、tap、OVS、DMA 或驱动里查。

现在主要在啃三块：

- **把重复请求提前回答掉**：在 XDP/tc 上解析协议，命中缓存就直接回包，没命中继续走
  原来的 Linux、OVS 和后端服务；
- **把 XDP 真正放进网卡驱动**：不只测 generic XDP，还会继续追 RX buffer、page-pool、
  DMA ownership、TX ring 和 completion；
- **把实验放进真实云网络**：研究 `tap`、`veth`、OVS、Geneve/VXLAN、VM 和 Pod 之间的
  完整路径，而不是只拿一个隔离 netns 的数字下结论。

## 几个我比较想拿出来讲的项目

### [eBPF Network Service Cache](https://github.com/Yukinoshita03/ebpf-network-service-cache)

这是我现在投入最多的项目。思路其实不复杂：对于答案已经知道、而且能明确判断是否过期的
请求，直接在 XDP 快路径里响应；遇到未知请求、过期项或者解析失败，就原样放行。

目前做了 DNS、通用 UDP、ARP、DHCP、gRPC 和 LDAP/LDAPS 等协议原型，也做了
OpenStack TAP 和 Kubernetes Pod-veth 的适配。它不会替换应用、CNI 或 OVS，挂错了可以
卸载，没命中也还能继续走原来的网络路径。

我比较在意的不只是“快了多少”，还包括双方缓存容量是否一致、流量分布是不是同一套、
失败率和丢包是不是为零，以及 netns 微基准和 VM 端到端结果有没有被混在一起。

### [r8169 Native XDP](https://github.com/Yukinoshita03/r8169-native-xdp)

这个项目一开始只是想验证：XDP 能不能不靠 generic 模式，直接在一张真实的 Realtek 网卡
驱动里跑起来。做到后面就一路追到了 RX buffer ownership、DMA 同步、page-pool、TX ring、
reset 和 link flap。

现在已经实现 `XDP_PASS`、`XDP_DROP`、`XDP_ABORTED` 和同网卡 `XDP_TX`，并在真实网卡上
完成过外部 DNS cache-hit 回包验证。这个仓库我会明确写出硬件、内核和安全边界，不会把
一张网卡上的实验结果说成所有机器都能直接用。

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

这是很多实验最早的总仓库。它会发现 `veth`、`tap`、Bridge、OVS 等路径，观察 DNS、
gRPC、TCP/UDP 流量，并提供一些 XDP/tc 快路径原型。这里还放着 C++20 用户态数据面和
虚拟网卡驱动实验，比较像我的 Linux 网络试验场。

### [campus-net-guard](https://github.com/Yukinoshita03/campus-net-guard)

这是从实际问题里拆出来的小工具：用 C++/libcurl 定时检查校园网是否还在线，掉线后按
Dr.COM 门户参数自动认证，再重新确认网络有没有恢复。它现在有 Linux systemd 部署、
macOS/Linux CI 和本地 mock 回归测试，真实账号和密码不会放进仓库。

## 我做项目时比较在意什么

- **先把路径搞清楚**：程序挂在哪里、包经过哪里、谁拥有这块内存，先说明白再谈优化；
- **命中快，没命中也得安全**：快路径只处理能证明正确的请求，其他情况回到原路径；
- **结果要能复现**：保留构建环境、测试命令、CPU/网卡信息、流量模型和原始结果；
- **负面结果也有用**：性能没提升、尾延迟变差或者出现丢包时，继续找原因，不只挑好看的数字；
- **尽量放到真环境里测**：netns 适合定位问题，但最后还是要回到真实网卡、VM、Pod 和 OVS。

## 平时会用的东西

- 主要写 **C/C++（C++20）**，也用 Go 和 Python 写控制面、测试工具和自动化脚本；
- 常用 Linux、eBPF/XDP、tc、NAPI、KVM、OVS、OpenStack、Kubernetes 和 Docker；
- 构建和排障会用 CMake、Make、Git、GDB、Clang/GCC、Shell、perf、bpftool、tcpdump；
- Rust 还在学，希望以后能拿它写一些更稳的系统工具。

## 接下来

我想继续往 Linux 内核网络、eBPF/XDP、网卡驱动、云基础设施和高性能 C++ 这条线走。
比起只写业务接口，我更喜欢能接触真实机器、真实数据面，还能一路把问题查到内核和驱动的工作。

如果你也在做这些方向，欢迎一起交流代码、实验和那些“看起来不该出问题，但它就是出问题了”
的网络现场。

## 题外话

我喜欢《Re:从零开始的异世界生活》和《我的青春恋爱物语果然有问题》，尤其喜欢雪之下雪乃。
这个 GitHub 名字也是这么来的。
