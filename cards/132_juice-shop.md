# 132｜OWASP Juice Shop 多挑战练习

- 镜像：`vulfocus/juice-shop`（Docker Hub 有该仓库，无概述、无本题专属 WP）
- 题库端口：`3000`
- 无 CVE。这是多挑战靶场，**不要**当成单一 RCE。[S1][S5]

## 一句话打法

先在前端 JS 里找出隐藏 Score Board，再只做**本实例计分板列出的**项：登录注入、后台路由、Search 上的 DOM XSS。[S1][S2][S4]

## 操作步骤

1. 打开 `http://<靶场IP>:3000/`。官方默认端口就是 3000。在 DevTools → Sources 打开压缩后的 `main.js`（可 Pretty-print），搜索 `score`，找到路由 `score-board` 后访问：[S2]

   `http://<靶场IP>:3000/#/score-board`

   打开后导航栏会出现 Score Board。之后**只按该页清单**做，不要把其它版本的挑战表整表硬套。[S1][S2][S4]

2. 登录管理员（计分项 “Login Admin”）。官方附录给出三条等价打法，邮箱在 **Email** 框，任意密码即可（第三条除外）：[S2]

   - `' or 1=1--`（打中 `Users` 表第一条，官方说恰好是管理员）
   - `admin@juice-sh.op'--`
   - 或邮箱 `admin@juice-sh.op`、密码 `admin123`（这条同时满足 “不改密、不用 SQLi” 的 Password Strength 项）[S2][S3]

3. 后台（“Admin Section”）：未登录访问 `/#/administration` 会 403。先完成步骤 2，再打开：[S2]

   `http://<靶场IP>:3000/#/administration`

   路由同样在 `main.js` 搜 `admin`，映射为 `path: "administration"`。[S2]

4. DOM XSS（仅当 Score Board 列出该项）：官方挑战描述要求的攻击串是下面这一条，贴进首页 **Search** 后回车，应弹出 `xss`：[S2][S4]

   ```text
   <iframe src="javascript:alert(`xss`)">
   ```

5. 其余项（购物车 `bid`、Contact Us 去 `disabled` 提交 0 星、`/ftp` 机密文档等）**只有计分板出现时才做**；Docker/Heroku 上部分 XSS/SSTi/NoSQL 项会标记 unavailable，不要强行套非 Docker 题解。[S2][S4]

## 本题特有排坑

- 哈希路由是 `/#/score-board`、`/#/login`、`/#/administration`，不是服务端 `/score-board` 静态路径。[S1][S2]
- SQLi 放 Email 字段；密码框乱填通用 payload 不会过。“Login Admin” 允许 SQLi，“Password Strength” 必须用原密码 `admin123`。[S2][S3]
- DOM XSS 官方校验的是带反引号的 `alert(\`xss\`)` iframe；普通 `<script>alert(1)</script>` 可能弹窗但不计分。[S4]
- 未找到 `vulfocus/juice-shop` 专属 WP，版本以实例 Score Board 为准；官方附录按 companion v15 / 挑战 YAML 书写，旧镜像可能少题或多禁用项。[S2][S4][S5]

## 来源

- [S1] 官方 companion：隐藏 Score Board、从 `main.js` 找路由。详见[来源清单](../sources/132_juice-shop/_meta.md)。
- [S2] 官方题解附录：Score Board / Login Admin / Administration 逐步操作。详见[来源清单](../sources/132_juice-shop/_meta.md)。
- [S3] 官方 companion 认证章：原密码登录与 SQLi 分题。详见[来源清单](../sources/132_juice-shop/_meta.md)。
- [S4] 官方 `challenges.yml`：DOM XSS 精确 payload、Score Board / Admin 题面。详见[来源清单](../sources/132_juice-shop/_meta.md)。
- [S5] Docker Hub `vulfocus/juice-shop`：镜像名对应；无 overview、无入口说明。详见[来源清单](../sources/132_juice-shop/_meta.md)。
