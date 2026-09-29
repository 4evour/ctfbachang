# 168｜xss-labs 多关 XSS 练习

> **教学靶场：**不是单一 CVE。按 `level1.php`–`level20.php` 的过滤逐关打。未找到本 Vulfocus 镜像专属 WP，以下入口来自同源靶场源码与通关笔记。[S1][S2]

- 镜像：`vulfocus/xss-labs`
- 题库端口：`80,3306`

## 操作步骤

1. 打开映射到容器 80 的地址，应能看到关卡入口（`index.php` / `level1.php`）。[S1]
2. Level 1：`name` 无过滤直接进页面。[S2][S3]

   ```text
   /level1.php?name=<script>alert(1)</script>
   ```

   成功信号：浏览器执行脚本；不少实现会跳到下一关。
3. Level 2 起参数多为 `keyword`，payload 要按输出点闭合属性（例如 `"><script>alert(1)</script>`），不要把 Level 1 的 `<script>` 硬套到已 `htmlspecialchars` 的关。[S2][S3]
4. 后续关用替换/`strtolower`/href 限制，按当前页源码构造；卡片不编造 20 关「标准 Flag 链」。[S1]

## 本题特有排坑

- 参数名 **Level1=`name`，其后常见 `keyword`**；用错键看起来像过滤成功。[S2]
- 这是练习场，不是 RCE；3306 不代表每关都有 SQLi。[S1]
- 镜像无 README 时以首页实际文件名为准（有的 fork 放在 `/xss/` 子目录）。[S2]

## 来源

- [S1] 靶场源码仓库（level1–20）。详见[来源清单](../sources/168_xss-labs/_meta.md)。
- [S2] 通关笔记：Level1 `name`、Level2 `keyword`。详见[来源清单](../sources/168_xss-labs/_meta.md)。
- [S3] Level1–5 源码级对照。详见[来源清单](../sources/168_xss-labs/_meta.md)。
- [S4] Docker Hub `vulfocus/xss-labs`。详见[来源清单](../sources/168_xss-labs/_meta.md)。
