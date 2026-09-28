# 048 — Java RMI Registry Bind 反序列化来源清单

## 题目范围

- 题名：`java-rmi-registry-bind-deserialization 代码执行`
- 镜像：`vulfocus/java-rmi-registry-bind-deserialization:latest`
- 题库内部端口：`1099`
- CVE：无
- 本卡只整理 classic RMI Registry `bind` 反序列化链。题库提供的 Vulfocus 镜像名和端口是任务输入；公开来源未证明该镜像的构建、JDK 版本和依赖与 Vulhub 同名环境完全相同。另需注意 Vulhub 同名环境 README 标题版本（≤8u111）与 compose 镜像标签（8u131）本身不一致。

## [S1] 同名环境直接复现
- 链接：[Vulhub — Java ≤JDK 8u111 RMI Registry 反序列化命令执行](https://github.com/vulhub/vulhub/blob/master/java/rmi-registry-bind-deserialization/README.zh-cn.md)
- 类型：同名靶场环境的复现文档。
- 支持内容：说明 Registry 在 `bind` 过程中反序列化 Remote 对象；该环境使用 `commons-collections:3.2.1`；给出 `RMIRegistryExploit <host> 1099 CommonsCollections6 "curl ..."` 命令，并提醒 Registry 报错不必然代表命令没有执行。
- 不支持内容：README 标题写 JDK 8u111 及以下，但同目录 compose 标签是 8u131，因此该文档与环境版本资料有冲突；不能将其描述为已验证可打通的公开镜像，更不能证明 Vulfocus `latest` 的 JDK、依赖版本或端口映射。

## [S2] RMI Registry 技术分析
- 链接：[浅谈 Java RMI Registry 安全问题](https://www.anquanke.com/post/id/197829)
- 类型：安全资讯平台刊载的 RMI Registry 技术分析译文。
- 支持内容：解释 bind/rebind 对象反序列化；说明 JDK 8u141 前来源检查发生在反序列化之后，及 JDK 8u121 引入的白名单过滤会拒绝旧版 `RMIRegistryExploit` 使用的非白名单对象。卡片仅引用 classic bind 与旧版链的版本边界。
- 不支持内容：不确认 Vulfocus 镜像版本。文章还讨论其他触发路径，本卡不使用那些步骤。

## [S3] ysoserial `RMIRegistryExploit` 源码
- 链接：[frohoff/ysoserial — RMIRegistryExploit.java](https://github.com/frohoff/ysoserial/blob/master/src/main/java/ysoserial/exploit/RMIRegistryExploit.java)
- 类型：PoC/利用器源代码。
- 支持内容：命令行参数的 host、port、payload 名称与 command；构造 gadget 对象，以动态代理包装为 `Remote` 并调用 `registry.bind(name, remote)`。
- 不支持内容：不证明目标含有相应 gadget 依赖，不确认目标 JDK/过滤设置，也不证明本 Vulfocus 镜像可被该链利用。

## [S4] Oracle JDK 8u121 官方发布说明
- 链接：[Java SE Development Kit 8, Update 121 Release Notes](https://www.oracle.com/java/technologies/javase/8u121-relnotes.html)
- 类型：Oracle 官方版本发布说明。
- 支持内容：记录 RMI Registry 与 DGC 使用 JEP 290 序列化过滤，并实现内置白名单过滤器；用于判断经典 gadget 链的版本适用性。
- 不支持内容：不提供本题 PoC，也不识别 Vulfocus 镜像使用的 JDK。

## [S5] 同名环境 Compose 配置
- 链接：[Vulhub docker-compose.yml](https://raw.githubusercontent.com/vulhub/vulhub/master/java/rmi-registry-bind-deserialization/docker-compose.yml)
- 类型：同名环境的容器编排配置。
- 支持内容：指定镜像标签 `vulhub/j2ee:8u131` 并映射 `1099:1099`。该版本与 README 标题中的 `≤8u111` 不一致，应并列记录。
- 不支持内容：不证明 Vulfocus `latest` 使用此镜像，也不能单凭镜像标签确认实际 JDK build。

## 链路与证据边界

- 文档中的 classic 链路：`RMIRegistryExploit` 构造 Commons Collections gadget → 包装为 Remote 代理 → 对目标 Registry 的 `bind` 发送对象 → Registry 反序列化并触发命令 → 通过攻击侧可达回连服务观察执行结果。
- README 声称环境为 JDK 8u111 及以下并使用 `commons-collections:3.2.1`，但 compose 使用 `vulhub/j2ee:8u131`；公开资料对同名环境的版本存在冲突。不能把这份复现描述为已确认适用于 Vulfocus 镜像。
- Oracle 资料表明从 JDK 8u121 起 RMI Registry 使用内置序列化过滤。若目标版本/过滤配置不符合 classic 链的条件，本卡没有把其它 RMI 路径拼接进来。
- 未实测；未写 Flag；未保存原文。
