# 第151题来源｜vulfocus/vulfocus-api

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/vulfocus-api`
- 镜像：`vulfocus/vulfocus-api:latest`
- 题库端口：`8000`
- 无 CVE/CNVD

## 外部来源（4 个唯一链接）

### [S1] Vulfocus 官方 docker-compose

- 链接：[docker-compose.yaml](https://github.com/fofapro/vulfocus/blob/master/docker-compose.yaml)
- 用途：确认 `vulfocus-api` 是平台后端服务，compose 不把它发布到宿主机端口；对外只有 `vulfocus-web` 的 80。支撑「非漏洞靶场、8000 不是对外入口」的结论。

### [S2] 官方安装说明

- 链接：[INSTALL.md](https://github.com/fofapro/vulfocus/blob/master/INSTALL.md)
- 用途：说明源码安装时 uWSGI 提供 `/api`、由 nginx 在 80 反代。支撑入口识别。

### [S3] 官方使用文档

- 链接：[Vulfocus 文档](https://fofapro.github.io/vulfocus/)
- 用途：说明平台用于编排漏洞镜像；Flag 写在漏洞环境内，不是平台 API 本身的利用目标。

### [S4] Docker Hub

- 链接：[vulfocus/vulfocus-api](https://hub.docker.com/r/vulfocus/vulfocus-api)
- 用途：确认镜像名存在。无漏洞复现说明。

## 检索结论

按题名 `vulfocus/vulfocus-api` 定向检索专业题解/PoC/CVE 公告，未找到该镜像对应的漏洞利用链。不把通用 Django/Docker 未授权访问套到本题。
