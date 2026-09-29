# 150｜ThinkPHP 5.0.24（无 CVE）

- 镜像：`vulfocus/thinkphp-5.0.24`
- 题库端口：`80`。无 CVE。
- **待补：**未找到可确认属于本题 Vulfocus 镜像、且针对 **5.0.24 默认入口仍可打** 的专业题解。不要把 5.0.23 的 `invokefunction` / `_method=__construct` 链当成已验证打法。[S1][S2][S3][S4][S5]

## 一句话打法

5.0.24 是官方对 5.0.x `Request::method` 远程命令执行的安全更新；在未证实镜像另开了反序列化入口之前，没有可执行的默认 RCE 链。[S1][S2][S3][S4]

## 操作步骤

1. 打开映射到容器 `80` 的站点，确认是否为 ThinkPHP 5 页面。这一步只用来识别框架，不构成利用。[S6]
2. **不要**发送 5.0.23 常用包，例如：
   - GET `?s=index/think\app/invokefunction&function=call_user_func_array&...`
   - POST `_method=__construct&filter[]=system&...`
   官方把 5.0.0–5.0.23 列为受影响、5.0.24 为修复版；绿盟/逐版本测试都写明 5.0.24 给 `method` 加了 GET/POST/DELETE/PUT/PATCH 白名单，`__construct` 进不去。控制器名正则也在 **大于 5.0.23** 后拦截 `think\app` 这类带反斜杠的类名。[S1][S3][S4][S5]
3. 公开资料里 5.0.24 仍被讨论的是**框架 POP 反序列化写文件**，前提是二次开发里存在可控 `unserialize()`。默认 `index` 控制器没有这个入口；本题镜像没有专属 WP 证明它加了 sink，因此**不写 Payload**。[S5]

## 本题特有排坑

- 镜像名就是 **5.0.24**，与“ThinkPHP 5.0.23 RCE”不是同一题；套 5.0.23 链失败不能用来反推“版本其实是 5.0.23”。[S1][S2]
- `_method=__construct` 在 5.0.24 的 `Request::method` 白名单下会落到普通 POST，不再任意调类方法。[S3][S4]
- `?s=index/\think\Request/input&filter[]=` 出现在 **5.1.x** 未强制路由分析里，不是已证实的 5.0.24 默认链。[S5]

## 来源

- [S1] ThinkPHP 官方博客：5.0.24 安全更新，受影响 5.0.0–5.0.23。详见[来源清单](../sources/150_thinkphp-5.0.24/_meta.md)。
- [S2] GitHub `v5.0.24` 发布说明。详见[来源清单](../sources/150_thinkphp-5.0.24/_meta.md)。
- [S3] 官方提交：改进 `Request::method`。详见[来源清单](../sources/150_thinkphp-5.0.24/_meta.md)。
- [S4] 绿盟：白名单补丁与 5.0.x PoC 边界。详见[来源清单](../sources/150_thinkphp-5.0.24/_meta.md)。
- [S5] 逐版本 RCE 总结：5.0.24 节写明 method 链已修；反斜杠控制器在 >5.0.23 被正则挡。详见[来源清单](../sources/150_thinkphp-5.0.24/_meta.md)。
- [S6] Docker Hub 镜像页：与题库名对应。详见[来源清单](../sources/150_thinkphp-5.0.24/_meta.md)。
