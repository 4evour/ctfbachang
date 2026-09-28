# 第038题来源清单：Grafana 未授权任意文件读取

题库信息：镜像 `vulfocus/grafana-read_arbitrary_file:latest`，内部端口 `3000`，题库未给 CVE 编号。

**资料边界：**公开资料可以确认这条 PoC 链路与 CVE-2021-43798 对应，但没有资料确认该 Vulfocus 镜像的具体版本或构建来源。

## 来源

- [S1] [Grafana V8.0+版本存在未授权任意文件读取 0Day漏洞 - POC（原文）](https://mik1th0n.github.io/2021/12/08/Grafana-0Day-Vuln-POC/)
  - 支持：公开 0Day 描述，以及作者 PoC 和参考仓库链接。

- [S2] [Grafana-0Day-Vuln-POC（作者脚本）](https://github.com/mik1th0n/Grafana-0Day-Vuln-POC/blob/main/Grafana-0Day-Vuln-POC.py)
  - 支持：固定读取的 `result-20211209001115.txt` 输入文件、直接运行方式；脚本中的插件候选、`/etc/passwd` 请求路径，以及 HTTP 200 并包含 `root:x` 的命中条件。
  - 用途：卡片步骤与排坑。

- [S3] [Grafana-CVE-2021-43798（原文引用的参考仓库）](https://github.com/jas502n/Grafana-VulnTips)
  - 支持：S1 原文引用的旧仓库地址现在跳转至标题为 `Grafana-CVE-2021-43798` 的仓库。
  - 用途：核对公开 PoC 的漏洞关联。

- [S4] [Grafana Labs 官方公告：Grafana 8.3.1、8.2.7、8.1.8、8.0.7 安全更新](https://grafana.com/blog/grafana-8-3-1-8-2-7-8-1-8-and-8-0-7-released-with-high-severity-security-fix/)
  - 支持：官方将 `/public/plugins/<plugin-id>` 目录遍历列为 CVE-2021-43798，并列出受影响版本范围为 Grafana 8.0.0-beta1 至 8.3.0。
  - 用途：确认公开 0Day PoC 所用漏洞链与 CVE-2021-43798 对应。

- [S5] [奇安信 CERT：Grafana 任意文件读取 0Day 漏洞安全风险通告](https://www.qianxin.com/news/detail?news_id=3054)
  - 支持：2021-12-07 通告确认 Grafana 8.x 存在未授权任意文件读取。
  - 用途：独立佐证漏洞类型和未授权影响。
