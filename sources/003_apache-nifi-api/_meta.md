# 来源清单 — 003 Apache NiFi API

- **[S1] 同题 Vulfocus WP：**[NOSEC：Vulfocus 靶场竞赛中级部分题解，vulfocus/041](https://nosec.org/home/detail/4950.html) — 与题库 NiFi 题相符，展示 PoC 与回连步骤；支撑卡片步骤 2–3。
- **[S2] PoC：**[imjdl/Apache-NiFi-Api-RCE](https://github.com/imjdl/Apache-NiFi-Api-RCE) — 读取根流程组并通过 API 创建、配置和启动 `ExecuteProcess` 处理器；支撑命令执行步骤。
- **[S3] 检测模板：**[ProjectDiscovery Nuclei Apache NiFi 未授权访问模板](https://github.com/projectdiscovery/nuclei-templates/blob/main/http/misconfiguration/apache/apache-nifi-unauth.yaml) — 使用 `GET /nifi-api/access/config` 与 `supportsLogin:false` 判断匿名访问；支撑步骤 1。
- **[S4] 官方文档：**[Apache NiFi 1.12.1 ExecuteProcess 文档](https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.12.1/org.apache.nifi.processors.standard.ExecuteProcess/) — 处理器的命令配置说明；支撑 PoC 参数理解。

题库：`vulfocus/apache_nifi_api:latest`，内部端口 `8080`；未提供 CVE。
