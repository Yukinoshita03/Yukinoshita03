<div align="center">
  <a href="https://github.com/Yukinoshita03/Yukinoshita03">
    <img src="./assets/yukino-code-hero-4k.png" width="760" alt="Yukino Yukinoshita programming at night" />
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
Technology**, originally from Chengdu, Sichuan. My laptop usually has a few VMs,
too many terminals, and at least one packet capture open. Most of what I work on
comes back to Linux networking, cloud-native infrastructure, and performance-
sensitive C++.

I keep getting pulled into one question: **how does a packet actually get where
it is going?** It may cross `virtio`, `tap`, `veth`, a bridge, and OVS, pick up a
VXLAN/Geneve envelope, and only then reach the physical NIC. I like taking that
path apart, finding the places that are observable, verifiable, and genuinely
worth accelerating.

Recently I pushed the eBPF/XDP experiments in `vnet-dataplane` down to a physical
NIC and split the driver work into `r8169-native-xdp`. That meant following RX
buffer ownership, page pools, DMA synchronization, TX completion, and `XDP_TX`
all the way through, then running 1024/1024 external DNS-cache requests on real
hardware.

I am not very satisfied with “it compiles” or “it works in a veth namespace.” I
want to know whether it holds on the real path, where it breaks, and whether the
breakage can be explained. That is why I keep the build inputs, test commands,
counters, and failure boundaries with the result.

## Research Areas

I am mainly working along three connected tracks:

- **Linux kernel networking and NIC drivers**: RX/TX, DMA, page pools, NAPI,
  driver lifecycles, and what Native XDP actually does on a real adapter;
- **eBPF/XDP dataplanes**: DNS caching, traffic observability, and narrow fast
  paths, with comparisons between tc, generic XDP, and native XDP;
- **Virtualized and cloud-native networking**: KVM, OpenStack, Kubernetes, OVS,
  `virtio`, `tap`, `veth`, VXLAN/Geneve, and router namespaces.

I also use C++ to study storage, indexing, and query execution through
[MiniRedBase](https://github.com/Yukinoshita03/MiniRedBase).

## Roles I Am Looking For

I am looking for roles involving Linux kernel networking, eBPF/XDP, NIC drivers,
cloud-native infrastructure, or high-performance C++ systems.

I prefer low-level infrastructure work where I can touch real machines and
dataplanes, write production code, measure performance, and investigate failure
modes. A team that combines engineering delivery with room for systems research
and experiments would be a particularly good fit.

## Languages and Toolbox

- **Most used**: C/C++ (mostly C++20), Go, and Python;
- **Currently learning**: Rust, especially for systems tools and infrastructure;
- **Systems and networking**: Linux, KVM, eBPF/XDP, TC, NAPI, NIC drivers, OVS,
  OpenStack, Kubernetes, and Docker;
- **Engineering tools**: CMake, Make, Git, GDB, Clang/GCC, Shell, and reproducible
  `netns`/bridge/`veth` test environments.

## Recent Work

- **The Native-XDP NIC driver is currently the rabbit hole**: extending `r8169`
  into a buildable external `r8169_xdp.ko` with `XDP_PASS`, `DROP`, `ABORTED`,
  invalid-action handling, `adjust_tail(+16)`, and same-device `XDP_TX`.
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

This is the repository I recently split out for the Linux `r8169` Native-XDP
driver. It started as “make XDP really run on a physical NIC” and quickly became
an exercise in buffer ownership, DMA, TX rings, and reset paths.

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

This is the main project and the starting point for most of the experiments: a
Linux eBPF agent for virtualized network-path observability and lightweight
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

This is a separate track: a modern C++ educational relational database under
development, inspired by
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

I want to keep following the systems and infrastructure path, and connect Linux
networking internals, NIC drivers, eBPF/XDP, OpenStack/Kubernetes dataplanes, and
performance-sensitive C++ into one coherent toolbox.

Next I want to keep digging into:

- multi-cycle attach/detach, reset, link-flap, and long-running validation for
  `r8169_xdp`;
- TX-ring-full, RX-refill, DROP/ABORTED/invalid-action, and other fault paths;
- the boundary between physical-NIC Native XDP and OVS/tap/veth observability;
- publicly reproducible build, test, and performance evidence. If someone clones
  a project later, I want them to know what I actually measured—not just see a
  polished result screenshot.

## Anime I Like

I like *Re:ZERO -Starting Life in Another World-* and *My Youth Romantic Comedy
Is Wrong, As I Expected* (Oregairu), especially Yukino Yukinoshita. They are
good background company for late-night debugging sessions.

<div align="center">
  <sub>It is fine to move slowly; understand the problem first, then build it.</sub>
</div>
