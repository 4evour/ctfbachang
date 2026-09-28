# BodgeIt Store 综合漏洞练习

> **先走计分板：**按本实例 Score 页列出的挑战逐项处理；先做隐藏页面、XSS、登录 SQL 注入和购物车参数类项目。BodgeIt 是多漏洞练习应用，不是单一 CVE。[S1][S3]

> 题库镜像：`vulfocus/bodgeit:latest`；内部端口 `8080`。未找到该 Vulfocus 镜像的专属 WP，以下路径和操作来自经典 BodgeIt Store 复现；先从页面自身链接确认实际 context path。

## 操作步骤

1. 打开 `http://<IP>:<PORT>/`，从首 页进入 **About Us → Score**。若应用部署在 `/bodgeit/`，计分页通常是 `/bodgeit/score.jsp`；以首页实际链接为准，先记下当前计分项。[S1][S3][S4]

2. 查看首页 HTML 源码，搜索 `admin.jsp`；经典版本把入口放在注释中。按实际 context path 访问该页面，查看公开的用户/basket 信息。[S1][S4]

3. 按 Score 项目测试基础输入点：
   - 在 Search 表单提交 `<script>alert('XSS')</script>`，查看浏览器是否执行脚本；这是反射型 XSS 检查。[S1]
   - 注册测试账号，在邮箱/用户名字段尝试 `demo@example.com<i>test</i>`，登录后查看用户名显示位置；经典版本用此处演示存储型 HTML/XSS。[S1]
   - 登录表单用户名输入下列字符串、密码填任意值，观察是否绕过登录：

```text
test@thebodgeitstore.com' OR '1'='1
```

经典复现再把用户名换成 `user1@thebodgeitstore.com` 或 `admin@thebodgeitstore.com` 测试不同账号。[S2][S5]

4. 使用自己的测试账号完成账户/购物车类项目：
   - 改密码时用浏览器开发者工具把表单 method 从 `POST` 改成 `GET`，再提交 `password1`、`password2` 参数。[S1]
   - 加入商品后用 Burp/ZAP 拦截购物车更新请求，把数量改成负数并放行，查看总价变化。[S1][S5]
   - 在 `admin.jsp` 取得经典版本展示的 basket ID 后，将浏览器 `b_id` Cookie 改为该 ID 并刷新购物车，检查是否切换到对应 basket。[S1][S4]

5. 只有当 Score 清单列出高级搜索时再做：进入 `/advanced.jsp`，检查浏览器端参数加密/转义逻辑；按 Part 2 文章修改查询输入，再使用其 HSQLDB 语法验证注入点。[S2]

## 这题特有的排坑

- **context path 不同：**公开复现常见 `/bodgeit/`；不要直接硬套绝对路径，从首页链接复制实际前缀后再访问 `admin.jsp`、`score.jsp`。[S1][S4]
- **XSS 只回显不执行：**反射型测试看浏览器是否弹窗；存储型测试要重新打开显示用户名的页面，不能只看注册响应。[S1]
- **SQL 注入目标是邮箱登录字段：**在用户名框输入完整字符串，别把 payload 放到密码框；登录失败时先核对账号拼接格式和引号，而不是换成 MySQL 通用 payload。公开复现使用 HSQLDB。[S2]
- **高级搜索参数在客户端处理：**Part 2 使用的 AES/转义流程是此应用特性；直接对表单 URL 跑通用 sqlmap 可能无法复现文章请求。[S2]
- 每完成一项都刷新 Score 页看该项是否被记录；不要把其他版本的挑战清单当作本实例计分表。[S1][S3]

## 来源

- **[S1] 专业复现：**[Infosec Institute — The BodgeIt Store, Part 1](https://www.infosecinstitute.com/resources/reverse-engineering/the-bodgeit-store-part-1-2/) — 详细复现隐藏 `admin.jsp`、搜索/注册 XSS、GET 改密、购物车负数及 `b_id` 篡改；支持步骤 1–4 与对应排坑。
- **[S2] 专业复现：**[Infosec Institute — The BodgeIt Store, Part 2](https://www.infosecinstitute.com/resources/reverse-engineering/the-bodgeit-store-part-2/) — 登录 SQL 注入、高级搜索 AES/HSQLDB、CSRF；支持步骤 3、5 与对应排坑。
- **[S3] 官方资料：**[OWASP Vulnerable Web Applications Directory — BodgeIt Store](https://vwad.owasp.org/app/bodgeit-store/) — 应用性质与漏洞类别；支持开头说明和 Score 页逐项解题方式。
- **[S4] 项目资料：**[psiinon/bodgeit README](https://github.com/psiinon/bodgeit) — 应用入口、部署路径及 Score 功能；支持步骤 1–2。
- **[S5] 复现补充：**[Passion for Pentesting — BodgeIt Walkthrough](https://passionforpentesting.files.wordpress.com/2021/02/bodgeit-walkthrough.pdf) — 对照登录绕过、购物车项目的实际操作顺序；支持步骤 3–4。

来源清单：[`../sources/008_bodgeit/_meta.md`](../sources/008_bodgeit/_meta.md)
