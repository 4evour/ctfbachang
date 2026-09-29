# 235｜Pikachu 综合漏洞练习（无 CVE）

> **先初始化再按菜单：**Pikachu 是多漏洞练习台，不是单一 CVE。未找到 Vulfocus 镜像专属逐步 WP；入口来自官方项目说明。[S2]

- 镜像：`vulfocus/pikachu`（Hub 无 overview）[S1]
- 题库端口：`80,3306`
- 官方仓库是 `zhuifengshaonianhanlu/pikachu`。`zhuzhichao/pikachu` 未找到。[S2]

## 操作步骤

1. 打开映射到 80 的地址。若出现「pikachu还没有初始化，点击进行初始化安装!」，点它或访问 `/install.php` 完成初始化。[S2][S5]
2. 使用左侧菜单：暴力破解、XSS、CSRF、SQLi、RCE、LFI、上传/下载、SSRF、XXE、反序列化等。每页有「提示」，按当前页参数测。[S2]
3. 平台本身**没有全站登录口令**。`admin`/`123456` 出现在暴力破解/XSS 等练习表单里，不是 Docker 门户账号。[S4]
4. 成功信号：当前练习页出现对应漏洞效果，而不是未初始化的空页/报错。

## 本题特有排坑

- 未初始化数据库时页面空白或报错，不是 payload 失败。[S2]
- 不要把第三方文的「全局 admin/123456 登录」套到本 Hub 镜像。[S4]
- 卡片不编造某一条必打 RCE。[S2]

## 来源

- [S1] Docker Hub `vulfocus/pikachu`。详见[来源清单](../sources/235_pikachu/_meta.md)。
- [S2] 官方 GitHub / README。详见[来源清单](../sources/235_pikachu/_meta.md)。
- [S3] README raw。详见[来源清单](../sources/235_pikachu/_meta.md)。
- [S4] issue #12：练习页账号。详见[来源清单](../sources/235_pikachu/_meta.md)。
- [S5] 文档：`vulfocus/pikachu` + 初始化点击。详见[来源清单](../sources/235_pikachu/_meta.md)。
