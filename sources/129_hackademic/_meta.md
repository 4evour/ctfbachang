# 第129题来源｜OWASP Hackademic Challenges

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/hackademic`
- 镜像：`vulfocus/hackademic`
- 题库端口：`80,3306`
- 无 CVE。未找到 Vulfocus 本题镜像专属 WP。

## 外部来源（9 个唯一链接）

### [S1] 项目 README

- 链接：[Hackademic/hackademic](https://github.com/Hackademic/hackademic)
- 类型：项目资料。
- 用途：OWASP Hackademic Challenges；当前 10 个 Web 场景；建议按首页顺序；依赖 Apache/nginx + PHP + MySQL/MariaDB；可能先走安装向导。支撑多关卡定位、步骤 1–2，以及不要写成单一 RCE。稳定分支名为 `next`。

### [S2] OWASP Wiki

- 链接：[OWASP Hackademic Challenges Project](https://wiki.owasp.org/index.php/OWASP_Hackademic_Challenges_Project)
- 类型：官方项目页。
- 用途：课堂练习、10 个 Web 场景、PHP+MySQL 部署。支撑“训练应用而非单洞”和端口形态。

### [S3] 挑战目录

- 链接：[hackademic/tree/next/challenges](https://github.com/Hackademic/hackademic/tree/next/challenges)
- 类型：项目源码目录。
- 用途：`ch001`–`ch018` 等文件夹存在，说明仓库关卡数可能多于官方“10 个场景”。支撑“以实例首页列表为准、不把 ch011+ 写进必做表”。

### [S4] 关卡题解索引

- 链接：[thefluffy007 — hackademic-challenge 标签](https://thefluffy007.com/tag/hackademic-challenge/)
- 类型：专业题解（多篇）。
- 用途：Challenge 5（`User-Agent: p0wnBrowser`）、7（`index_files` + Cookie `userlevel`）、8（`b64.txt` + `su`）、9（隐藏 `page`、改 UA 上传 hint 中的 shell；UA 具体值在截图中）、10（隐藏域 `LetMeIn`）。支撑步骤 3 表中 5–10。同作者 Challenge 3/4/6 在相邻博文。

### [S5] Challenge 1 题解

- 链接：[OWASP Hackademic Challenges Project - Challenge 1](https://thefluffy007.com/2017/03/28/owasp-hackademic-challenges-project-challenge-1/)
- 类型：专业题解。
- 用途：看源码找浅色账号、隐藏目录、按“周五 13 号”选邮箱并从站点发信。支撑步骤 3 第 1 关。

### [S6] Challenge 2 题解

- 链接：[OWASP Hackademic Challenges Project – Challenge 2](https://thefluffy007.com/2017/03/29/owasp-hackademic-challenges-project-challenge-2/)
- 类型：专业题解。
- 用途：源码中 `GetPassInfo()`，用 JS 解释器看返回值再提交。支撑步骤 3 第 2 关。

### [S7] Challenge 3 题解

- 链接：[OWASP Hackademic Challenges Project – Challenge 3](https://thefluffy007.com/2017/04/06/owasp-hackademic-challenges-project-challenge-3/)
- 类型：专业题解。
- 用途：目标弹出 `XSS!`；题解示例为 `alert("XSS!");`。支撑步骤 3 第 3 关及该关排坑。

### [S8] Challenge 4 题解

- 链接：[OWASP Hackademic Challenge – Challenge 4](https://thefluffy007.com/2017/04/27/owasp-hackademic-challenge-challenge-4/)
- 类型：专业题解。
- 用途：过滤 `<>()` 后用 `alert(String.fromCharCode(88,83,83,33))`。支撑步骤 3 第 4 关。

### [S9] Challenge 6 题解

- 链接：[OWASP Hackademic Challenge 6](https://thefluffy007.com/2017/04/20/owasp-hackademic-challenge-6/)
- 类型：专业题解。
- 用途：解码页面 JS，注释口令无效，真正用于校验的口令在函数逻辑里。支撑步骤 3 第 6 关。
