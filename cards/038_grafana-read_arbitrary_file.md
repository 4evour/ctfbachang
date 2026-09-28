# Grafana 未授权任意文件读取

> **一句话打法：**公开 PoC 逐个尝试 `/public/plugins/<插件ID>/../../../../../../../../etc/passwd`，以 HTTP 200 且响应包含 `root:x` 作为命中判断。[S1][S2]

## 题库环境

- 题名：Grafana 未授权任意文件读取
- 镜像：`vulfocus/grafana-read_arbitrary_file:latest`
- 内部端口：`3000`；访问时替换为 Vulfocus 分配的映射端口。
- **资料边界：**题库未给 CVE 编号；现有公开资料能确认利用链与 CVE-2021-43798 对应，但没有资料确认这个镜像的具体版本或构建来源，所以下列为公开 PoC 参考链路，不代表镜像已验证。[S1][S2][S4]

## 操作步骤（按来源脚本调用）

1. 在脚本所在目录创建 `result-20211209001115.txt`，每行填写一个目标基础地址，例如：

   ```text
   http://<靶场IP>:<映射端口>
   ```

   这是来源脚本实际读取的输入文件名；脚本会从每行解析目标地址。[S2]

2. 将来源中的 `Grafana-0Day-Vuln-POC.py` 放在该目录，执行原脚本：

   ```powershell
   python .\Grafana-0Day-Vuln-POC.py
   ```

   脚本会自动遍历其内置插件路径候选并请求 `/etc/passwd`，不需要手工拼接或另写请求代码。[S2]

3. 成功时脚本会输出“发现可利用的漏洞”、命中的 Payload 和响应片段。脚本判定条件为 HTTP 200 且响应正文包含 `root:x`。[S2]

## 本题排坑

- **输入文件名必须一致。**脚本固定读取 `result-20211209001115.txt`；目标基础地址按每行一个填写。[S2]
- **插件候选由脚本自动遍历。**候选路径和目录回退已写在脚本中，直接使用其调用方式，不要把路径改成其他漏洞接口。[S2]
- **以正文特征判断命中。**仅有 HTTP 200 不够，脚本还要求响应中出现 `root:x`。[S2]

## 与 CVE-2021-43798 的关系

公开 0Day PoC 使用的插件路径遍历与 CVE-2021-43798 的公开链路对应：原文链接的参考仓库现指向 `Grafana-CVE-2021-43798`，Grafana 官方公告也将 `/public/plugins/<plugin-id>` 目录遍历编号为 CVE-2021-43798。[S1][S2][S3][S4]

## 来源

- [S1] [Grafana V8.0+版本存在未授权任意文件读取 0Day漏洞 - POC（原文）](https://mik1th0n.github.io/2021/12/08/Grafana-0Day-Vuln-POC/)：公开 0Day 描述及作者 PoC、参考仓库链接。
- [S2] [Grafana-0Day-Vuln-POC（作者脚本）](https://github.com/mik1th0n/Grafana-0Day-Vuln-POC/blob/main/Grafana-0Day-Vuln-POC.py)：脚本输入文件名、调用方式、插件候选、请求路径及命中条件。
- [S3] [Grafana-CVE-2021-43798（原文引用的参考仓库）](https://github.com/jas502n/Grafana-VulnTips)：原文引用的旧仓库地址现在跳转至该 CVE 仓库。
- [S4] [Grafana Labs 官方公告：Grafana 8.3.1、8.2.7、8.1.8、8.0.7 安全更新](https://grafana.com/blog/grafana-8-3-1-8-2-7-8-1-8-and-8-0-7-released-with-high-severity-security-fix/)：将 `/public/plugins/<plugin-id>` 目录遍历列为 CVE-2021-43798，并说明受影响版本范围。
- [S5] [奇安信 CERT：Grafana 任意文件读取 0Day 漏洞安全风险通告](https://www.qianxin.com/news/detail?news_id=3054)：2021-12-07 通告，独立确认 Grafana 8.x 存在未授权任意文件读取。

来源清单：[`../sources/038_grafana-read_arbitrary_file/_meta.md`](../sources/038_grafana-read_arbitrary_file/_meta.md)
