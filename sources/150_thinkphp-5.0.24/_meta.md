# 第150题来源｜vulfocus/thinkphp-5.0.24

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/thinkphp-5.0.24`
- 镜像：`vulfocus/thinkphp-5.0.24`
- 题库端口：`80`
- 无 CVE；未找到可确认的本题镜像默认 RCE 题解。

## 外部来源（6 个唯一链接）

### [S1] ThinkPHP 官方博客（安全更新）

- 链接：[ThinkPHP5.0.24版本发布——安全更新](https://www.kancloud.cn/top-think/thinkphp-blog/910675)
- 用途：官方写明本次为可能 GetShell 的安全更新，**受影响版本 5.0.0～5.0.23**，不能升级时按最新 `Request::method` 手工修。支撑“5.0.24 是修复版、不要套 5.0.23 链”。

### [S2] 官方版本标签

- 链接：[top-think/framework v5.0.24](https://github.com/top-think/framework/releases/tag/v5.0.24)
- 用途：发布说明列出“改进 Request 类的 method 方法”。支撑版本边界。

### [S3] 官方修复提交

- 链接：[commit 4a4b5e6 改进Request类](https://github.com/top-think/framework/commit/4a4b5e64fa4c46f851b4004005bff5f3196de003)
- 用途：补丁改 `library/think/Request.php`。与 [S1][S4] 的 method 白名单修复一致。支撑 construct 链排坑。

### [S4] 绿盟全版本分析

- 链接：[ThinkPHP 5.0.x-5.0.23、5.1.x、5.2.x 全版本远程代码执行漏洞分析](https://blog.nsfocus.net/thinkphp-full-version-rce-vulnerability-analysis/)
- 用途：影响范围写到 5.0.x～5.0.23；PoC `_method=__construct&filter=system&method=get&server[REQUEST_METHOD]=id` 针对该区间；补丁把 `$this->method` 限制为 GET/POST/DELETE/PUT/PATCH。支撑步骤 2 与 method 链排坑。5.1.x 的 `_method=filter` 不是 5.0.24。

### [S5] 逐版本测试总结

- 链接：[Thinkphp5 RCE总结](https://www.cnblogs.com/nongchaoer/p/12029478.html)
- 用途：在 5.0.24 小节写“作为 5.0.x 的最后一个版本，rce 被修复”；未强制路由的 `invokefunction` 示例标在 5.0.x，并写明 **大于 5.0.23** 用正则校验控制器名。`?s=index/thinkRequest/input` 出现在 5.1.x 分析。支撑“不要复制 5.0.23 invokefunction / construct 链”。作者提到反序列化姿势，但没有给本题镜像的 unserialize 入口。

### [S6] 题库镜像仓库

- 链接：[Docker Hub — vulfocus/thinkphp-5.0.24](https://hub.docker.com/r/vulfocus/thinkphp-5.0.24)
- 用途：确认存在与题库同名的镜像。页面无 overview，不能证明默认应用是否暴露反序列化或其它入口。

公开链路限制：目前没有能确认本题 Vulfocus 镜像在 5.0.24 默认路由上仍可 RCE 的专业题解；框架 POP 反序列化需要应用层 `unserialize()`，不能当成已验证入口。
