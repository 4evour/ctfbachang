# 034 glzjin/upload-labs 来源清单

共 4 个唯一来源链接。题库没有给出 Pass 编号；来源能确认 Upload-Labs 是多关卡训练项目，直接题解覆盖 Less-1 至 Less-10，但不能确定 Vulfocus 镜像具体对应哪一关。

- **[S1] 题库镜像仓库 — glzjin/upload-labs**  
  https://hub.docker.com/r/glzjin/upload-labs  
  与题库镜像名对应。现有页面信息不足以确定镜像内具体 Pass；只支撑镜像身份和“关卡未确认”的范围说明，不支撑绕过步骤。

- **[S2] Upload-Labs 项目 README — c0ny1/upload-labs**  
  https://github.com/c0ny1/upload-labs  
  项目说明和部署入口，展示其按多个 Pass 组织的训练形式。支撑卡片对多关卡靶场的判断；不能据此断定 Vulfocus 镜像的具体版本或关卡。

- **[S3] Upload-Labs 项目菜单 — menu.php**  
  https://github.com/c0ny1/upload-labs/blob/master/menu.php  
  展示 Pass 编号入口。支撑操作步骤 1 中先识别页面实际关卡，再选择对应链路的做法；不用于推断 Vulfocus 镜像的关卡数。

- **[S4] 直接题解 — 博客园《Upload-labs 闯关（一）》**  
  https://www.cnblogs.com/wwcdg/p/15913940.html  
  逐关覆盖 Less-1 至 Less-10：前端校验、MIME 类型、替代扩展名、Apache `.htaccess`、大小写、空格/点号处理和 NTFS 数据流等。支撑卡片操作步骤 2–3、快速步骤表以及相关平台/配置条件。文章使用作者自己的部署环境；Less-10 的可读文字没有完整文件名示例，所以卡片未补写 Payload。
