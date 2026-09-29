# 第194题来源｜CNVD-2020-27175 DCRCMS 上传

## 题库字段（本地资料，不计外部来源数）

- 题名：`dcrcms 文件上传 （CNVD-2020-27175）`
- 镜像：`vulfocus/dcrcms-cnvd_2020_27175`
- 题库端口：`80,3306`
- 编号：CNVD-2020-27175

## 外部来源（4 个唯一链接）

### [S1] Docker Hub

- 链接：[vulfocus/dcrcms-cnvd_2020_27175](https://hub.docker.com/r/vulfocus/dcrcms-cnvd_2020_27175)
- 用途：`/dcr/login.htm`、admin:123456。

### [S2] Vulfocus 复现

- 链接：[CSDN DCRCMS 上传](https://blog.csdn.net/qq_53079406/article/details/127238674)
- 用途：新闻上传 + `Content-Type: image/jpeg` + `/uploads/news/`。

### [S3] 点名 CNVD 的 CTF 题解

- 链接：[NewStarCTF 题解中的 DCRCMS](https://wanth3f1ag.top/posts/NewStarCTF2025%E9%A2%98%E8%A7%A3/)
- 用途：`tpl_import_action.php` / `configfile` MIME 绕过；明确写 CNVD-2020-27175。

### [S4] 路径对照

- 链接：[wlaqsys 5837](https://www.wlaqsys.com/archives/5837)
- 用途：新闻上传路径对照。该页同时误列 CVE-2017-20063，**不作为 CVE 依据**。

## 检索结论

CNVD 官方页未能打开。未把未引用本编号的其他 DCRCMS 漏洞拼进本题。
