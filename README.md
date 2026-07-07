<div align="center">
  <table>
    <tr>
      <td width="280" align="center" valign="middle">
        <img src="./assets/yukino-source.png" width="260" alt="Yukinoshita Yukino illustration" />
      </td>
      <td align="left" valign="middle">
        <h1>Shuka</h1>
        <p>
          I am a first-year graduate student at <b>Guilin University of Electronic Technology</b>.<br/>
          I come from <b>Chengdu, Sichuan</b>.<br/>
          I focus on systems, infrastructure, and the small details that decide whether an experiment is actually reproducible.
        </p>
        <p>
          <sub>If I have to introduce myself, I prefer to keep it precise.</sub>
        </p>
      </td>
    </tr>
  </table>
</div>

<div align="center">
  <img src="https://img.shields.io/badge/Focus-Systems%20%26%20Infrastructure-f6cfe0?style=flat-square" />
  <img src="https://img.shields.io/badge/Style-Quiet%20%26%20Precise-c8d8ff?style=flat-square" />
  <img src="https://img.shields.io/badge/Approach-Readable%20%26%20Reproducible-e7d9ff?style=flat-square" />
</div>

<br />

> I care about careful engineering, reproducible results, and explanations that do not hide the cost.

## About Me

- Interested in **Linux, containers, storage, networking, and system performance**.
- Mainly write **Go**, and also use **C / C++ / Python / Shell** for tools and experiments.
- Prefer reproducible measurements over vague claims.
- Usually start from boundaries, tradeoffs, and failure cases before talking about results.
- I like quiet pages, clear code, and projects that can be run again by someone else.

## Currently Working On

- Building [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane), a systems and infrastructure project for Linux virtualized network path observability and lightweight eBPF acceleration.
- Studying asynchronous I/O in **gVisor / sandbox** scenarios, especially boundary conditions and fallback paths.
- Organizing **paper experiments** and benchmark harnesses so that claims are backed by reproducible data.
- Reading implementations of **container runtimes**, **file systems**, and **storage systems** to understand why they are shaped the way they are.

## Maintained Project

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

`vnet-dataplane` is a Linux eBPF agent for virtualized network path observability and lightweight service acceleration.

- Discovers virtualized network paths and candidate eBPF attach points such as `veth`, `tap`, `bridge`, and `OVS`.
- Observes DNS, gRPC, TCP, and UDP traffic with path, latency, service classification, and attach-status output.
- Provides DNS XDP cache, gRPC fast-cache, and `netns + bridge + veth` benchmark prototypes.
- Keeps a virtual NIC driver and C++ userspace dataplane as lower-level experimental components.

<div align="center">

![C++](https://img.shields.io/badge/C++20-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-networking-FCC624?style=flat-square&logo=linux&logoColor=111827)
![eBPF](https://img.shields.io/badge/eBPF-XDP%20%2F%20tc-111827?style=flat-square&logo=linux&logoColor=white)
![Infrastructure](https://img.shields.io/badge/Infrastructure-observability%20%26%20acceleration-e7d9ff?style=flat-square)

</div>

## Yukino Fragments

<div align="center">
  <img src="./assets/gifs/yukino-1.gif" width="220" alt="Yukino gif 1" />
  <img src="./assets/gifs/yukino-2.gif" width="220" alt="Yukino gif 2" />
  <img src="./assets/gifs/yukino-3.gif" width="220" alt="Yukino gif 3" />
</div>

<div align="center">
  <sub>Quiet, restrained, but not empty.</sub>
</div>

## Reol

<div align="center">
  <img src="https://i.makeagif.com/media/4-19-2026/qI99YS.gif" width="260" alt="Reol MV clip" />
</div>

<div align="center">
  <sub>I like Reol, especially the clean and sharp tension in these short clips.</sub>
</div>

## Tech I Use

<div align="center">

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=111827)
![C](https://img.shields.io/badge/C-1f2937?style=for-the-badge&logo=c&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![eBPF](https://img.shields.io/badge/eBPF-111827?style=for-the-badge&logo=linux&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)

</div>

## Current State

- Continuing systems research and infrastructure engineering practice.
- Keeping experiments reproducible, explainable, and reviewable.
- Building projects with a bias toward clear boundaries and measurable behavior.
- Not loud, but still moving.

<div align="center">
  <sub>Slow progress is still progress, as long as it is real.</sub>
</div>
