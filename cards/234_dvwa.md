# 234｜DVWA 综合漏洞练习（无 CVE）

> **先走菜单：**DVWA 是故意留洞的练习应用，不是单一 CVE。先 Setup、登录、把安全级别设为 **low**，再按左侧模块做。未找到该 Vulfocus 镜像的专属 WP，入口来自官方文档。[S2][S3]

- 镜像：`vulfocus/dvwa`（Hub 无 overview）[S1]
- 题库端口：`80,3306`

## 操作步骤

1. 打开映射到容器 80 的地址。数据库未就绪时进 **Setup DVWA** / `setup.php`，点 **Create / Reset Database**。[S3]
2. 登录 **`admin` / `password`**（`login.php`）。这是 Web 账号，不是 `config.inc.php` 里的数据库 `dvwa`/`p@ssw0rd`。[S3][S4]
3. **DVWA Security** 设为 **low** 再 Submit。然后从左侧菜单选 Brute Force、SQLi、Command Injection、File Upload、XSS 等；用当前页表单，不要硬套其他靶场 payload。[S5]
4. 成功信号：当前练习页出现对应效果，而不是停在 setup 或登录失败。

## 本题特有排坑

- Web 口令是 `admin`/`password`，不是数据库口令。[S4]
- 上游较新默认级别可能是 **impossible**；payload「无效」时先看 cookie/级别。[S5]
- Hub 无模块清单，以实例左侧菜单为准。[S1]
- 卡片不编造某一条「必打」RCE。[S2]

## 来源

- [S1] Docker Hub `vulfocus/dvwa`。详见[来源清单](../sources/234_dvwa/_meta.md)。
- [S2] DVWA 官方仓库。详见[来源清单](../sources/234_dvwa/_meta.md)。
- [S3] 官方 Getting Started：setup/登录。详见[来源清单](../sources/234_dvwa/_meta.md)。
- [S4] Quickstart。详见[来源清单](../sources/234_dvwa/_meta.md)。
- [S5] Security levels。详见[来源清单](../sources/234_dvwa/_meta.md)。
