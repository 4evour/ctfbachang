# 041 — Hessian 反序列化来源清单

## [S1] Vulfocus 官方项目说明
- 链接：[GitHub — fofapro/vulfocus README](https://github.com/fofapro/vulfocus)
- 类型：Vulfocus 官方平台说明；非本题漏洞复现或 PoC。
- 支持内容：说明平台以 Docker 镜像集成漏洞环境，并可从 Docker Hub 拉取镜像或上传本地镜像文件。卡片据此限定：题名和镜像标签不足以确定具体案例，先通过实际页面与请求识别入口和请求格式。
- 不支持内容：该 README 未提及 `vulfocus/hessian:latest`，不提供 Hessian 服务端点、请求格式、payload、gadget 或镜像专属利用步骤。

## 检索结论

按用户限定，仅使用准确题名「Hessian 反序列化」及准确镜像名 `vulfocus/hessian:latest` 查找本镜像直接相关资料；未找到能确认具体案例的专业复现文章或 PoC。未搜索或拼接宽泛 Hessian 链路。当前卡片中的入口识别与请求分析步骤是通用起手流程，不代表已确认该镜像的具体利用链。
