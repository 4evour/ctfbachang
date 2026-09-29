# 第122题来源｜vulfocus/bwapp

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/bwapp`
- 镜像：`vulfocus/bwapp:latest`
- 题库端口：`80,3306`
- 无 CVE。Hub 描述为空。

## 外部来源（4 个唯一链接）

### [S1] 官方项目站点

- 链接：[ITSEC Games — bWAPP](http://www.itsecgames.com/)
- 用途：确认 bWAPP 是含 100+ Web 漏洞的教学应用，覆盖 OWASP Top 10，不是单一 CVE。支撑题目性质与「按 portal 清单逐项做」。

### [S2] 官方安装说明

- 链接：[bWAPP - Installation](http://itsecgames.blogspot.com/2013/01/bwapp-installation.html)
- 用途：`install.php` 初始化数据库、登录页、默认凭据 `bee`/`bug`。支撑步骤 1–3 与安装/口令排坑。

### [S3] 安装与练习入口对照

- 链接：[Installation & configuration of bWAPP tutorial — Part 1](https://infosecwriteups.com/installation-configuration-bwapp-tutorial-part-1-7984ac4f8c84)
- 用途：对照 `install.php?install=yes`、登录 `bee`/`bug`、以及随后将 severity 设为 low。支撑步骤 1–3。文中 Docker 部署不等于 Vulfocus 镜像配置。

### [S4] Docker Hub 镜像页

- 链接：[vulfocus/bwapp](https://hub.docker.com/r/vulfocus/bwapp)
- 用途：确认题库镜像存在且无专属 WP/账号说明；内部端口以题库为准。
