# Hessian 反序列化

> **题库信息：**题名「Hessian 反序列化」；镜像 `vulfocus/hessian:latest`；内部端口 `8080`；题库未提供 CVE。
>
> **通用起手流程，非镜像专属利用链。**目前没有直接来源确认该镜像的具体案例；先从实际服务请求识别 Hessian 入口，再按观察到的协议与接口构造兼容请求，不预设 URL 或 gadget。

## 上手流程

1. 在 Vulfocus 启动实例，通过分配的访问地址打开映射到容器内部 `8080` 的服务。先查看首页响应、跳转和页面引用的脚本；不要把内部端口直接当成外部端口，也不要猜 context path。
2. 若页面提供正常操作入口，在浏览器开发者工具的 **Network** 中触发一次正常请求；记录请求方法、完整路径、`Content-Type`、请求体及响应。若没有可操作页面，从首页实际返回的链接、脚本和配置中找调用地址；没有找到就停止猜路径，需补镜像说明或构建来源。
3. 只有在捕获到实际 Hessian 请求后，才确认序列化协议版本、RPC 方法和参数结构；再用支持该 Hessian 格式的工具构造请求。按服务端实际依赖与可用类选择兼容载荷，不要把通用 Java 序列化字节流或未经确认的 gadget 直接塞进请求。
4. 重放时只替换已识别的序列化对象/参数，保持捕获到的路径、方法、请求头和封装格式；对比响应确认请求确实进入目标 Hessian 调用。具体利用链仍需由该镜像的依赖与案例来源补证。

## 现场需确认

题库目前只给出镜像名和内部端口。现场还需从真实流量或镜像说明确认：Vulfocus 外部映射地址/端口、应用页面或 context path、Hessian 调用路径、HTTP 方法、`Content-Type`、Hessian 协议版本、RPC 方法与参数，以及服务端依赖中是否存在可用 gadget。未确认这些条件前，这是一套识别入口和构造请求的通用起手流程，不代表已得到可执行的 RCE 链。

## 特有排坑

- **入口和 Content-Type 以捕获的真实请求为准。**仅凭题名不要假设是 Dubbo、Spring HessianServiceExporter 或某个固定 `/service` 路径。
- **载荷格式要与协议和服务端依赖匹配。**不要把“使用 Hessian”直接等同于某个 ysoserial gadget 可用；需要先确认服务端实际反序列化的对象类型与依赖条件。
- **8080 是容器内部端口。**从 Vulfocus 页面显示的实例映射访问，不要默认外部也使用 8080。

## 来源

- **[S1] Vulfocus 官方项目说明：**[fofapro/vulfocus README](https://github.com/fofapro/vulfocus) — 说明 Vulfocus 可集成 Docker 漏洞镜像，镜像可从 Docker Hub 拉取或由管理员上传。该文档不介绍 `vulfocus/hessian:latest` 的具体漏洞案例；因此本卡只给通用识别流程，不据此推断镜像专属入口或利用链。

来源清单：[`../sources/041_hessian/_meta.md`](../sources/041_hessian/_meta.md)
