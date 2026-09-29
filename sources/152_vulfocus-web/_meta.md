# 第152题来源｜vulfocus/vulfocus-web

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/vulfocus-web`
- 镜像：`vulfocus/vulfocus-web:latest`
- 题库端口：`80`
- 无 CVE/CNVD

## 外部来源（4 个唯一链接）

### [S1] Vulfocus 官方 docker-compose

- 链接：[docker-compose.yaml](https://github.com/fofapro/vulfocus/blob/master/docker-compose.yaml)
- 用途：确认 `vulfocus-web` 是平台前端，compose 映射 `80:80`。

### [S2] 官方安装说明

- 链接：[INSTALL.md](https://github.com/fofapro/vulfocus/blob/master/INSTALL.md)
- 用途：安装与端口 80、平台登录说明。

### [S3] Docker Hub

- 链接：[vulfocus/vulfocus-web](https://hub.docker.com/r/vulfocus/vulfocus-web)
- 用途：确认镜像名。无漏洞复现说明。

### [S4] 官方使用文档

- 链接：[Vulfocus 文档](https://fofapro.github.io/vulfocus/)
- 用途：说明该组件是漏洞靶场的编排 UI，不是 CVE 环境。

## 检索结论

按题名 `vulfocus/vulfocus-web` 定向检索，未找到该镜像对应的专业漏洞题解或 PoC。不编造前端 XSS/未授权链。
