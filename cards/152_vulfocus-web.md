# 152｜vulfocus/vulfocus-web

- 镜像：`vulfocus/vulfocus-web:latest`
- 题库端口：`80`
- 无 CVE/CNVD

## 一句话结论

这是 **Vulfocus 平台前端（nginx）**，不是漏洞靶场；按镜像名检索未找到可执行利用链。[S1][S2][S3]

## 利用链路

官方 compose 把 `vulfocus-web` 映射到宿主机 **80**，页面是平台 UI。[S1]

```powershell
curl.exe -sI "http://<靶场IP>/"
```

成功信号：HTTP 200/302 且正文/跳转指向 Vulfocus 前端。这只用于识别组件，不是漏洞成功信号。

## 本题特有排坑

- 不要和同样走 80 端口的漏洞镜像混淆；本题镜像名就是平台 Web。[S1][S3]
- 文档里的默认管理员账号属于**平台登录**，不是本题 CVE 链。[S2]

## 来源

- [S1] 官方 compose：`vulfocus-web` 发布 80。详见[来源清单](../sources/152_vulfocus-web/_meta.md)。
- [S2] 官方安装说明。详见[来源清单](../sources/152_vulfocus-web/_meta.md)。
- [S3] Docker Hub `vulfocus/vulfocus-web`。详见[来源清单](../sources/152_vulfocus-web/_meta.md)。
- [S4] 官方文档：平台角色。详见[来源清单](../sources/152_vulfocus-web/_meta.md)。
