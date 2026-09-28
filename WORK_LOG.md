# 工作记录

> 当前进度以 `batches/progress.csv` 与 `index.csv` 为准；逐题步骤见 `cards/`，来源链接与用途见 `sources/`。

## 记录恢复说明（2026-09-28）

原工作记录文件在本轮自动更新时被截断。本页依据仍在的进度表、卡片和来源清单重建摘要；没有这些文件支撑的旧过程细节不作猜测。249 题的逐题状态仍保存在进度表中。

## 截至第076题的进度摘要

- 001｜apache  远程代码执行 （CVE-2021-42013）：已整理：Apache 双重编码路径穿越与 CGI RCE（来源 7）；卡片 `cards/001_CVE-2021-42013_apache.md`。
- 002｜apache-kylin 命令执行 (CVE-2020-1956)：已整理：Kylin Cube Migration 管理员命令注入（来源 4）；卡片 `cards/002_CVE-2020-1956_apache-kylin.md`。
- 003｜apache-nifi-api 代码执行：已整理：NiFi 匿名 API 创建 ExecuteProcess（来源 4）；卡片 `cards/003_apache-nifi-api.md`。
- 004｜apache-shenyu（题库原标CVE-2021-38570；镜像对应CVE-2021-37580）：已整理：ShenYu Admin JWT 认证绕过（编号已校正）（来源 6）；卡片 `cards/004_CVE-2021-37580_apache-shenyu.md`。
- 005｜Arm 64位 Debian环境：已整理：环境/架构识别题（非漏洞利用链）（来源 4）；卡片 `cards/005_arm64_debian_env.md`。
- 006｜Atlassian Jira 路径遍历 （CVE-2021-26086）：已整理：Jira 限定文件读取（来源 4）；卡片 `cards/006_CVE-2021-26086_atlassian-jira.md`。
- 007｜bash 命令执行 （CVE-2014-6271）：已整理：Shellshock CGI 请求头利用链（来源 4）；卡片 `cards/007_CVE-2014-6271_bash.md`。
- 008｜bodgeit 靶场：已整理：BodgeIt Score 漏洞练习路线（来源 5）；卡片 `cards/008_bodgeit.md`。
- 009｜casdoor SQL注入（CVE-2022-24124）：已整理：公开接口 field 参数 SQL 注入错误回显（来源 5）；卡片 `cards/009_CVE-2022-24124_casdoor.md`。
- 010｜cisco 代码执行 （CVE-2020-3331）：已整理：guest_logout.cgi POST 栈溢出 + MIPS ROP 反弹 Shell（来源 3）；卡片 `cards/010_CVE-2020-3331_cisco.md`。
- 011｜cmseasy 远程命令执行 （CNVD-2021-34045）：待补链路：精确编号检索未找到含操作步骤的题解/PoC（来源 2）；卡片 `cards/011_CNVD-2021-34045_cmseasy.md`。
- 012｜coldfusion 代码执行 （CVE-2018-15961）：已整理：CKEditor upload.cfm 上传 JSP 后 GET 执行（来源 4）；卡片 `cards/012_CVE-2018-15961_coldfusion.md`。
- 013｜coldfusion 代码执行 （CVE-2021-21087）：已整理：确认官方分类为 XSS；模板仅支持 cfajax.js 特征探测（来源 2）；卡片 `cards/013_CVE-2021-21087_coldfusion.md`。
- 014｜Confluence OGNL 注入 (CVE-2022-26134)：已整理：URI 路径 OGNL 注入，按版本选链并从响应头取回显（来源 3）；卡片 `cards/014_CVE-2022-26134_confluence.md`。
- 015｜couchdb 权限绕过 （CVE-2017-12635）：已整理：重复 roles 键实现 CouchDB _admin 权限提升（来源 3）；卡片 `cards/015_CVE-2017-12635_couchdb.md`。
- 016｜daemon-api 未授权访问：已整理：Docker Remote API 2375 未授权访问并创建远端容器（来源 4）；卡片 `cards/016_daemon-api_unauthorized.md`。
- 017｜dedecms SQL注入 （CVE-2017-17731）：已整理：recommend.php 的 $_FILES SQL 注入检测链（来源 4）；卡片 `cards/017_CVE-2017-17731_dedecms.md`。
- 018｜dedecms 代码执行 (CNVD-2018-01221)：已整理：tpl.php savetagfile 写入 PHP 文件并访问触发（来源 4）；卡片 `cards/018_CNVD-2018-01221_dedecms.md`。
- 019｜dedecms 远程文件包含 （CVE-2015-4553）：已整理：两阶段利用配置覆盖实现远程文件写入（来源 3）；卡片 `cards/019_CVE-2015-4553_dedecms.md`。
- 020｜domoticz  sql注入（CVE-2019-10664）：已整理：floorplans/plan 的 idx SQL 注入读取配置项（来源 3）；卡片 `cards/020_CVE-2019-10664_domoticz.md`。
- 021｜Druid 任意文件读取 （CVE-2021-36749）：已整理：sampler 的 HTTP Firehose file URI 任意文件读取（来源 3）；卡片 `cards/021_CVE-2021-36749_druid.md`。
- 022｜drupal 远程代码执行 （CVE-2019-6339）：已整理：管理员头像 JPEG/PHAR 触发 phar:// 反序列化（来源 4）；卡片 `cards/022_CVE-2019-6339_drupal.md`。
- 023｜dubbo 代码执行 （CVE-2019-17564）：已整理：Dubbo HTTP Invoker 反序列化 RCE（来源 5）；卡片 `cards/023_CVE-2019-17564_dubbo.md`。
- 024｜dubbo 代码执行 （CVE-2020-1948）：已整理：Dubbo Provider Hessian2 反序列化链（来源 6）；卡片 `cards/024_CVE-2020-1948_dubbo.md`。
- 025｜elasticsearch 代码执行 (CVE-2015-1427)：已整理：Elasticsearch Groovy script_fields 沙盒绕过（来源 5）；卡片 `cards/025_CVE-2015-1427_elasticsearch.md`。
- 026｜empire 代码执行 （CVE-2018-19462）：已整理：后台 SQL INTO OUTFILE 写 PHP；镜像账号/绝对路径待实战确认（来源 3）；卡片 `cards/026_CVE-2018-19462_empire.md`。
- 027｜exim4 命令执行 （CVE-2020-28020）：已整理：公开RCE链分析；暂无可照抄完整exploit（来源 4）；卡片 `cards/027_CVE-2020-28020_exim4.md`。
- 028｜Fastjson 1.2.80 反序列化：已整理：Groovy两段链片段；镜像接口/依赖待补（来源 3）；卡片 `cards/028_fastjson_1.2.80.md`。
- 029｜forgerok openam 代码执行 （CVE-2021-35464）：已整理：JATO jato.pageSession + Click1 反序列化 RCE（来源 6）；卡片 `cards/029_CVE-2021-35464_openam.md`。
- 030｜Fuelcms 远程代码执行 （CVE-2018-16763）：已整理：/fuel/pages/select/ 的 GET filter PHP 表达式执行命令（来源 5）；卡片 `cards/030_CVE-2018-16763_fuelcms.md`。
- 031｜genixcms SQL注入 （CVE-2015-3933）：已整理：注册接口 SQL 注入；SQLMap 使用原始 POST 请求（来源 5）；卡片 `cards/031_CVE-2015-3933_genixcms.md`。
- 032｜Gerapy 远程代码执行 （CVE-2021-43857）：已整理：认证后利用已有项目触发 parse 命令注入（来源 4）；卡片 `cards/032_CVE-2021-43857_gerapy.md`。
- 033｜GhostScript 沙箱绕过（CVE-2018-16509）：已整理：图片上传 PostScript 载荷触发 Ghostscript %pipe% 命令执行（来源 5）；卡片 `cards/033_CVE-2018-16509_ghostscript.md`。
- 034｜glzjin/upload-labs：已整理：多关卡上传靶场；题库未指定Pass，整理Less-1至Less-10题解（来源 4）；卡片 `cards/034_glzjin-upload-labs.md`。
- 035｜goahead 变量注入 (CVE-2021-42342)：已整理：CGI 环境变量注入；满足条件时可借 LD_PRELOAD 加载共享库（来源 5）；卡片 `cards/035_CVE-2021-42342_goahead.md`。
- 036｜GoCD 任意文件读取漏洞 (CVE-2021-43287)：已整理：Business Continuity 未授权插件接口读取服务器文件（来源 5）；卡片 `cards/036_CVE-2021-43287_gocd.md`。
- 037｜grafana 目录遍历 （CVE-2021-43798）：已整理：/public/plugins/ 路径遍历读取文件；curl 保留原始路径（来源 3）；卡片 `cards/037_CVE-2021-43798_grafana.md`。
- 038｜Grafana未授权任意文件读取：已整理：公开PoC遍历插件静态资源路径读文件；与CVE-2021-43798相关但镜像对应未证实（来源 5）；卡片 `cards/038_grafana-read_arbitrary_file.md`。
- 039｜gxlcms 文件读取 （CVE-2018-14685）：已整理：Tpl新增路由参数转换路径读取配置文件和安装SQL（来源 2）；卡片 `cards/039_CVE-2018-14685_gxlcms.md`。
- 040｜h2database RCE（CVE-2022-23221）：已整理：H2 Console JDBC URL INIT触发器执行命令；区分不同PoC链路（来源 6）；卡片 `cards/040_CVE-2022-23221_h2database.md`。
- 041｜Hessian 反序列化：已整理：未找到镜像专属链路；附通用Hessian入口识别流程（来源 1）；卡片 `cards/041_hessian.md`。
- 042｜httpd 后缀解析：已整理：上传phpinfo.php.jpg绕过末尾后缀检查并由Apache PHP handler解析（来源 3）；卡片 `cards/042_httpd-apache_parsing_vulnerability.md`。
- 043｜httpd-ssi 命令执行：已整理：.shtml 使用SSI #exec执行命令；镜像上传入口未确认（来源 2）；卡片 `cards/043_httpd-ssi.md`。
- 044｜huawei HG532 远程命令执行 （CVE-2017-17215）：已整理：SOAP DeviceUpgrade / NewStatusURL 命令注入链（来源 5）；卡片 `cards/044_CVE-2017-17215_hg532.md`。
- 045｜imcat 远程代码执行 （CNVD-2020-32339）：已整理：准确编号资料未提供可执行步骤（来源 3）；卡片 `cards/045_CNVD-2020-32339_imcat.md`。
- 046｜jackson 代码执行 (CVE-2020-8840)：已整理：JndiConverter 多态反序列化至 JNDI/LDAP 远程类加载链（来源 5）；卡片 `cards/046_CVE-2020-8840_jackson.md`。
- 047｜java-rmi-codebase 代码执行：已整理：RMI codebase 自定义子类远程加载链（来源 4）；卡片 `cards/047_java-rmi-codebase.md`。
- 048｜java-rmi-registry-bind-deserialization 代码执行：已整理：RMI Registry bind + ysoserial CommonsCollections 链（来源 5）；卡片 `cards/048_java-rmi-registry-bind-deserialization.md`。
- 049｜java-rmi-registry-bind-deserialization-bypass 代码执行：已整理：UnicastRef 回连 JRMP Listener 两阶段 bypass 链（来源 4）；卡片 `cards/049_java-rmi-registry-bind-deserialization-bypass.md`。
- 050｜jboss 反序列化 （CVE-2017-7504）：已整理：JBossMQ HTTPServerILServlet 反序列化入口链（来源 4）；卡片 `cards/050_CVE-2017-7504_jboss.md`。
- 051｜jenkins 代码执行 （CVE-2017-1000353）：已整理：Jenkins HTTP CLI SignedObject 分块序列化利用链（来源 7）；卡片 `cards/051_CVE-2017-1000353_jenkins.md`。
- 052｜jetty 敏感信息泄露 （CVE-2021-28169）：已整理：ConcatServlet/WelcomeFilter 双重解码读取 WEB-INF（来源 7）；卡片 `cards/052_CVE-2021-28169_jetty.md`。
- 053｜jetty 敏感信息泄露 (CVE-2021-34429)：已整理：/%u002e/WEB-INF/web.xml 路径解析绕过链（来源 7）；卡片 `cards/053_CVE-2021-34429_jetty.md`。
- 054｜joomla 注册流程账号接管（题库误标CVE-2016-9839；实际CVE-2016-9838）：已整理：同一会话两阶段注册表单修改既有账号（来源 8）；卡片 `cards/054_CVE-2016-9838_joomla.md`。
- 055｜joomla 远程代码执行 （CVE-2021-23132）：已整理：com_media 路径绕过、配置替换到模板 RCE（来源 5）；卡片 `cards/055_CVE-2021-23132_joomla.md`。
- 056｜jquery 文件上传 （CVE-2018-9207）：已整理：myfile multipart 上传并访问 uploads 文件（来源 3）；卡片 `cards/056_CVE-2018-9207_jquery.md`。
- 057｜junams 文件上传 （CNVD-2020-24741）：已整理：add_images.html 非图片校验绕过上传 PHP（来源 4）；卡片 `cards/057_CNVD-2020-24741_junams.md`。
- 058｜jupyter-notebook XSSI（题库误标命令执行；CVE-2019-9644）：已整理：官方资料确认是 XSSI，非命令执行（来源 3）；卡片 `cards/058_CVE-2019-9644_jupyter-notebook.md`。
- 059｜kindeditor 目录遍历 （CVE-2018-18950）：已整理：upload_json.php path 枚举附件目录（来源 3）；卡片 `cards/059_CVE-2018-18950_kindeditor.md`。
- 060｜kylin  命令注入 （CVE-2021-45456）：已整理：项目名清洗与诊断 Shell 调用不一致（来源 5）；卡片 `cards/060_CVE-2021-45456_kylin.md`。
- 061｜kylin 命令执行（CVE-2020-13925）：已整理：诊断下载接口 project 路径段命令注入（来源 3）；卡片 `cards/061_CVE-2020-13925_kylin.md`。
- 062｜log4j 代码执行 (CVE-2017-5645)：已整理：Log4j TCP/UDP SocketServer 反序列化代码执行（来源 3）；卡片 `cards/062_CVE-2017-5645_log4j.md`。
- 063｜Metabase geojson任意文件读取漏洞 （CVE-2021-41277）：已整理：Metabase GeoJSON 本地文件读取（来源 4）；卡片 `cards/063_CVE-2021-41277_metabase.md`。
- 064｜MinIO SSRF （CVE-2021-21287）：已整理：MinIO Browser API SSRF 与 Docker API build 链路（来源 4）；卡片 `cards/064_CVE-2021-21287_minio.md`。
- 065｜mogodb 代码执行 （CVE-2013-1892）：已整理：MongoDB nativeHelper.apply 代码执行（来源 4）；卡片 `cards/065_CVE-2013-1892_mongodb.md`。
- 066｜msvod SQL注入 （CVE-2018-14418）：已整理：MSVOD v10 extractvalue() SQL 注入（来源 3）；卡片 `cards/066_CVE-2018-14418_msvod.md`。
- 067｜nagios 代码执行 (CVE-2016-9565)：已整理：Nagios RSS/MagpieRSS curl 参数注入 RCE（来源 3）；卡片 `cards/067_CVE-2016-9565_nagios.md`。
- 068｜nagiosxi SQL注入 （CVE-2018-10735）：已整理：Nagios XI commandline.php cname UNION SQL 注入（来源 5）；卡片 `cards/068_CVE-2018-10735_nagiosxi.md`。
- 069｜nagiosxi SQL注入 （CVE-2018-10737）：已整理：Nagios XI logbook.php txtSearch 错误型 SQL 注入（来源 4）；卡片 `cards/069_CVE-2018-10737_nagiosxi.md`。
- 070｜Nexus Repository Manager3 EL注入（CVE-2018-16621）：已整理：Nexus coreui_User.update 角色字段 EL 注入算术验证（来源 4）；卡片 `cards/070_CVE-2018-16621_nexus.md`。
- 071｜nexus 命令执行 （CVE-2020-10204）：已整理：Nexus coreui_User.update EL 过滤绕过至命令执行（来源 4）；卡片 `cards/071_CVE-2020-10204_nexus.md`。
- 072｜nexus 权限绕过 (CVE-2020-11444)：已整理：Nexus coreui_User.changePassword 权限绕过重置管理员密码（来源 2）；卡片 `cards/072_CVE-2020-11444_nexus.md`。
- 073｜nexus 远程命令执行 （CVE-2019-5475）：已整理：Nexus 2 Yum capability createrepoPath 命令注入（来源 5）；卡片 `cards/073_CVE-2019-5475_nexus.md`。
- 074｜nginx：信息待补：题库仅给 nginx:latest 与端口80，无漏洞编号/应用路径/利用资料（来源 0）；卡片暂缓（题库未给具体漏洞/路由）。
- 075｜Nginx 权限提升 （CVE-2016-1247）：已整理：Nginx Debian/Ubuntu logrotate 本地提权 PoC 链（来源 4）；卡片 `cards/075_CVE-2016-1247_nginx.md`。
- 076｜nginx 信息泄露 （CVE-2017-7529）：已整理：Nginx 缓存资源 Range 整数溢出泄露缓存文件头（来源 5）；卡片 `cards/076_CVE-2017-7529_nginx.md`。

