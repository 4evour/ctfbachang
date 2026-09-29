# 129｜OWASP Hackademic Challenges 多关卡练习

- 镜像：`vulfocus/hackademic`
- 题库端口：`80,3306`；Web 走 `80`，`3306` 是 MySQL。无 CVE。未找到该 Vulfocus 镜像专属 WP。[S1][S2]

## 一句话打法

这是课堂用的多场景练习平台（官方写明当前 **10** 个 Web 场景），不是单一 RCE。打开首页按列表进关，一关一种检查点。[S1][S2]

## 操作步骤

1. 访问 `http://<靶场IP>:80/`。若出现安装向导：填管理员与数据库（本机 MySQL 在容器 `3306`），装完再用提示 URL 登录。已装好则从首页挑战列表进入。[S1][S2]

2. 以页面实际列出的关卡为准。GitHub `next` 分支在 `challenges/ch001`… 下还有更多目录，**不能**假定本题镜像等于仓库全量。官方建议按首页顺序。[S1][S3]

3. 经典 10 关（thefluffy007 题解，路径以首页链接为准，不要硬套别的靶场 URL）：[S4][S5][S6][S7][S8][S9]

   | 关卡 | 题解做法 |
   |---|---|
   | 1 | 看源码（含白色字）、进隐藏目录读邮箱列表，按剧情“周五 13 号”找到联系邮箱并从站点面板发出。 |
   | 2 | 源码里 `GetPassInfo()` 等 JS，在解释器里看返回值，再把得到的口令提交。 |
   | 3 | 目标是弹出写有 `XSS!` 的 alert；题解按页内 POST 做 XSS。 |
   | 4 | 过滤了 `<>()` 一类字符；题解用 `alert(String.fromCharCode(88,83,83,33))`。 |
   | 5 | 改请求头 `User-Agent` 为题目里的 `p0wnBrowser`。 |
   | 6 | 解码页面 JS，在函数里找真正用于校验的口令（注释掉的不是）。 |
   | 7 | 源码目录 `index_files` 泄露上次登录用户；改 Cookie 里的 `userlevel` 为 `admin`。 |
   | 8 | Web 壳里 `ls` 找到 `b64.txt`，解码后 `su`。 |
   | 9 | 源码有隐藏 `page=answer.php`；题解改 User-Agent 上传 hint 中的 `shell.txt`。**具体 UA 字符串在该文截图里，此处不补造。** |
   | 10 | 把隐藏域 `LetMeIn` 从 `false` 改成 `true` 再提交，解码弹出的串得到 serial 后填表。 |

## 本题特有排坑

- 不要当成 VulnHub **Hackademic RTB1**（WordPress + 内核提权那台 VM）；本题端口形态是 PHP 站点 + MySQL。[S1][S2]
- 未找到 `vulfocus/hackademic` 专属题解；上表来自 OWASP 项目的经典 10 关，context path / 是否预装以首页为准。[S1][S4]
- 仓库后加的 `ch011+` 等关，没有写进官方“当前 10 个场景”的说明，也没有收入上表。[S1][S3]
- 第 3 关题解示例偏简，以页面是否弹出 `XSS!` 为准，不要把别的 XSS 靶场 payload 硬套进来。[S4]

## 来源

- [S1] 项目 README：10 个场景、PHP+MySQL、按首页顺序。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S2] OWASP Wiki：课堂练习应用说明。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S3] GitHub `challenges/` 目录。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S4] thefluffy007 关卡题解索引（5、7–10）。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S5] Challenge 1。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S6] Challenge 2。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S7] Challenge 3。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S8] Challenge 4。详见[来源清单](../sources/129_hackademic/_meta.md)。
- [S9] Challenge 6。详见[来源清单](../sources/129_hackademic/_meta.md)。
