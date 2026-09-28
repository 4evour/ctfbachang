# 来源清单 — 018 DedeCMS 代码执行（CNVD-2018-01221）

- **[S1] Vulfocus 对应镜像复现：**[博客园：dedecms 命令执行（CNVD-2018-01221）](https://www.cnblogs.com/-ggbond-/p/16821088.html) — 使用 `vulfocus/dedecms-cnvd_2018_01221` 镜像，展示 `tpl.php` 的 `savetagfile` 写入逻辑、空 token 请求、`include/taglib/` 目标目录及镜像端口映射。支撑题目环境和该镜像主链。
- **[S2] 代码审计与复现：**[Mochazz：代码审计之 DedeCMS V5.7 SP2 后台代码执行漏洞（复现）](https://mochazz.github.io/2018/03/08/%E4%BB%A3%E7%A0%81%E5%AE%A1%E8%AE%A1%E4%B9%8BDedeCMS%20V5.7%20SP2%E5%90%8E%E5%8F%B0%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C%E6%BC%8F%E6%B4%9E%EF%BC%88%E5%A4%8D%E7%8E%B0%EF%BC%89/) — 给出 `CheckPurview('plus_文件管理器')`、CSRF token 检查、文件名正则、`stripslashes()` 及 `DEDEINC.'/taglib/'.$filename` 写入源码，并说明从 `action=upload` 取 token。用于补充空 token 与需 token 的源码/复现差异，并支撑特有排坑。
- **[S3] 安全公告与复现：**[UCloud U安全：DedeCMS V5.7 SP2 后台存在代码执行漏洞安全预警](https://m.ucloud.cn/mobile/ucsafe/1688.html) — 列明受影响版本，给出 token 获取、写入 `phpinfo()` 文件和访问验证步骤。支撑漏洞版本及操作链。
- **[S4] 官方漏洞编号记录：**[国家信息安全漏洞共享平台（CNVD）— CNVD-2018-01221](https://www.cnvd.org.cn/flaw/show/CNVD-2018-01221) — CNVD 官方编号记录入口，仅用于核对漏洞编号，不作为具体操作步骤依据。

本题卡片的利用链由 S1–S3 直接支撑；未引用其他 DedeCMS 漏洞链。共列出 4 个不重复来源链接，其中 3 个直接支撑操作链，1 个为 CNVD 编号记录。

