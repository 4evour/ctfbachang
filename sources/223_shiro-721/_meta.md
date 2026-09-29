# 第223题来源｜SHIRO-721 / CVE-2019-12422 rememberMe Padding Oracle

## 题库字段（本地资料，不计外部来源数）

- 题名：`shiro-721 代码执行`
- 镜像：`vulfocus/shiro-721`
- 题库端口：`8080`
- 题库无 CVE 字段；公开对应 CVE-2019-12422。勿与第143题 Shiro-550、第05/096/097题路径绕过混淆。

## 外部来源（6 个唯一链接）

### [S1] Apache JIRA SHIRO-721

- 链接：[SHIRO-721 RememberMe Padding Oracle Vulnerability](https://issues.apache.org/jira/browse/SHIRO-721)
- 用途：AES-128-CBC rememberMe 可 Padding Oracle；步骤为登录取合法 Cookie → 当前缀 → 加密 ysoserial → 重放反序列化；不必知道 cipherKey。影响 1.2.5–1.4.1，修到 1.4.2。支撑一句话打法、步骤 1/4–5、版本排坑。

### [S2] 官方公告与 NVD

- 链接：[oss-sec CVE-2019-12422](https://seclists.org/oss-sec/2019/q4/72)
- 用途：Shiro 1.4.2 安全发布：默认 rememberMe 可被 padding 攻击。交叉：[NVD CVE-2019-12422](https://nvd.nist.gov/vuln/detail/CVE-2019-12422)。支撑编号校正与修复版本。NVD 正文偏 padding，RCE 步骤以 [S1][S3] 为准。

### [S3] 公开利用仓库

- 链接：[3ndz/Shiro-721](https://github.com/3ndz/Shiro-721)
- 用途：`deleteMe` 填充判定、`python shiro_exp.py <url> <cookie> payload.class`、短 payload 约 1 小时、升级 1.4.2。支撑步骤 3–5 与耗时排坑。

### [S4] Vulfocus 靶机复现

- 链接：[Shiro550/Shiro721复现](https://syunaht.com/p/3654935441.html)
- 用途：明确靶机 `vulfocus/shiro-721`、CVE-2019-12422、影响 &lt; 1.4.2；脚本对 `sys.argv[1]` URL 发 GET、用 `deleteMe` 当 oracle，入口示例 `/account`。支撑镜像与步骤 2、4。

### [S5] 同镜像 Docker 复现

- 链接：[shiro反序列化复现与审计](https://www.cnblogs.com/Litsasuk/articles/18823428)
- 用途：`docker pull/run vulfocus/shiro-721` 映射 8080；登录后抓 rememberMe 再跑 padding。支撑步骤 2。未在文中写死唯一账号。

### [S6] Vulfocus 官方镜像表

- 链接：[fofapro/vulfocus images/README.md](https://github.com/fofapro/vulfocus/blob/master/images/README.md)
- 用途：`docker pull vulfocus/shiro-721`。支撑镜像名。
