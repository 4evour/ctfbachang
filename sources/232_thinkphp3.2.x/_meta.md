# 第232题来源｜ThinkPHP 3.2.x 日志包含

## 题库字段（本地资料，不计外部来源数）

- 题名：`thinkphp3.2.x 代码执行`
- 镜像：`vulfocus/thinkphp-3.2.x`（NOSEC 竞赛表 `vulfocus/thinkphp-3.2.x:latest`）
- 题库端口：`80,3306`
- 无 CVE。fofapro images/README 未列出该仓库名，镜像以竞赛 WP 与题解标题为准。

## 外部来源（6 个唯一链接）

### [S1] Vulfocus 题解

- 链接：[Vulfocus靶场 | thinkphp3.2.X代码执行](https://www.cnblogs.com/mlxwl/p/16558822.html)
- 用途：抓包写入后访问 `/index.php?m=Home&c=Index&a=index&value[_filename]=./Application/Runtime/Logs/Common/YY_MM_DD.log`，出现 phpinfo。支撑步骤 3 与 Common 日志路径。第一步改包细节在文中以截图给出，参数以 [S2] 补全。

### [S2] 同题日志 RCE 步骤

- 链接：[vulfocus thinkphp-3.2.x_thinkphp3.2.x log rce](https://blog.csdn.net/A1bewhy/article/details/123676942)
- 用途：标题含 vulfocus thinkphp-3.2.x；`GET ...&test=--><?=phpinfo();?>`；debug 关→`Logs/Common`、开→`Logs/Home`。支撑步骤 2。

### [S3] 原理通报

- 链接：[【漏洞通报】ThinkPHP3.2.x RCE漏洞通报](https://cloud.tencent.com/developer/article/1855060)
- 用途：`assign` 第一参数可控 → `extract` 覆盖 → `include` 日志；3.2.3 用 `_filename`，3.2/3.2.1 用 `filename`。支撑一句话打法与版本差异。Seebug SSVid-99297 为同类条目。

### [S4] Vulhub ThinkPHP 2.x（对照，勿套用）

- 链接：[vulhub/thinkphp/2-rce/README.md](https://github.com/vulhub/vulhub/blob/master/thinkphp/2-rce/README.md)
- 用途：2.x（及 3.0 Lite）是 `preg_replace /e`，PoC `index.php?s=/index/index/name/${@phpinfo()}`。支撑“不要当 3.2.x 打法”。

### [S5] Vulhub ThinkPHP 5.0.23（对照，勿套用）

- 链接：[vulhub/thinkphp/5.0.23-rce/README.md](https://github.com/vulhub/vulhub/blob/master/thinkphp/5.0.23-rce/README.md)
- 用途：`POST /index.php?s=captcha` + `_method=__construct&filter[]=system`。支撑“不要用 TP5 invokefunction/construct”。

### [S6] 3.2 缓存写入（非本题已验证入口）

- 链接：[Thinkphp3.2.3-5.0.10缓存漏洞](http://h3art3ars.github.io/2019/12/16/Thinkphp3-2-3-5-0-10%E7%BC%93%E5%AD%98%E6%BC%8F%E6%B4%9E/)
- 用途：`S('name', I('post.a3'))` 时可用 `%0d%0a` 绕 `//` 注释写 Temp 下 php。需要应用调用 `S()`。支撑排坑“不是 Vulfocus 默认通关链”。

镜像名来源：[NOSEC Vulfocus 竞赛 WP](https://www.nosec.org/home/detail/4944.html) 第 4 题 `vulfocus/thinkphp-3.2.x:latest`。
