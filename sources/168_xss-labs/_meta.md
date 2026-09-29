# 第168题来源｜xss-labs

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/xss-labs`
- 镜像：`vulfocus/xss-labs`
- 题库端口：`80,3306`
- 无 CVE

## 外部来源（4 个唯一链接）

### [S1] 靶场源码

- 链接：[goodric/xss-labs](https://github.com/goodric/xss-labs)
- 用途：确认 `level1.php`–`level20.php` 文件布局。支撑「多关练习场」定位。原 c0ny1 仓库本次检索 404，用仍可访问的文件副本。

### [S2] 通关笔记

- 链接：[xss-labs通关笔记（一）](https://developer.cloud.tencent.com/article/1665021)
- 用途：Level1 `?name=<script>alert('xss')</script>`；Level2 改为 `keyword` 且需 `">` 闭合。支撑步骤 2–3。

### [S3] Level1–5 源码分析

- 链接：[XSS-labs Level 1-5](https://www.programmersought.com/article/32863879141/)
- 用途：`htmlspecialchars` / `str_replace` 差异，避免把 Level1 payload 套到后续关。

### [S4] Docker Hub

- 链接：[vulfocus/xss-labs](https://hub.docker.com/r/vulfocus/xss-labs)
- 用途：确认镜像存在。Hub 无关卡说明。
