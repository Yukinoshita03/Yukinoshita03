<div align="center">
  <a href="https://github.com/Kumampet/Aqours5thaniv">
    <img src="https://raw.githubusercontent.com/Kumampet/Aqours5thaniv/master/img/top_mamber.png" width="760" alt="Aqours" />
  </a>

  <h1>Hi, I'm Shuka</h1>

  <p>
    Graduate student at <b>Guilin University of Electronic Technology</b><br />
    Linux Networking · eBPF/XDP · Virtualized Dataplanes · C++ Systems
  </p>

  <p>
    <img src="https://img.shields.io/badge/Focus-Linux%20Dataplanes-0f766e?style=flat-square" alt="Linux Dataplanes" />
    <img src="https://img.shields.io/badge/Research-eBPF%20%2F%20XDP-111827?style=flat-square" alt="eBPF and XDP" />
    <img src="https://img.shields.io/badge/Engineering-Reproducible-2563eb?style=flat-square" alt="Reproducible Engineering" />
  </p>
</div>

## About Me

I am a first-year graduate student at **Guilin University of Electronic Technology**, originally from Chengdu, Sichuan. My current work sits at the intersection of kernel networking, cloud-native infrastructure, and performance engineering.

I am interested in a simple systems question: **how does a packet actually move through a virtualized host, and where can that path be observed or accelerated without making it unsafe?** I use Linux, eBPF/XDP, C/C++, and Go to build small, testable dataplanes around that question.

I care about clear boundaries, measurable behavior, safe fallback paths, and experiments that someone else can reproduce.

## What I Am Researching

- **eBPF/XDP dataplanes** for container and virtualized networking.
- **Packet-path observability** across `veth`, `tap`, Linux bridge, and OVS in KVM, OpenStack, and Kubernetes environments.
- **Kubernetes CNI fast paths**, including local and cross-node Pod forwarding, IPIP encapsulation, Service load balancing, SNAT, and connection tracking.
- **C++20 userspace packet processing** and a minimal Linux virtual NIC driver as lower-level dataplane components.
- **Reproducible network benchmarks** that make correctness, latency, and fallback behavior visible.

## Current Work

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

`vnet-dataplane` is a Linux eBPF agent for virtualized network-path observability and lightweight service acceleration.

- Discovers packet paths and candidate attach points across `veth`, `tap`, bridge, and OVS.
- Observes DNS, gRPC, TCP, and UDP traffic with path, latency, service classification, and attach-status information.
- Provides controlled DNS XDP cache and gRPC fast-cache prototypes.
- Includes reproducible `netns + bridge + veth` benchmarks, a C++20 userspace dataplane, and a minimal virtual NIC driver.

## Toolbox

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

## Current Direction

I am working toward systems and infrastructure engineering roles where Linux internals, network dataplanes, and performance-sensitive C++ matter. For now, the goal is to keep building, measuring, and turning low-level experiments into software that is understandable and repeatable.

<div align="center">
  <sub>I like Aqours. Their energy is a good reminder that meaningful progress is built one step at a time.</sub>
</div>
