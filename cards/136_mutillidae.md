# 136｜OWASP Mutillidae II 综合漏洞练习

> **先走应用菜单：**按本实例左侧 OWASP Top 10 / 练习页逐项处理；先做登录 SQL 注入、DNS Lookup 命令注入，再用页面自带 Hints。Mutillidae II 是多漏洞训练应用，不是单一 CVE。[S1][S2][S3]

> 题库镜像：`vulfocus/mutillidae`；题库端口 `80,3306`。未找到该 Vulfocus 镜像的专属 WP，以下路径来自经典 OWASP Mutillidae II 复现；先从首页链接确认实际 context path（公开材料常见 `/mutillidae/`）。`3306` 是 MySQL，不是 Web 入口。

## 操作步骤

1. 打开 `http://<IP>:80/`。若首页或跳转带 `/mutillidae/`，后续一律用该前缀；否则按页面实际链接复制。公开复现入口是 `http://<IP>/mutillidae`。[S2][S4][S6]

2. 先看页面上的 **Setup / Reset DB**。官方项目用一键 Setup 把库恢复到默认；库未初始化或被改乱时，先点它再做登录类题目。再把安全级别调到 **0（Hosed / insecure）**；级别 1 会在浏览器端拦截引号，要改请求体才能复现同一条注入。[S2][S4]

3. 打开内置 Hints（经典版本 Cookie `showhints=1`）。按菜单做登录绕过，不要另造一条通用 SQLi：[S4][S5]

   - 菜单走到登录页。公开复现 URL 是 `/mutillidae/index.php?page=login.php`。[S4]
   - 用户名框先提交单引号，确认是否出现 SQL 语法错误。[S4][S5]
   - 用户名填已知账号（如 `admin`）、密码留空：若回“密码错误”而不是“账号不存在”，说明用户枚举成立；公开材料里 `Jeremy`/`jeremy` 同样可枚举。[S4][S5]
   - 在**用户名**框提交下面字符串，密码填任意值。`--` 后面必须留空格，否则注释吃掉后续 SQL 会语法失败：[S5]

```text
' or 1=1 -- 
```

公开复现也会用 `admin' OR 1=1-- -`。成功时进已登录会话（常见为库中第一条账号，多为 admin）。要指定用户，用户名用 `' or (1=1 and username = 'jeremy') -- `，不要只写 `' or 1=1 -- ` 再填 jeremy——后者仍会落到第一条记录。[S4][S5]

4. 再做命令注入（同一应用的另一项，不是登录题的后续）：菜单 **OWASP Top 10 → XSS / Reflected → DNS Lookup**，地址栏应对应 `page=dns-lookup.php`。Hostname/IP 先提交正常主机名确认 nslookup 有回显，再在后面接 `;` 与系统命令，例如 `www.cnn.com; uname -a`。成功时页面同时出现 DNS 结果和命令输出。[S6]

5. 其余项按左侧清单和 Hints 做（反射/存储 XSS、文件包含、HTML 注入等）。Irongeek 收录了 webpwnized 的分项视频（认证绕过、sqlmap、命令注入、LFI、XSS），以**本实例菜单和 Hints**为准，不要把视频里的旧路径硬套过来。[S1][S3]

## 这题特有的排坑

- **context path 不同：**公开复现常见 `/mutillidae/`；Vulfocus 本题镜像未由专属 WP 证实。从首页链接复制前缀后再访问 `index.php?page=login.php`、`dns-lookup.php`。[S4][S6]
- **先降安全级别：**级别 0 才能在表单里直接打引号；级别 1 要拦截登录 POST（`username` / `password` / `login-php-submit-button=Login`）再改用户名，不能只看前端报错就换 payload。[S4]
- **登录注入打用户名框，`--` 后留空格；**指定用户必须把 `username='...'` 放进括号条件，否则 `OR 1=1` 仍登录第一条。[S5]
- **命令注入入口是 DNS Lookup 的 `target_host`，**不是登录框。分隔符用 `;`（公开课也测 `|` / `||` / `&` / `&&`）；只提交主机名没有命令输出不等于失败。[S6]
- **`3306` 不是本题 Web 打法。**旧 SamuraiWTF 课里出现过远程连库的演示口令，不能当成 Vulfocus 镜像的 MySQL 密码。[S6]
- 每做完一项看 Hints/菜单是否指向下一项；不要把单一 SQLi 或命令注入写成整题唯一解。[S1][S2]

## 来源

- **[S1] 官方资料：**[OWASP Mutillidae II](https://owasp.org/www-project-mutillidae-ii/) — 应用性质、40+ 练习、内置 Hints/教程；支持开头说明与按菜单解题。
- **[S2] 项目资料：**[webpwnized/mutillidae README](https://github.com/webpwnized/mutillidae) — Setup 一键恢复、安全/非安全模式、漏洞覆盖；支持步骤 1–2。
- **[S3] 教程索引：**[Irongeek — Web Application Pen-testing Tutorials With Mutillidae](https://www.irongeek.com/i.php?page=videos/web-application-pen-testing-tutorials-with-mutillidae) — 分项视频目录（SQLi 绕过、命令注入、LFI、XSS）；支持步骤 5。
- **[S4] 专业复现：**[Mutillidae — SQLi: Bypass Authentication (Login)](https://inventyourshit.com/mutillidae-sqli-bypass-authentication-login/) — `index.php?page=login.php`、安全级别 0/1、用户名注入与 POST 字段；支持步骤 2–3。
- **[S5] 专业复现：**[hausec — SQLInjections](https://hausec.com/web-pentesting-write-ups/mutillidae/sqlinjections/) — `' or 1=1 -- ` 空格、用户枚举、指定 jeremy 必须加括号；支持步骤 3 与对应排坑。
- **[S6] 专业复现：**[Computer Security Student — Mutillidae Lesson 2 Command Injection](https://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson2/index.html) — DNS Lookup 菜单、`dns-lookup.php`、`host; command`；支持步骤 4。其中远程连库口令来自旧课环境，不作为本题凭据。

来源清单：[`../sources/136_mutillidae/_meta.md`](../sources/136_mutillidae/_meta.md)
