# 第247题来源｜禅道 9.1.2 SQL

## 题库字段（本地资料，不计外部来源数）

- 题名：`zentaopms-9.1.2-sql SQL注入`
- 镜像：`vulfocus/zentaopms_9.1.2_sql`
- 题库端口：`80,3306`
- 无 CVE；未找到对应 CNVD。不是 16.5 登录框 CNVD-2022-42853。

## 外部来源（4 个唯一链接）

### [S1] 安骑士 / 安恒

- 链接：[禅道 getblockdata SQL](https://www.anquanke.com/post/id/160473)
- 用途：`block/main`、base64 `param`、`orderBy` 堆叠、outfile 示例。支撑步骤 1–2。

### [S2] 博客园 iamstudy

- 链接：[chandao_pentest_1](https://www.cnblogs.com/iamstudy/articles/chandao_pentest_1.html)
- 用途：Referer 校验、前台开放方法。支撑排坑。

### [S3] Docker Hub

- 链接：[vulfocus/zentaopms_9.1.2_sql](https://hub.docker.com/r/vulfocus/zentaopms_9.1.2_sql)
- 用途：与题库镜像对应。

### [S4] cn-sec 复述

- 链接：[禅道 9.1.2](https://cn-sec.com/archives/4384479.html)
- 用途：`mode=getconfig`、hex PREPARE sleep。支撑步骤 3。fofapro images README 仅作镜像名对照，与 Hub 重复则不另计。
