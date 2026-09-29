# 第184题来源｜YApi Mock RCE

## 题库字段（本地资料，不计外部来源数）

- 题名：`yapi 代码执行`
- 镜像：`vulfocus/yapi:latest`
- 题库端口：`3000,27017`
- 无 CVE

## 外部来源（6 个唯一链接）

### [S1] Vulhub README

- 链接：[yapi/unacc](https://github.com/vulhub/vulhub/tree/master/yapi/unacc)
- 用途：1.9.2、注册、Mock 脚本、Mock URL。支撑步骤 1–4。

### [S2] YMFE Issue 2233

- 链接：[YMFE/yapi#2233](https://github.com/YMFE/yapi/issues/2233)
- 用途：PoC 与 `mockJson` 大小写。

### [S3] sechub 分析

- 链接：[sechub 2366798](https://sechub.in/view/2366798)
- 用途：vm 沙箱逃逸。

### [S4] NSFocus

- 链接：[YApi 0day 处置](https://blog.nsfocus.net/yapi-0day/)
- 用途：影响与缓解背景。

### [S5] NOSEC Vulfocus 记录

- 链接：[nosec 4948](https://nosec.org/home/detail/4948.html)
- 用途：`vulfocus/yapi` 与 `ls` 类命令注意点。

### [S6] YMFE Issue 2809

- 链接：[ymfe/yapi#2809](https://github.com/YMFE/yapi/issues/2809)
- 用途：后续 safeify/`/mock/{id}/` 变体，避免与 1.9.2 vm 链混写。
