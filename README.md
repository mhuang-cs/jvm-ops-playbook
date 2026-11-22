# jvm‑ops‑playbook

> 聚焦线上高频 JVM 稳定性故障，基于原生单文件 `.java` 复现故障现场，配合 `jcmd`、Unified GC Logging (`-Xlog`)、`jstack`、`Arthas` 与 `Eclipse MAT` 完成现象观测与根因定位，并通过工程化代码改造（如 Maven + Caffeine）完成修复验证的完整闭环。

## 实验环境

- **OS**: macOS (Apple Silicon / Intel)
- **JDK**: OpenJDK 21 (Azul Zulu 21.0.13, via SDKMAN!)
- **默认 GC**: G1
- **诊断工具**: `jcmd`（替代传统 `jps` / `jstat` / `jmap`） / Unified GC Logging (`-Xlog`) / `jstack` / `Arthas` / `Eclipse MAT`

## 实战案例导航

| 编号 | 故障场景 | 核心异常 / 现象 | 核心排查手段 | 详细实录 |
| :--- | :--- | :--- | :--- | :--- |
| 01 | 堆内存溢出 | `OutOfMemoryError: Java heap space` | `jcmd` + `-Xlog` + `HeapDump` + `Eclipse MAT` | [查看排查实录](./01-heap-oom/README.md) |
| 02 | CPU 飙升与线程死锁 | CPU 占用 200%+ 且业务线程永久阻塞 | `ps -M` / `Arthas thread` + `jstack` | [查看排查实录](./02-high-cpu-deadlock/README.md) |
| 03 | 元空间溢出 | `OutOfMemoryError: Metaspace` | `jstat -gcmetacapacity` + `Arthas classloader` | [查看排查实录](./03-metaspace-oom/README.md) |
