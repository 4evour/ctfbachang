# 第235题来源｜vulfocus/pikachu

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/pikachu`
- 镜像：`vulfocus/pikachu`
- 题库端口：`80,3306`
- 无 CVE。

## 外部来源（5 个唯一链接）

### [S1] Docker Hub

- 链接：[vulfocus/pikachu](https://hub.docker.com/r/vulfocus/pikachu)
- 用途：镜像存在、无 overview。

### [S2] zhuifengshaonianhanlu/pikachu

- 链接：[GitHub](https://github.com/zhuifengshaonianhanlu/pikachu)
- 用途：初始化提示、左侧漏洞菜单。支撑步骤 1–2。

### [S3] README

- 链接：[README.md](https://raw.githubusercontent.com/zhuifengshaonianhanlu/pikachu/master/README.md)
- 用途：项目说明。支撑定位。

### [S4] issue #12

- 链接：[issues/12](https://github.com/zhuifengshaonianhanlu/pikachu/issues/12)
- 用途：`admin`/`123456` 出现在练习表单（如 xss_reflected_post），不是门户登录。支撑排坑。

### [S5] issue #39 与初始化文档合并计数时：保留 cn-sec 文作为 [S5]

- 链接：[vulfocus/pikachu 初始化](https://cn-sec.com/archives/3364546.html)
- 用途：记录 `vulfocus/pikachu` 与初始化点击。支撑步骤 1。

`zhuzhichao/pikachu` 检索 404，不计来源。issue #39 未单列以免与菜单说明重复。
