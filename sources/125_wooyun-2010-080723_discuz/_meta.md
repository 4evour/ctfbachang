# 第125题来源｜wooyun-2010-080723 Discuz 6/7 GLOBALS

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/discuz-wooyun-2010-080723`
- 镜像：`vulfocus/discuz-wooyun_2010_080723:latest`（Hub 描述：`admin:admin`）
- 题库端口：`80,3306`
- 编号：`wooyun-2010-080723`（无 CVE）

## 外部来源（3 个唯一链接）

### [S1] Vulhub 官方复现 README

- 链接：[discuz/wooyun-2010-080723/README.md](https://github.com/vulhub/vulhub/blob/master/discuz/wooyun-2010-080723/README.md)
- 用途：说明 PHP 5.3 `request_order=GP` 导致可用 Cookie 覆盖 `$GLOBALS`；给出 `viewthread.php` + `GLOBALS[_DCACHE][smilies][searcharray]=/.*/eui` / `replacearray=phpinfo();` 请求；并注明不强制表情帖。支撑步骤 1–3 与排坑。Vulhub 端口 8080，本题内部端口 80。

### [S2] Seebug 漏洞记录

- 链接：[Discuz! $_DCACHE 代码执行漏洞（SSV-88026）](https://www.seebug.org/vuldb/ssvid-88026)
- 用途：确认测试版本 6.x/7.x、触发文件 `include/discuzcode.func.php` 的 `preg_replace` `/e`、以及访问 `viewthread.php` 验证 `phpinfo()`。支撑步骤 2–3。

### [S3] 专业技术复现

- 链接：[Discuz 7.x/6.x 全局变量防御绕过导致代码执行](https://www.cnblogs.com/lyh1/p/16872592.html)
- 用途：与 Vulhub 相同的 Cookie 请求对照，支撑步骤 2。文章环境需自行安装论坛，Vulfocus 镜像是否已预装以首页为准。
