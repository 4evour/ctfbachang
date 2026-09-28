# glzjin/upload-labs 多关卡文件上传靶场

> **定位：**题库只给出 `glzjin/upload-labs:latest`，没有 CVE，也没有 Pass 编号。Upload-Labs 按关卡训练不同的上传校验绕过；因此不能替题目选定一条漏洞链。下表只整理直接题解覆盖的 Less-1 至 Less-10，先看目标实际关卡，再套对应步骤。[S1][S2][S3][S4]

- 内部端口：`80`。
- 直接题解：博客园《Upload-labs 闯关（一）》，覆盖 Less-1 至 Less-10；该文的具体部署路径不等于本题已确认路径。[S4]

## 操作步骤

1. 打开 Vulfocus 映射到容器 `80` 的地址；只有目标页面确实显示 Pass/Less 编号时，才按编号选择对应步骤。题库没有指定关卡，若页面无法确认编号，**不要预先选某个绕过方式**。[S1][S2][S3]
2. 在关卡页面提交测试文件，用 Burp 捕获上传请求；按下表找到对应关卡，只改该关检查的文件名或请求字段后重放。[S4]
3. 以该关原本拒绝的文件被接受作为绕过信号。若页面编号超出 Less-1 至 Less-10，本卡片的博客来源未覆盖。[S4]

## Less-1 至 Less-10 快速步骤

| 关卡 | 对应操作 | 关键条件/排坑 |
|---|---|---|
| Less-1 | 绕过前端 JavaScript 校验：禁用页面脚本，或用 Burp 重放请求并修改 multipart 文件名后缀。[S4] | 只绕过前端检查；若服务端另有校验仍会被拒绝。 |
| Less-2 | 在 Burp 中修改上传文件部分的 `Content-Type` 为页面允许的图片 MIME，再重放请求。[S4] | 只针对 MIME 检查；不要误认为它同时绕过扩展名检查。 |
| Less-3 | 对黑名单未覆盖、且服务器会按 PHP 处理的替代扩展名进行测试；文章示例为 `.phtml`。[S4] | 依赖服务端扩展名映射；目标不支持时此链不成立。 |
| Less-4 | 先将 Apache `AllowOverride None` 改为 `All`，再上传内容为 `SetHandler application/x-httpd-php` 的 `.htaccess`，随后测试上传图片后缀文件。[S4] | 依赖 Apache 和允许目录级配置；题解中的服务端配置步骤不等于远程上传者可修改目标配置。 |
| Less-5 | 把文件名后缀改为文章示例 `webshell.Php` 后重放。[S4] | 依赖大小写敏感的校验逻辑。 |
| Less-6 | 在 `.php` 后添加空格后重放请求。[S4] | 代理需保留尾随空格，且目标校验与保存时的处理存在差异。 |
| Less-7 | 把文件名写成 `.php.` 后重放。[S4] | 题解依赖 Windows 文件名处理；不能直接套到 Linux 环境。 |
| Less-8 | 在 `.php` 后追加 `::$DATA` 再重放请求。[S4] | Windows/NTFS 特有，不适用于一般 Linux 文件系统。 |
| Less-9 | 按题解用 `.php. .` 形式测试点号/空格清理顺序。[S4] | 依赖目标清理顺序；以保存后的文件名为准。 |
| Less-10 | 按题解所述检查扩展名字符串替换逻辑，利用重复片段避开替换。[S4] | 文章可读文字没有完整文件名示例；不补造具体 Payload。 |

## 来源

- **[S1] 题库镜像：**[Docker Hub — glzjin/upload-labs](https://hub.docker.com/r/glzjin/upload-labs) — 与题库镜像名对应；现有页面信息不足以确定镜像内具体 Pass。
- **[S2] Upload-Labs 项目说明：**[c0ny1/upload-labs — README](https://github.com/c0ny1/upload-labs) — 说明项目按多个文件上传 Pass 组织，支持将题目归类为多关卡靶场；不能据此锁定 Vulfocus 镜像的具体关卡。
- **[S3] 项目关卡菜单：**[c0ny1/upload-labs — menu.php](https://github.com/c0ny1/upload-labs/blob/master/menu.php) — 展示 Pass 编号入口，支撑“先确定实际关卡，再选对应链路”的步骤。
- **[S4] 直接关卡题解：**[博客园 — Upload-labs 闯关（一）](https://www.cnblogs.com/wwcdg/p/15913940.html) — 逐关记录 Less-1 至 Less-10 的检查点、请求/文件名改法及平台或配置条件；支撑操作步骤和速查表。文章中的部署路径、OS 和服务端配置不是本题镜像的已知信息。

来源清单：[`../sources/034_glzjin-upload-labs/_meta.md`](../sources/034_glzjin-upload-labs/_meta.md)

