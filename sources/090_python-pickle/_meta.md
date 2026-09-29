# 第090题来源｜python-pickle 命令执行

## 题库字段（本地资料，不计外部来源数）

- 题名：`python-pickle 命令执行`
- 题库端口：`8000`
- 无 CVE；未找到可确认的 Vulfocus 本题镜像题解。

## 外部来源（2 个唯一链接）

### [S1] Vulhub 同类环境

- 链接：[Python unpickle 造成任意命令执行](https://vuls.vercel.app/Vulnerability-Wiki/vulhub/Other/Python-unpickle-%E9%80%A0%E6%88%90%E4%BB%BB%E6%84%8F%E5%91%BD%E4%BB%A4%E6%89%A7%E8%A1%8C%E6%BC%8F%E6%B4%9E/)
- 用途：公开 Flask 靶场：端口 8000，Cookie `user` 经 Base64 + `pickle.loads`，默认 `Hello Guest`，以及 `__reduce__`/`os.system` 示例。支撑步骤，并标明**不能自动当成 Vulfocus 本题入口**。

### [S2] 原理说明

- 链接：[Python Pickle命令执行漏洞原理](http://www.hackersb.cn/study/python-pickle-command-execute.html)
- 用途：说明 `__reduce__` 返回 `(os.system, (cmd,))` 在反序列化时执行。支撑 payload 结构。

公开链路限制：目前没有能确认与本题 Vulfocus 镜像同一路由/Cookie 的专业题解。