## 本轮新增/核对记录（2026-09-28）

### 第073题｜Nexus Repository Manager 2 CVE-2019-5475

- 完成 Yum capability 的 `createrepoPath` Bash 命令注入步骤；标清管理员会话、动态 capability ID、回连地址和后续 CVE-2019-15588 的区分。
- 核对 GitHub PoC、技术复现、NVD 与 Sonatype 官方公告；修正 Sonatype 公告链接，保留 NVD CPE 和厂商修复版本记录的差异。来源 5 个；未实测、未写 Flag。

### 第074题｜nginx（待补场景）

- 题库只给 `nginx:latest` 与端口80，没有漏洞编号、应用路由或利用资料；不把普通 Nginx 服务臆写成漏洞链。等待补充真实题目漏洞点后再出卡片。

### 第075题｜Nginx CVE-2016-1247

- 完成 Debian/Ubuntu Nginx logrotate 本地提权卡片：限定已有 `www-data` shell 的前提，整理原始 `nginxed-root.sh` PoC、logrotate/USR1 触发与 root EUID 成功信号；补充发行版包版本边界和特有依赖/路径排坑。
- 来源 4 个：CVE 发现者技术公告、原始 PoC、Debian Security Tracker、Ubuntu USN-3114-1。未实测、未写 Flag。

