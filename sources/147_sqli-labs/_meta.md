# 第147题来源｜vulfocus/sqli-labs

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/sqli-labs`
- 镜像：`vulfocus/sqli-labs`
- 题库端口：`80,3306`
- 无 CVE；题库未指定 Less 编号。

## 外部来源（4 个唯一链接）

### [S1] 题库镜像仓库 — vulfocus/sqli-labs

- 链接：[Docker Hub — vulfocus/sqli-labs](https://hub.docker.com/r/vulfocus/sqli-labs)
- 用途：与题库镜像名对应。现有页面信息不足以确定镜像内具体 Less；只支撑镜像身份和“关卡未确认”，不支撑注入步骤。

### [S2] sqli-labs 项目 README — Audi-1/sqli-labs

- 链接：[readme.md](https://github.com/Audi-1/sqli-labs/blob/master/readme.md)
- 用途：说明项目覆盖 Error Based、Blind、Header、WAF 绕过等多类 GET/POST 关卡；安装后访问首页并点击 setup/resetDB。支撑卡片对多关卡靶场的判断和步骤 1；不能据此锁定 Vulfocus 镜像的具体 Less。

### [S3] 项目首页 — index.html

- 链接：[index.html](https://github.com/Audi-1/sqli-labs/blob/master/index.html)
- 用途：展示 **Setup/reset Database for labs** 与 Page-1 Basic Challenges 入口。支撑步骤 1 中先初始化数据库、再按页面关卡进入。

### [S4] 直接关卡题解 — ZQQ《SQLi Labs》

- 链接：[SQLi Labs](https://zqq.name/docs/security/exploits/1-SQLi-Labs/)
- 用途：逐关覆盖 Less-1 至 Less-10：单引号/数字型/括号/双引号、double query 报错、outfile、布尔盲注、时间盲注，以及 `--+` 注释。支撑操作步骤 2–3 与速查表。文章使用 `acgpiano/sqli-labs` 与主机端口 `50080`，不是本题镜像的已知配置。
