# 第113题来源｜ThinkPHP lang 文件包含/命令执行

## 题库字段（本地资料，不计外部来源数）

- 题名：`thinkphp lang 命令执行`
- 镜像：`vulfocus/thinkphp:6.0.12`
- 题库端口：`80`
- 无 CVE；按多语言 LFI + pearcmd 写文件整理。

## 外部来源（4 个唯一链接）

### [S1] Vulhub 官方复现 README

- 链接：[vulhub/thinkphp/lang-rce](https://github.com/vulhub/vulhub/tree/master/thinkphp/lang-rce)
- 用途：确认 6.0.12 环境、`?lang=../../../../../public/index` 探测、pearcmd `+config-create` 写 `shell.php` 的完整请求。支撑步骤 1–3 与排坑。

### [S2] NOSEC 漏洞通报（Vulfocus 环境）

- 链接：[Thinkphp 多语言模块命令执行漏洞](https://nosec.org/m/share/5050.html)
- 用途：影响 6.0.1–6.0.13 与 5.0.x/5.1.x；给出 `docker pull vulfocus/thinkphp:6.0.12`。支撑镜像与题库对应关系。

### [S3] pearcmd 利用原理

- 链接：[Docker PHP 环境的文件包含 getshell](https://www.leavesongs.com/PENETRATION/docker-php-include-getshell.html)
- 用途：说明 `register_argc_argv` + `pearcmd.php` `config-create` 写文件。支撑步骤 2 与条件排坑。

### [S4] 上游修复

- 链接：[top-think/framework commit c4acb8b](https://github.com/top-think/framework/commit/c4acb8b4001b98a0078eda25840d33e295a7f099)
- 用途：官方对 lang 参数的修复对照。
