# Arm 64位 Debian 环境

> **题目性质：**环境/架构识别，不是已知 CVE 利用题。题库镜像为 `vulfocus/armhf22:latest`，内部端口 `5535`。[S1]

## 操作步骤

1. 识别 5535 端口上开放的服务：[S2]

```bash
nmap -Pn -sV -p 5535 <IP>
nc -nv <IP> 5535
```

按识别出的协议使用题目提供的入口信息连接；不要仅凭端口号猜服务或凭据。

2. 获得题目允许的 shell 后，确认运行系统和架构：[S3][S4]

```bash
uname -a
uname -m
cat /etc/os-release
dpkg --print-architecture
```

3. 按运行时输出选择对应架构的程序；不要只凭题名中的“Arm 64位”决定使用 ARM64 文件。[S3][S4]

## 本题特有排坑

- `uname -m` 输出的是内核报告的机器类型；`dpkg --print-architecture` 输出 Debian 包管理器的架构名，两者名称可能不同，结合判断。[S3][S4]
- 5535 是题库给出的内部端口；实际连接时使用 Vulfocus 映射端口。[S1]

## 来源

- **[S1] 镜像/端口：**[Docker Hub vulfocus/armhf22](https://hub.docker.com/r/vulfocus/armhf22) — 镜像资料；题库端口以本地 `vulfocus_知识库.csv` 为准。
- **[S2] 官方工具文档：**[Nmap Network Scanning — Port Scanning Basics](https://nmap.org/book/man-port-scanning-basics.html) — 端口扫描与服务识别的命令参考。
- **[S3] 命令文档：**[uname(1), Linux man-pages](https://man7.org/linux/man-pages/man1/uname.1.html) — `-m` 返回机器硬件类型。
- **[S4] Debian 官方手册：**[dpkg(1)](https://manpages.debian.org/bookworm/dpkg/dpkg.1.en.html) — `--print-architecture` 输出 dpkg 使用的包架构。

来源清单见 [`../sources/005_arm64_debian_env/_meta.md`](../sources/005_arm64_debian_env/_meta.md)。
