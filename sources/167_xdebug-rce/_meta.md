# 第167题来源｜Xdebug 远程调试 RCE

## 题库字段（本地资料，不计外部来源数）

- 题名：`vulfocus/xdebug-rce`
- 镜像：`vulfocus/xdebug-rce`
- 题库端口：`80`
- 无 CVE

## 外部来源（3 个唯一链接）

### [S1] Vulhub 官方 README（中文）

- 链接：[php/xdebug-rce/README.zh-cn.md](https://github.com/vulhub/vulhub/blob/master/php/xdebug-rce/README.zh-cn.md)
- 用途：2.x/3.x 配置、`XDEBUG_SESSION_START`、9000/9003、`exp.py` 命令与回连要求。支撑全部步骤。

### [S2] Vulhub 利用脚本

- 链接：[exp.py](https://github.com/vulhub/vulhub/blob/master/php/xdebug-rce/exp.py)
- 用途：DBGp eval、触发参数。

### [S3] Docker Hub

- 链接：[vulfocus/xdebug-rce](https://hub.docker.com/r/vulfocus/xdebug-rce)
- 用途：确认镜像存在。Hub 无独立复现说明。
