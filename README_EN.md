<div align="center">
  <a href="https://github.com/Kumampet/Aqours5thaniv">
    <img src="https://raw.githubusercontent.com/Kumampet/Aqours5thaniv/master/img/top_mamber.png" width="760" alt="Aqours" />
  </a>

  <h1>Hi, I'm Kaiwen Tan</h1>

  <p>
    Graduate student at <b>Guilin University of Electronic Technology</b><br />
    Linux Kernel Networking · eBPF/XDP · Native NIC Drivers · Cloud Dataplanes · C++ Systems
  </p>

  <p>
    <img src="https://img.shields.io/badge/Focus-Linux%20Dataplanes-0f766e?style=flat-square" alt="Linux Dataplanes" />
    <img src="https://img.shields.io/badge/Research-eBPF%20%2F%20XDP-111827?style=flat-square" alt="eBPF and XDP" />
    <img src="https://img.shields.io/badge/Driver-r8169%20Native%20XDP-b91c1c?style=flat-square" alt="r8169 Native XDP" />
    <img src="https://img.shields.io/badge/Engineering-Reproducible-2563eb?style=flat-square" alt="Reproducible Engineering" />
  </p>

  <p>
    <a href="./README.md">中文</a> · <b>English</b>
  </p>
</div>

## About Me

I am a second-year graduate student at **Guilin University of Electronic
Technology**, originally from Chengdu, Sichuan. My work focuses on Linux kernel
networking, physical-NIC dataplanes, cloud-native infrastructure, and systems
performance.

I like following a packet through its complete lifecycle: from a VM or
container, through `virtio`, `tap`, `veth`, Linux bridge, OVS, and VXLAN/Geneve,
to the physical NIC—and then asking where that path can be observed, verified,
or accelerated without losing control of its failure modes.

Recently I moved from eBPF programs and virtual-path observability in
`vnet-dataplane` to an out-of-tree Native-XDP `r8169` driver. That work involves
RX-buffer ownership, page pools, DMA synchronization, TX completion, and
same-device `XDP_TX`, with a physical DNS-cache validation run reaching
1024/1024 external replies.

I care about clear boundaries, measurable behavior, reproducible experiments,
and explicit recovery conditions for experiments that can interrupt a network
interface.

## Recent Work

- **Native-XDP NIC driver**: extending `r8169` into a buildable external
  `r8169_xdp.ko` with `XDP_PASS`, `DROP`, `ABORTED`, invalid-action handling,
  `adjust_tail(+16)`, and same-device `XDP_TX`.
- **DNS eBPF acceleration**: server/client caches, pending flows, TTLs, trusted
  DNS servers, ring-buffer events, and comparisons between tc, generic XDP, and
  native XDP paths.
- **Virtualized network paths**: packet-flow analysis across `virtio-net`,
  `tap`, `veth`, bridge, OVS, Geneve/VXLAN, and router namespaces in OpenStack,
  KVM, and Kubernetes environments.
- **Reproducible acceptance**: external-peer traffic, driver counters, carrier
  state, and ordinary connectivity checks that exercise the physical RX/TX path
  instead of only producing a successful veth or VM result.

## Projects

### [r8169-native-xdp](https://github.com/Yukinoshita03/r8169-native-xdp)

An out-of-tree Native-XDP patch set and source repository for Linux `r8169`.

- Core Native-XDP RX/TX patches based on Linux 7.2-rc6;
- Ubuntu 7.0 target-ABI compatibility, explicit PCI/BDF protection, and
  test-only fault-injection patches;
- RX page-pool ownership, DMA synchronization, replacement buffers, shared TX
  rings, and completion handling;
- Expanded `r8169` source snapshots, reproducible build scripts, and validation
  notes;
- A physical RTL8168H/8111H-class acceptance run with 1024/1024 DNS cache-hit
  replies.

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

A Linux eBPF agent for virtualized network-path observability and lightweight
service acceleration.

- Discovers packet paths and candidate attach points across `veth`, `tap`,
  bridge, and OVS;
- Observes DNS, gRPC, TCP, and UDP paths, latency, service classification, and
  attach state;
- Provides DNS XDP cache, client/server cache, and gRPC fast-cache prototypes;
- Includes reproducible `netns + bridge + veth` experiments, a C++20 userspace
  dataplane, and a virtual NIC driver prototype;
- Documents OpenStack/Kubernetes/OVS path probes, tc attach checks, and dataplane
  experiments.

### [MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase)

A modern C++ educational relational database under development, inspired by
Stanford RedBase and organized with lessons from OceanBase MiniOB.

- C++20, CMake, and cross-platform CI;
- Planned Page, Buffer Pool, LRU, Heap File, Tuple, RID, B+ Tree, and Catalog
  components;
- A simplified SQL parser and Volcano execution model for basic CRUD;
- The project scaffold, CLI entry point, and smoke tests are in place while the
  database internals are still being implemented.

## Toolbox

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

## Current Direction

I am working toward systems and infrastructure engineering roles where Linux
networking internals, NIC drivers, eBPF/XDP, OpenStack/Kubernetes dataplanes,
and performance-sensitive C++ matter.

Next, I want to deepen:

- multi-cycle attach/detach, reset, link-flap, and long-running validation for
  `r8169_xdp`;
- TX-ring-full, RX-refill, DROP/ABORTED/invalid-action, and other fault paths;
- the boundary between physical-NIC Native XDP and OVS/tap/veth observability;
- publicly reproducible build, test, and performance evidence.

<div align="center">
  <sub>I like Aqours. Meaningful progress is built one step at a time.</sub>
</div>
