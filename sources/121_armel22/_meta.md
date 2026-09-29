# 第121题来源｜vulfocus/armel22

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/armel22`
- 镜像：`vulfocus/armel22:latest`
- 题库端口：`5535`
- 无 CVE。Hub 描述为空。

## 外部来源（5 个唯一链接）

### [S1] Docker Hub 镜像页

- 链接：[vulfocus/armel22](https://hub.docker.com/r/vulfocus/armel22)
- 用途：确认镜像存在且无漏洞说明；内部端口以题库为准。支撑题目性质说明与端口排坑。

### [S2] 官方工具文档

- 链接：[Nmap Network Scanning — Port Scanning Basics](https://nmap.org/book/man-port-scanning-basics.html)
- 用途：端口扫描与服务识别命令参考。支撑步骤 1。

### [S3] 命令文档

- 链接：[uname(1), Linux man-pages](https://man7.org/linux/man-pages/man1/uname.1.html)
- 用途：`-m` 返回内核报告的机器类型。支撑步骤 2 与排坑。

### [S4] Debian 官方手册

- 链接：[dpkg(1)](https://manpages.debian.org/bookworm/dpkg/dpkg.1.en.html)
- 用途：`--print-architecture` 输出包架构名。支撑步骤 2 与排坑。

### [S5] Debian 官方 ARM 移植页

- 链接：[Debian ARM Ports](https://www.debian.org/ports/arm/)
- 用途：区分 armel（32 位 EABI 软浮点）、armhf、arm64。支撑步骤 3 与「不要套 armhf/arm64」排坑。
