# 第224题来源｜ShowDoc CNVD-2020-26585 前台上传

## 题库字段（本地资料，不计外部来源数）

- 题名：`showdoc 文件上传 （cnvd-2020-26585）`
- 镜像：`vulfocus/showdoc-CNVD-2020-26585`
- 题库端口：`80,3306`

## 外部来源（6 个唯一链接）

### [S1] Vulhub 官方 README

- 链接：[vulhub/showdoc/CNVD-2020-26585/README.md](https://github.com/vulhub/vulhub/blob/master/showdoc/CNVD-2020-26585/README.md)
- 用途：ShowDoc **2.8.2**、未授权 POST `/index.php?s=/home/page/uploadImg`、字段 `editormd-image-file`、`filename="test.<>php"`、正文 `<?=phpinfo();?>`；中文版写明 **≤ 2.8.6**、修到 2.8.7。Vulhub 示例端口 8080。支撑步骤 1–2 与版本。中文：[README.zh-cn.md](https://github.com/vulhub/vulhub/blob/master/showdoc/CNVD-2020-26585/README.zh-cn.md)。

### [S2] 公开 PoC 摘录

- 链接：[Awesome-POC ShowDoc CNVD-2020-26585](https://github.com/Threekiii/Awesome-POC/blob/master/Web%E5%BA%94%E7%94%A8%E6%BC%8F%E6%B4%9E/ShowDoc%20%E5%89%8D%E5%8F%B0%E4%BB%BB%E6%84%8F%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%20CNVD-2020-26585.md)
- 用途：响应里给出 PHP 路径，示例 `/Public/Uploads/2024-06-03/665d568d2cdd9.php`。支撑成功信号。

### [S3] 官方修复

- 链接：[star7th/showdoc pull/1059](https://github.com/star7th/showdoc/pull/1059)
- 用途：upload 后缀校验修复。支撑“这就是 uploadImg 这条链”。

### [S4] CNVD 公告

- 链接：[CNVD-2020-26585](https://www.cnvd.org.cn/flaw/show/CNVD-2020-26585)
- 用途：编号核对。页面可能需登录；步骤以 [S1] 为准。

### [S5] 后续编号对照

- 链接：[CVE-2025-0520（Armis）](https://cve.armis.com/CVE-2025-0520)
- 用途：同一 ShowDoc &lt; 2.8.7 未授权上传，引用 Vulhub CNVD-2020-26585 与 PR 1059。支撑“不要另开一条 CVE-2025 链”。

### [S6] Vulfocus 官方镜像表

- 链接：[fofapro/vulfocus images/README.md](https://github.com/fofapro/vulfocus/blob/master/images/README.md)
- 用途：`docker pull vulfocus/showdoc-CNVD-2020-26585`。支撑镜像名。
