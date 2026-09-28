# 047 — java-rmi-codebase 代码执行 来源清单

## [S1] 同题环境复现（CSDN）
- 链接：https://blog.csdn.net/AsagiRiAsagi/article/details/129591849
- 类型：标题对应 `java-rmi-codebase` 的 Vulhub 环境复现文章。
- 支持内容：确认这篇资料讨论的是同名 Java RMI codebase 环境，可用于关联题目背景。
- 不支持内容：当前可访问页面正文受限；本卡不据此声称已核对 Vulfocus `latest` 的 Dockerfile、JVM 参数、端口或完整操作命令。

## [S2] RMI codebase 直接复现（天下大木头）
- 链接：https://wjlshare.com/archives/1522
- 类型：Java RMI codebase 原理与直接复现文章。
- 支持内容：演示 `RemoteRMIServer` 注册 `refObj`；`ICalc.sum(List<Integer>)` 接收 `Payload extends ArrayList<Integer>`；客户端以 `java.rmi.server.codebase` 指向 HTTP 类文件服务，并展示 `useCodebaseOnly=false`、SecurityManager/策略文件及代码下载过程。
- 不支持内容：文章示例不是 Vulfocus 镜像的构建说明，不能证明 `vulfocus/java-rmi-codebase:latest` 使用完全相同的 JDK、stub 地址、固定服务端口或启动参数。

## [S3] Oracle Java RMI 官方 codebase 文档
- 链接：https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/codebase.html
- 类型：Oracle Java SE 8 官方技术文档。
- 支持内容：说明 Java RMI 可用客户端设置的 codebase 注解传递自定义子类位置；当接收 JVM 找不到参数对象的类定义时，会尝试从 codebase 下载；目录形式的 codebase URL 需以 `/` 结尾，并列出动态类下载条件。
- 不支持内容：不涉及 VulFocus/Vulhub 题目、`refObj` 名称、payload 行为或镜像参数。

## [S4] Oracle Java RMI 官方 FAQ
- 链接：https://docs.oracle.com/javase/7/docs/technotes/guides/rmi/faq.html
- 类型：Oracle Java SE 7 官方 RMI 与对象序列化 FAQ。
- 支持内容：Registry 返回的远程引用包含服务端主机和端口；客户端取得引用后会按该地址连接远程对象。因此，Registry 可访问与远程方法调用可访问是两项不同的网络条件。
- 不支持内容：不涉及本题具体端口映射、漏洞触发或 codebase payload。

## 卡片边界

资料支持的直接利用思路是：客户端通过 RMI Registry 获取远程对象引用，向其对象参数传入服务端本地 classpath 中没有的可序列化子类，并让该类的 codebase 指向可被目标访问的 HTTP 类文件目录；目标配置允许远程类加载时，在反序列化/类加载路径触发后续行为。原始复现使用 `refObj` 与 `ICalc.sum(List<Integer>)`，但没有足够证据确认 Vulfocus `latest` 镜像与原始环境逐项相同，所以卡片要求核对 registry 绑定与 stub 实际地址；没有把其他 RMI/JNDI 链路拼进来。未实测、未写 Flag。

