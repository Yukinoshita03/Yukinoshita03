<div align="center">
  <table>
    <tr>
      <td width="280" align="center" valign="middle">
        <img src="./assets/yukino-source.png" width="260" alt="Yukinoshita Yukino illustration" />
      </td>
      <td align="left" valign="middle">
        <h1>雪之下雪乃 / Shuka</h1>
        <p>
          我叫雪之下雪乃。<br/>
          来自 <b>四川成都</b>，就读于 <b>桂林电子科技大学</b>。<br/>
          目前<b>研究生一年级在读</b><br/>
          不太擅长把自己说得很热闹，不过，做事还算认真。
        </p>
        <p>
          <sub>如果一定要给自己一个说明，那就写得清楚一点吧。</sub>
        </p>
      </td>
    </tr>
  </table>
</div>

<div align="center">
  <img src="https://img.shields.io/badge/Focus-Systems%20%26%20Infrastructure-f6cfe0?style=flat-square" />
  <img src="https://img.shields.io/badge/Style-Yukino%20%E2%80%94%20Cold%20%26%20Calm-c8d8ff?style=flat-square" />
  <img src="https://img.shields.io/badge/Approach-Readable%20%26%20Reproducible-e7d9ff?style=flat-square" />
</div>

<br />

> 我会认真做事，也会认真喜欢可爱的东西。  
> 只是，我不太喜欢把这种事说得太大声。

## 关于我

- 关注 **Linux、容器、存储、网络、系统性能** 这些更接近底层的方向。
- 主要使用 **Go**，也会写 **C / Python / Shell**，做工具，也做实验。
- 我更相信可复现的结果，而不是漂亮但空泛的描述。
- 不太喜欢把话说满，通常会先把边界、成本和收益讲清楚。
- 页面看起来安静一些，不是因为我没想法，而是我觉得这样更合适。

## 雪之下的片段

<div align="center">
  <img src="./assets/gifs/yukino-1.gif" width="220" alt="Yukino gif 1" />
  <img src="./assets/gifs/yukino-2.gif" width="220" alt="Yukino gif 2" />
  <img src="./assets/gifs/yukino-3.gif" width="220" alt="Yukino gif 3" />
</div>

<div align="center">
  <sub>安静、克制、但并不无趣。</sub>
</div>

## Reol

<div align="center">
  <img src="https://i.makeagif.com/media/4-19-2026/qI99YS.gif" width="260" alt="Reol MV clip" />
</div>

<div align="center">
  <sub>我很喜欢 Reol，更喜欢这种干净一点、张力也更足的片段。</sub>
</div>

<div align="center">
  <sub>主页里这段短循环只是留一点气氛。</sub>
</div>

## 最近在做

- 做一个偏系统和基础设施方向的开源项目：[vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)。它面向 Linux 虚拟化网络路径，使用 eBPF / XDP / tc 观测 `veth`、`tap`、`bridge`、`OVS` 等路径上的 DNS、gRPC 和 TCP/UDP 流量，并尝试在可控场景下做轻量快路径优化。
- 研究 **gVisor / sandbox** 场景下的异步 I/O，尤其是它的边界和退化条件。
- 整理 **论文实验** 和 **benchmark harness**，把每个结论都落到可复现的数据上。
- 读 **容器运行时**、**文件系统**、**存储系统** 的实现，顺手理解它们为什么会那样工作。
- 把实验结果整理成能复现、能解释、也能顺利写进论文的形式。

## 正在维护的项目

### [vnet-dataplane](https://github.com/Yukinoshita03/vnet-dataplane)

一个面向 Linux 虚拟化网络路径的 eBPF 观测与轻量加速项目。

- 发现 `veth`、`tap`、`bridge`、`OVS` 等虚拟化网络路径和候选挂载点。
- 观测 DNS、gRPC、TCP/UDP 流量，输出路径、延迟、服务分类和 eBPF 挂载状态。
- 提供 DNS XDP cache、gRPC fast-cache、`netns + bridge + veth` benchmark 等实验能力。
- 保留虚拟网卡驱动和 C++ userspace dataplane 作为底层实验组件。

<div align="center">

![C++](https://img.shields.io/badge/C++20-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-networking-FCC624?style=flat-square&logo=linux&logoColor=111827)
![eBPF](https://img.shields.io/badge/eBPF-XDP%20%2F%20tc-111827?style=flat-square&logo=linux&logoColor=white)
![Infrastructure](https://img.shields.io/badge/Infrastructure-observability%20%26%20acceleration-e7d9ff?style=flat-square)

</div>

## 我常用的技术

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

## 现在的状态

- 继续推进系统方向的研究和工程实践。
- 保持输出可复现、可解释、可复查。
- 想把主页做得更像“安静一点、可爱一点”的感觉。
- 不是很吵，但也不会太冷。

<div align="center">
  <sub>ゆっくりでも、ちゃんと進める。たぶん、それで十分。</sub>
</div>
