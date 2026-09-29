# 第132题来源｜OWASP Juice Shop 多挑战靶场

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/juice-shop`
- 无 CVE
- 题库端口：`3000`
- 镜像：`vulfocus/juice-shop`（Docker Hub 存在，无概述）。未找到该 Vulfocus 镜像的专属 WP。

## 外部来源（5 个唯一链接）

### [S1] 官方 companion — Score Board

- 链接：[Finding the Score Board · Pwning OWASP Juice Shop](https://pwning.owasp-juice.shop/companion-guide/latest/part2/score-board.html)
- 用途：说明 Score Board 无导航链接，需猜测 URL 或从不可见资源找线索。支撑步骤 1 的“先找计分板、再按清单做”定位。该页未写出完整 `/#/score-board` 步骤（步骤在附录）。

### [S2] 官方题解附录

- 链接：[Challenge solutions · Pwning OWASP Juice Shop](https://help.owasp-juice.shop/appendix/solutions.html)
- 用途：逐步：DevTools 打开 `main.js` 搜 `score` → `http://localhost:3000/#/score-board`；搜 `admin` → `/#/administration`（未登录 403）；Login Admin 的 `' or 1=1--`、`admin@juice-sh.op'--`、`admin@juice-sh.op`/`admin123`；以及 Docker 上部分挑战不可用的提示。支撑步骤 1–3、5 与对应排坑。附录声明默认端口 3000、兼容 companion 对应的 Juice Shop 版本（该页写 v15.0.0），**不能**自动当成 Vulfocus 镜像版本。

### [S3] 官方 companion — Broken Authentication

- 链接：[Broken Authentication · Pwning OWASP Juice Shop](https://pwning.owasp-juice.shop/companion-guide/latest/part2/broken-authentication.html)
- 用途：区分 “Login Admin”（可用 SQLi）与 “Password Strength”（必须用管理员原密码、不能先改密或先 SQLi）。支撑步骤 2 第三条与排坑。

### [S4] 官方挑战定义 YAML

- 链接：[juice-shop data/static/challenges.yml](https://github.com/juice-shop/juice-shop/blob/master/data/static/challenges.yml)
- 用途：Score Board / Admin Section / Login Admin 题面；DOM XSS 描述给出精确串 `<iframe src="javascript:alert(\`xss\`)">`。支撑步骤 4 与 XSS 计分校验排坑。master 与旧镜像挑战集合可能不一致，以实例 Score Board 为准。

### [S5] Docker Hub — vulfocus/juice-shop

- 链接：[vulfocus/juice-shop](https://hub.docker.com/r/vulfocus/juice-shop)
- 用途：与题库镜像名对应；页面无 overview、无端口/版本说明。只支撑镜像身份，不支撑利用步骤。
