# 第178题来源｜CNVD-2020-50280 / CVE-2020-25213 File Manager

## 题库字段（本地资料，不计外部来源数）

- 题名：`wordpress 文件上传  （CNVD-2020-50280）`
- 镜像：`vulfocus/wordpress-cnvd_2020_50280`
- 题库端口：`80,3306`
- 编号：CNVD-2020-50280（对应 CVE-2020-25213）

## 外部来源（4 个唯一链接）

### [S1] CNVD 记录镜像

- 链接：[ZONE.CI CNVD-2020-50280](https://zone.ci/aliyun/ali_nonvd/254769.html)
- 用途：确认 CNVD 名称与 WordPress 文件上传类别（CNVD 官网常无法打开）。

### [S2] NVD CVE-2020-25213

- 链接：[CVE-2020-25213](https://nvd.nist.gov/vuln/detail/CVE-2020-25213)
- 用途：wp-file-manager 6.0–6.8；未授权 elFinder connector。支撑编号映射。

### [S3] 上传 PoC

- 链接：[wpFileManagerExploit.sh](https://github.com/ALIF101XL/wpFileManagerExploit/blob/main/wpFileManagerExploit.sh)
- 用途：`errUnknownCmd` 探测、`cmd=upload`、`target=l1_Lw`、`upload[]`。支撑步骤 1–3。

### [S4] FortiGuard 通告

- 链接：[RCE in WordPress File Manager](https://www.fortiguard.com/threat-signal-report/3663/remote-code-execution-vulnerability-in-wordpress-file-manager-plugin)
- 用途：6.9 修复、公开利用情况。
