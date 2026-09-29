# 第136题来源｜OWASP Mutillidae II

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/mutillidae`
- 镜像：`vulfocus/mutillidae`
- 题库端口：`80,3306`
- 无 CVE；未找到可确认的 Vulfocus 本题镜像专属题解。卡片路径来自经典 Mutillidae II 文章，实际 context path 以首页链接为准。

## 外部来源（6 个唯一链接）

### [S1] OWASP 官方项目页

- 链接：[OWASP Mutillidae II](https://owasp.org/www-project-mutillidae-ii/)
- 用途：说明这是带 40+ 练习与内置 Hints 的训练应用，不是单一 CVE。支撑开头说明和按菜单解题。

### [S2] 官方仓库 README

- 链接：[webpwnized/mutillidae](https://github.com/webpwnized/mutillidae)
- 用途：Setup 一键恢复默认、可切换 secure/insecure、漏洞覆盖范围。支撑步骤 1–2。

### [S3] Irongeek 教程索引

- 链接：[Web Application Pen-testing Tutorials With Mutillidae](https://www.irongeek.com/i.php?page=videos/web-application-pen-testing-tutorials-with-mutillidae)
- 用途：webpwnized 分项视频目录（认证绕过、sqlmap、命令注入、LFI、XSS）。支撑步骤 5，不单独提供可复制路径。

### [S4] 登录 SQLi 复现

- 链接：[Mutillidae — SQLi: Bypass Authentication (Login)](https://inventyourshit.com/mutillidae-sqli-bypass-authentication-login/)
- 用途：`/mutillidae/index.php?page=login.php`、安全级别 0/1、用户名框 `admin' OR 1=1-- -`、POST 字段 `username`/`password`/`login-php-submit-button`。支撑步骤 2–3。

### [S5] 登录 SQLi 原理复现

- 链接：[hausec — SQLInjections](https://hausec.com/web-pentesting-write-ups/mutillidae/sqlinjections/)
- 用途：`' or 1=1 -- ` 必须留空格、用户枚举、指定 jeremy 要用括号条件。支撑步骤 3 与对应排坑。

### [S6] 命令注入复现

- 链接：[Mutillidae: Lesson 2: Command Injection Database Interrogation](https://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson2/index.html)
- 用途：菜单走到 DNS Lookup、`page=dns-lookup.php`、`www.cnn.com; uname -a`。支撑步骤 4。文中远程 MySQL 口令属于旧课环境，不作为本题凭据。
