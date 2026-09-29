# 第228题来源｜Spring Boot Whitelabel 错误页 SpEL

## 题库字段（本地资料，不计外部来源数）

- 题名：`spring-boot-whitelabel-spel`
- 镜像：`vulfocus/spring-boot_whitelabel_spel`
- 题库端口：`9090`
- 无 CVE。勿与第144题 CVE-2016-4977 混淆。

## 外部来源（5 个唯一链接）

### [S1] LandGrey 利用清单

- 链接：[LandGrey/SpringBootVulExploit](https://github.com/LandGrey/SpringBootVulExploit)
- 用途：条件为 Boot 1.1.0–1.1.12、1.2.0–1.2.7、1.3.0；`/article?id=xxx` 触发 500 Whitelabel；`${7*7}` 回显 49；`Runtime.exec` + `byte[]`；demo 端口 **9091**。支撑步骤 1–3 与路径确认。

### [S2] 配套 EXP

- 链接：[xzajyjs/SpringBoot-whitelabel-error-rce-EXP](https://github.com/xzajyjs/SpringBoot-whitelabel-error-rce-EXP)
- 用途：同一原理（`PropertyPlaceholderHelper` / `ErrorMvcAutoConfiguration.resolvePlaceholder`）；目标示例 `http://127.0.0.1:9091/article?id=`。支撑入口。

### [S3] 版本边界（扫描插件）

- 链接：[Tenable WAS 112380](https://www.tenable.com/plugins/was/112380)
- 用途：Spring Boot &lt; 1.2.8 与 1.3.0；Whitelabel 把用户输入当 SpEL；升级 1.2.8 / 1.3.1。支撑版本排坑。

### [S4] 官方修复发布

- 链接：[Spring Boot 1.3.1 and 1.2.8 available now](https://spring.io/blog/2015/12/18/spring-boot-1-3-1-and-1-2-8-available-now)
- 用途：与 [S3] 引用的修复版本一致。支撑“无 CVE 编号、按发行说明修”。

### [S5] Vulfocus 竞赛镜像表

- 链接：[Vulfocus 靶场竞赛WP公布](https://www.nosec.org/home/detail/4944.html)
- 用途：题名 `spring-boot-whitelabel-spel` 对应 `vulfocus/spring-boot_whitelabel_spel:latest`。支撑镜像名。fofapro images/README 未列此条，以竞赛表为准。
