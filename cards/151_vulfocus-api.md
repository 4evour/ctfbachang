# 151｜vulfocus/vulfocus-api

- 镜像：`vulfocus/vulfocus-api:latest`
- 题库端口：`8000`
- 无 CVE/CNVD

## 一句话结论

这是 **Vulfocus 平台后端**（Django/Celery + Docker），不是漏洞靶场镜像；按镜像名检索未找到可执行利用链，不能编造成 CVE 题。[S1][S2][S3]

## 利用链路

现有来源只确认该镜像是编排 API：官方 `docker-compose` **不把 API 映射到宿主机**，对外只暴露 `vulfocus-web` 的 **80**；源码安装时由 nginx 反代 `/api`。[S1][S2]

```powershell
curl.exe -sI "http://<靶场IP>/"
```

成功信号：若实例实际跑的是完整平台，首页是 Vulfocus 登录/控制台；这不是漏洞回显，只用于识别组件。

## 本题特有排坑

- 题库内部端口 **8000** 不等于 compose 对外端口；compose 文档只发布 **80**。[S1]
- 不要把平台容器里的 `/var/run/docker.sock` 或默认账号当成「本题 CVE」。官方说明 Flag 写在**被拉取的漏洞镜像**里，不在平台 API 容器。[S3]

## 来源

- [S1] 官方 compose：API 不对外发布。详见[来源清单](../sources/151_vulfocus-api/_meta.md)。
- [S2] 官方安装说明：uWSGI `/api`、nginx :80。详见[来源清单](../sources/151_vulfocus-api/_meta.md)。
- [S3] 官方文档：平台用途与 Flag 约定。详见[来源清单](../sources/151_vulfocus-api/_meta.md)。
- [S4] Docker Hub `vulfocus/vulfocus-api`。详见[来源清单](../sources/151_vulfocus-api/_meta.md)。
