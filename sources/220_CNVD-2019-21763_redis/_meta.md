# 第220题来源｜CNVD-2019-21763 Redis

## 题库字段（本地资料，不计外部来源数）

- 题名：`redis 未授权访问 (CNVD-2019-21763)`
- 镜像：`vulfocus/redis-cnvd_2019_21763`
- 题库端口：`6379`
- 官方/转载是 4.x+ module rogue replica，不是 crontab、不是 CVE-2015-4335。

## 外部来源（5 个唯一链接）

### [S1] 山东大学转载

- 链接：[CNVD-2019-21763](https://cybersecurity.sdu.edu.cn/info/1017/1029.htm)
- 用途：modules、披露日期。支撑编号校正。

### [S2] Seebug Paper

- 链接：[paper.seebug.org/975](https://paper.seebug.org/975/)
- 用途：CNVD 引用的技术文。支撑 module 原语。

### [S3] 腾讯云复现

- 链接：[CNVD-2019-21763 复现](https://cloud.tencent.com/developer/article/1627282)
- 用途：rogue-server，不是 crontab。支撑步骤 1–3。

### [S4] CSDN / Vulfocus 题名复现

- 链接：[CNVD-2019-21763](https://blog.csdn.net/weixin_44971640/article/details/128117510)
- 用途：以 Vulfocus 本题为题的 module RCE。支撑一句话打法。

### [S5] NVD CVE-2015-4335（对照，不计逐步 Payload）

- 链接：[NVD](https://nvd.nist.gov/vuln/detail/CVE-2015-4335)
- 用途：Lua EVAL 沙箱逃逸，明确不是本 CNVD。支撑「不要标成 4335」。
