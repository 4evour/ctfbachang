# 来源清单 — 016 daemon-api 未授权访问

- **[S1] 官方同类环境与完整复现：**[Vulhub — Docker Remote API Unauthorized Access Leads to Remote Code Execution](https://github.com/vulhub/vulhub/blob/master/docker/unauthorized-rce/README.md) — Vulhub 官方同类环境说明 daemon 未认证监听 TCP `2375`；提供 Python Docker SDK 连接及创建容器的复现，并通过把 daemon 主机 `/etc` 挂入容器后向 `/tmp/etc/crontabs/root` 写入 cron 回连命令。支撑卡片中的端口/连接方式、容器创建、挂载与 cron 利用链。该资料对应 Vulhub 的 `docker/unauthorized-rce`，不是 Vulfocus 镜像专属 WP。
- **[S2] 技术复现文章：**[青藤云安全 — 容器安全防线：Docker攻击方式与防范技术探究](https://www.qingteng.cn/news/642fdee8021c63005a13bd44.html) — 明确讨论 Vulhub Docker daemon API 未授权环境，复现使用 `2375`、Alpine、新建容器、挂载 `/etc` 到 `/tmp/etc` 及 crontab 回连。支撑卡片的远端容器操作步骤与 cron 链。
- **[S3] 技术复现及环境排坑：**[CN-SEC — 新姿势之Docker Remote API未授权访问漏洞分析和利用](https://cn-sec.com/archives/53287.html) — 介绍 Docker Remote API 未授权访问，展示 `docker -H tcp://<目标>:2375 version`、远端容器/镜像查询、Docker API 直接请求及挂载宿主机目录、写入 crontab 的复现方式。支撑卡片步骤 1–4 和远端/本机 daemon 区分排坑。
- **[S4] Docker 官方安全说明：**[Docker Engine security](https://docs.docker.com/engine/security/) — 官方说明 Docker daemon 的高权限属性，以及通过共享目录让容器访问/修改 host 文件系统的安全影响。支撑原理说明，不提供题目专属命令。

## 资料边界

以题名 `daemon-api 未授权访问`、题库镜像 `vulfocus/daemon-api:latest` 和端口 `2375` 检索，未找到能够确认与该 Vulfocus 镜像完全对应的专属 WP。卡片利用链取自同为 Docker Remote API 未授权访问的 Vulhub 官方复现及直接复现文章；题目内部具体 daemon 拓扑，以及 Vulhub cron 链依赖的 crontab 路径、cron 服务和 `nc -e` 支持情况，不能仅凭现有公开材料断定与该镜像一致。

题库条目：`daemon-api 未授权访问`；镜像：`vulfocus/daemon-api:latest`；内部端口：`2375`。有效且不重复的外部来源：4。

