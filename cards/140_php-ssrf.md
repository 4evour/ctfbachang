# 140｜php-ssrf

- 题库端口：`80`
- 无 CVE。Docker Hub 上存在镜像 `vulfocus/php-ssrf`，但页面无说明、无 Dockerfile/题解。未找到可确认属于本题 Vulfocus 镜像的专业 WP（参数名、路由、是否 file/gopher/Redis 均未知）。**入口未由本题资料证实**，先对照首页是否出现可提交的 URL 输入，再决定能否复用任何公开 PHP SSRF 链。[S1]

## 一句话打法

待补。在确认页面把用户输入交给服务端请求（`curl` / `file_get_contents` 等）之前，不能把通用 gopher/Redis/FastCGI 链套到本题。[S1]

## 操作步骤

1. 访问 `http://<靶场IP>:80/`。只根据**本页**表单、查询串和源码注释记录真实参数名与路径；题库没有给出路由。[S1]
2. 若存在 URL 类参数，先用页面自己的回显判断服务端是否出站（例如让它请求一个你控制的 HTTP 地址）。不要在未看到参数的情况下假设 `?url=`、`?file=` 或 `file:///var/www/html/...`。[S1]
3. **不要**据此题编造一条 curl→file/gopher→Redis/php-fpm 的载荷。公开 PHP SSRF 靶场（CTFHub、Pikachu 等）的路径和协议与本题镜像没有对应关系，不能当本题步骤。[S1]

## 本题特有排坑

- 镜像在 Docker Hub 能拉到，但 overview 为空，不能从仓库说明推断入口。[S1]
- 题库只有端口 `80`、无 CVE。Vulhub 没有与本题同名的 `php/ssrf` 环境可对齐（有的是 Weblogic/Solr SSRF，不是这张 PHP 镜像）。[S1]
- 未确认包装器时，`gopher://`、`file://`、`php://filter` 都可能根本没开；失败不能靠换通用 payload 解释。[S1]

## 来源

- [S1] Docker Hub 镜像页：确认 `vulfocus/php-ssrf` 存在且无文档。详见[来源清单](../sources/140_php-ssrf/_meta.md)。
