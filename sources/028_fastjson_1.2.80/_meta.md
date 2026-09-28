# 来源清单 — 028 Fastjson 1.2.80 反序列化

- **[S1] 同版本技术复现：**[CTF导航转载 — Fastjson 1.2.80 反序列化利用链分析（作者：blckder02）](https://www.ctfiot.com/60476.html) — 使用 Fastjson `1.2.80`、Groovy `3.0.8`、JDK `8u12`，说明 Groovy ASTTransformation 与远程 classpath 加载链；PoC 主体以图片呈现。支撑依赖条件及链路类型。
- **[S2] 同版本 PoC：**[su18/hack-fastjson-1.2.80](https://github.com/su18/hack-fastjson-1.2.80) — 给出 Groovy 链两段 JSON：Groovy 类型处理请求，以及通过 `classpathList` 指向 `evil.jar` 的远程加载请求。支撑卡片 PoC 片段、顺序和 JAR 前提；不提供本题 HTTP 路径或 JAR 构建材料。
- **[S3] Fastjson 官方安全公告：**[Alibaba Fastjson — security_update_20220523](https://github.com/alibaba/fastjson/wiki/security_update_20220523) — 说明 Fastjson `≤1.2.80` 在特定依赖存在时的安全影响及 AutoType 限制条件。用于限定版本/依赖前提，不提供本题 Payload 或 HTTP 接口。

共 3 个不重复来源链接。
