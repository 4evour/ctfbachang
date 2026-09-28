# 来源清单 — 008 BodgeIt Store

- **[S1] 专业复现：**[Infosec Institute — The BodgeIt Store, Part 1](https://www.infosecinstitute.com/resources/reverse-engineering/the-bodgeit-store-part-1-2/) — 步骤：Score/`admin.jsp`、反射与存储型 XSS、GET 改密、负数购物车、`b_id` Cookie 篡改。
- **[S2] 专业复现：**[Infosec Institute — The BodgeIt Store, Part 2](https://www.infosecinstitute.com/resources/reverse-engineering/the-bodgeit-store-part-2/) — 步骤：登录 SQL 注入；高级搜索 AES、HSQLDB 查询和 CSRF。
- **[S3] 官方目录：**[OWASP VWAD — BodgeIt Store](https://vwad.owasp.org/app/bodgeit-store/) — 应用性质、漏洞类别和练习方式。
- **[S4] 项目资料：**[psiinon/bodgeit README](https://github.com/psiinon/bodgeit) — 应用部署入口、路径和 Score 功能。
- **[S5] 复现补充：**[Passion for Pentesting — BodgeIt Walkthrough](https://passionforpentesting.files.wordpress.com/2021/02/bodgeit-walkthrough.pdf) — 登录与购物车项目的操作对照。

题库条目：`bodgeit 靶场`；镜像 `vulfocus/bodgeit:latest`；内部端口 `8080`。卡片的路径与利用细节来自经典 BodgeIt Store 文章；实际 context path 以首页链接为准。
