# httpd-ssi 命令执行

> **题库信息：**题名「httpd-ssi 命令执行」；镜像 `vulfocus/httpd-ssi:latest`；内部端口 `80`；无 CVE。
>
> **一句话打法：**若能通过题目实际提供的文件写入方式把 `.shtml` 放进 Web 可访问目录，在其中写入 `<!--#exec cmd="id" -->` 并 GET 该文件；响应体出现 `uid=` / `gid=` 命令输出即表明 SSI 命令执行。公开复现支持这条 Apache SSI 链，但没有确认该 Vulfocus 镜像的上传入口和配置。

## 操作步骤

1. 启动实例，访问 Vulfocus 分配给容器内部 `80` 端口的地址。只使用页面或实际请求中找到的文件上传/写入功能；公开资料没有给出本镜像的入口、表单字段或上传路径，不要自行猜测。[S1]
2. 若确实存在可用的写入方式，将文件名设为 `test.shtml`，内容为：

   ```html
   <pre><!--#exec cmd="id" --></pre>
   ```

   公开复现使用 `.shtml` 和 `#exec cmd="id"`；Apache 官方文档说明 `exec` 会由 shell 执行命令并把输出插入页面。[S1][S2]
3. 用浏览器访问该文件，或将实际 URL 代入以下命令发起 GET：

   ```bash
   curl -i 'http://<Vulfocus分配地址>/<实际文件路径>/test.shtml'
   ```

   响应体中出现类似 `uid=...`、`gid=...` 的 `id` 输出是成功信号；HTTP 200 本身不代表命令执行。若源码中的 SSI 注释原样返回，说明该文件没有经过 SSI 解析。[S1][S2]

## 前提与特有排坑

- SSI 需由 Apache `mod_include` 处理；目录允许 `Options +Includes`，并将 `.shtml` 映射到 SSI 输出过滤器（官方示例为 `AddType text/html .shtml` 与 `AddOutputFilter INCLUDES .shtml`）。题库和公开复现没有证明这些配置在目标镜像中的具体状态。[S2]
- `Options IncludesNOEXEC` 会禁止 `exec` 命令；SSI 标记能被处理，不等于命令执行一定允许。[S2]
- 使用 `.shtml`，不要默认 `.html` 也会被解析；Apache 需要相应的文件扩展名/过滤器配置。`XBitHack` 是另一种配置方式，但不能据此推断本镜像启用了它。[S2]
- `#exec cmd` 直接由 shell 执行，不要求 CGI；不要把 CGI 可用当成本链前提。[S2]
- `.shtml` 只解决 SSI 文件识别问题，不会自动提供上传能力。没有找到镜像实际提供的写入入口时，链路停在这里，不补造 URL 或参数。[S1][S2]

## 来源

- **[S1] Apache SSI 命令执行复现：**[Apache服务攻防（含“Apache SSI远程命令执行漏洞”复现）](https://byesec.com/posts/1eb6476e.html) — 该文 SSI 小节展示上传 `test.shtml`、写入 `<!--#exec cmd="id" -->` 并访问文件观察执行结果；不是 `vulfocus/httpd-ssi:latest` 的镜像专属说明。
- **[S2] Apache 官方 SSI 教程：**[Introduction to Server Side Includes](https://httpd.apache.org/docs/2.4/howto/ssi.html) — 支持 `.shtml` 过滤配置、`mod_include`、`Options +Includes`、`#exec cmd` 的执行方式，以及 `IncludesNOEXEC` 的限制。

来源清单：[`../sources/043_httpd-ssi/_meta.md`](../sources/043_httpd-ssi/_meta.md)
