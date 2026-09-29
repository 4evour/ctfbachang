# 122｜bWAPP 综合漏洞练习

> **先走门户菜单：**bWAPP 是故意留洞的练习应用（100+ 项），不是单一 CVE。按本实例 portal 下拉框列出的 bug、并把安全级别设为 **low** 再逐项做。未找到该 Vulfocus 镜像的专属 WP，以下入口来自官方安装说明。[S1][S2]

- 镜像：`vulfocus/bwapp:latest`（Hub 无描述）
- 题库端口：`80,3306`

## 操作步骤

1. 打开映射到容器 80 的地址。若跳到安装页或提示数据库未就绪，按官方流程访问 `install.php`（或 `install.php?install=yes`）完成安装后再登录。context path 可能是 `/` 或 `/bWAPP/`，以首页实际链接为准。[S2]
2. 登录默认账号 **`bee` / `bug`**（官方安装文档给出；页面若改过则以页面为准），进入 **portal**。[S2]
3. 在 portal 把 **security level 设为 low**，再从 bug 下拉框选具体练习（HTML/XSS/SQLi/文件包含等）。每一项用当前页表单和提示的参数去测，不要把其他靶场的 payload 硬套过来。[S1][S2]
4. 成功信号：当前练习页出现对应漏洞效果（例如 SQL 报错/回显、脚本执行、文件被包含），而不是登录失败或一直停在 install。

## 本题特有排坑

- **先安装再登录。**未跑 `install.php` 时常见空白页或 `Unknown database 'bWAPP'`，不是漏洞本身失败。[S2]
- 默认口令是 `bee`/`bug`，不是 `admin`/`admin`。[S2]
- 安全级别 medium/high 会加过滤，公开练习步骤默认 **low**；级别不对时 payload 看起来「无效」。[S2]
- 这是多漏洞训练场，卡片不编造某一条「必打」RCE；以 portal 清单为准。[S1]

## 来源

- [S1] bWAPP 官方站点。详见[来源清单](../sources/122_bwapp/_meta.md)。
- [S2] 官方安装说明（`install.php`、`bee`/`bug`）。详见[来源清单](../sources/122_bwapp/_meta.md)。
- [S3] 安装与 portal/low 级别操作对照。详见[来源清单](../sources/122_bwapp/_meta.md)。
- [S4] Docker Hub `vulfocus/bwapp`。详见[来源清单](../sources/122_bwapp/_meta.md)。
