# 043 — httpd-ssi 命令执行来源清单

## [S1] Apache SSI 命令执行复现
- 链接：[Apache服务攻防（含“Apache SSI远程命令执行漏洞”复现）](https://byesec.com/posts/1eb6476e.html)
- 类型：Apache SSI 命令执行实践文章。
- 支持内容：SSI 复现小节给出 `.shtml` 文件、`<!--#exec cmd="id" -->` 指令、上传文件后访问该文件并观察命令执行结果的链路。
- 不支持内容：没有说明 `vulfocus/httpd-ssi:latest` 的上传入口、请求字段、文件落点或 Apache 实际配置；文章其他 Apache 漏洞章节不作为本卡依据。

## [S2] Apache 官方 SSI 教程（httpd 2.4）
- 链接：[Apache httpd Tutorial: Introduction to Server Side Includes](https://httpd.apache.org/docs/2.4/howto/ssi.html)
- 类型：Apache HTTP Server 官方文档。
- 支持内容：`mod_include`、`Options +Includes`、`.shtml` 的 `AddType` / `AddOutputFilter INCLUDES` 配置；`#exec cmd` 通过 shell 执行并把输出写入响应；`IncludesNOEXEC` 可禁用命令执行。该指令不以 CGI 为前提。
- 不支持内容：不描述 Vulfocus 镜像本身、上传入口、文件路径或其当前启用的配置。

## 本题链路边界

限定检索准确题名「httpd-ssi 命令执行」及准确镜像名 `vulfocus/httpd-ssi:latest`，未找到能确认该镜像专属上传入口或配置的直接资料。当前步骤是公开 Apache SSI 复现链与官方配置文档所能支持的最短可复用链路；仅在实际目标确有可用文件写入方式且 SSI/exec 配置满足前提时成立。