### 第076题｜Nginx CVE-2017-7529

- 完成代理缓存资源的特制 Range 请求链，步骤写明缓存资源、`Content-Length` 与数值构造；明确需要启用 proxy cache，并将效果限定为缓存文件头信息泄露，不扩写成任意文件读取。
- 来源 5 个：技术复现、GitHub PoC、360CERT、Nginx 官方安全公告、NVD。未实测、未写 Flag。
- 用户此前给出的博客园链接核对为 Tomcat CVE-2017-12615，不作为第076题来源。

### 第077题｜Node.js CVE-2017-14849

- 整理 Node.js 8.5.0 与 Express/Send 静态目录穿越链路，保留 `/static` 挂载前缀及 `curl --path-as-is` 关键点。
- 来源 5 个：Node.js 官方公告、腾讯安全分析、博客园复现、Vulhub README、ProjectDiscovery Nuclei 模板。未实测、未写 Flag。

### 第078题｜node-serialize CVE-2017-5941

- 整理 `unserialize()` 接收不可信数据后触发 IIFE 的公开复现链，附 Base64 Cookie 请求示例和服务端日志成功信号；示例入口按来源标注，不冒充题目已确认接口。
- 来源 3 个：专业技术复现、GitHub 官方漏洞公告、上游 PoC/Issue。未实测、未写 Flag。

## 工作约定

- 卡片只总结直接相关技术复现、PoC 与官方资料；不保存原文、不做靶场实测、不写 Flag。
- 每题步骤与特有排坑标注来源编号；同一时间并行不超过两题；主线程负责同步索引、进度和工作记录。
