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

## 本轮新增/核对记录（2026-09-29｜第079–100题）

按题库顺序整理 22 道待整理题。未实测、未写 Flag、不下载整篇原文。编号/题名与公开资料不一致时按 CVE 校正，不编造利用链。

### 第079题｜Nuxeo CVE-2018-16341

- 完成 `login.jsp/` 前缀绕过 + Facelet 不存在即解析的 SSTI 链；算术探测与 Runtime EL 均要求百分号编码。
- 来源 4 个：发现者分析、mpgn PoC、Nuxeo NXP-25746 提交、NVD。

### 第080题｜O2OA CVE-2022-22916

- 完成后台 `Authorization` + `/x_program_center/jaxrs/invoke` 创建/execute 两步。默认口令以 NVD 收录 PoC 的 `xadmin/o2` 为主，并注明较新文档的 `o2oa@2022`。
- 来源 4 个。

### 第081题｜OFBiz CVE-2021-30128

- 完成 SOAPService + ysoserial CommonsBeanutils1 三处类名 `<java.短名` 改写；与 26295/9496 区分。
- 来源 4 个：分析、阿里云致谢文、EXP、Apache oss-security。

### 第082题｜OKLite CVE-2019-16131

- 完成后台模块导入 ZIP 解压到 `data/cache/`；与插件子目录链分开。
- 来源 4 个。账号题库未给，不编造。

### 第083题｜Online Book Store CVE-2020-24115

- 题库标「代码执行」；NVD 为硬编码凭据。卡片只整理 SQL/默认 Admin Login，不把 `edit_book.php` 上传写成这条 CVE。
- 来源 3 个。

### 第084题｜OpenSMTPD CVE-2020-7247

- 完成 Qualys MAIL FROM `;read;sh` + DATA 注释滑梯链；标明远程需 “uncommented” 监听。
- 来源 3 个。

### 第085题｜PbootCMS CVE-2018-16356

- 采用 Vulfocus 同题题解：启用 API 后打 `api.php/List/index?order=` + `updatexml`/`md5(1954)`。不套用后续 3.x 搜索框注入。
- 来源 4 个。

### 第086题｜phpCollab CVE-2017-6089

- 三处未授权删除接口；与 login.php 老洞区分。
- 来源 3 个。

### 第087题｜PHPOK CVE-2018-12491

- 只整理 4.9.032 的 `framework/admin/modulec_control.php` → `import_f`（含 PHP 的 ZIP 解到 `data/cache/`）。
- 4.8.338 附件分类链标为 CVE-2018-8944；4.9.015 ZIP 解压链标为 CVE-2018-19562；两者不计本题来源、不作 12491 依据。
- 来源 2 个。

### 第088题｜Piwigo CVE-2022-26266

- 后台 `pwg.users.getList` 的 `order`；与 CVE-2022-32297 二次注入区分。
- 来源 3 个（NVD 引用的 JCCD 页检索时 404，步骤以分析文为准）。

### 第089题｜PrimeFaces CVE-2017-1000486

- `pfdrid` + 默认 secret `primefaces`；口令非默认时走 Padding Oracle。
- 来源 3 个。

### 第090题｜python-pickle（无 CVE）

- 未找到 Vulfocus 本题镜像专属题解。附 Vulhub Flask `user` Cookie pickle 链，并标明入口未确认。来源 2 个。

### 第091题｜Rails CVE-2018-3760

- Sprockets 报错取允许目录 + `%252e%252e/`。来源 3 个。

### 第092题｜Ruby CVE-2017-17405

- Net::FTP `Kernel#open` + `|` 文件名；公开 `/download` 路由未由本题镜像确认。来源 3 个。

### 第093题｜Salt CVE-2021-25281

- 本题是 `wheel_async` 未授权；完整 RCE 需拼 25282/25283。来源 4 个。

### 第094题｜ShardingSphere CVE-2020-1947

- `/api/schema` 的 `dataSourceConfiguration` SnakeYAML + JdbcRowSetImpl。来源 4 个。

### 第095题｜ShenYu CVE-2022-23944

- 只整理 `GET /plugin` 未授权，与第004题 CVE-2021-37580 区分。来源 4 个。

### 第096题｜Shiro CVE-2020-11989

- 分号 context-path 与 `%25%32%66` 双重编码两条。来源 3 个。

### 第097题｜Shiro CVE-2022-32532

- `RegExPatternMatcher` + `%0a`/`%0d`；含 Vulfocus 镜像复现。来源 4 个。

### 第098题｜Solr CVE-2019-12409

- 题库标「上传代码」；实际为 Linux 默认 JMX RMI 18983。来源 4 个。

### 第099题｜Spark CVE-2020-9480

- 官方是 standalone + `spark.authenticate` 的 RPC 绕过；REST `/v1/submissions/create` 仅作公开辅助并加限制说明。来源 4 个。

### 第100题｜Spring Data MongoDB SpEL

- 题库/镜像编号 CVE-2022-22890，官方同一问题为 CVE-2022-22980。按 `@Query` SpEL + `name=` 复现整理。来源 3 个。

## PR #1 评审修正（079–100）

- 087：收敛到 CVE-2018-12491 的 4.9.032 `import_f`；8944 / 19562 只在来源清单标号，不计来源。
- 089：受影响区间改为 4.0–4.0.24、5.0–5.2.20、5.3–5.3.7；5.2.21 / 5.3.8 / 6.0 为已修复。
- 081：ysoserial 重定向注明需 PowerShell 7.4+ 或二进制安全写法。
- 092：`curl.exe` URL 改为单引号，避免 PowerShell 展开 `${IFS}`。

## 本轮新增/核对记录（2026-09-29｜第101–125题）

第079–100题已由其他分支（PR #1 / `cursor/cards-079-100-445e`）完成并合入，本轮**不重做**；下一批从第101题起。

### 第101–125题｜批量整理

- 按题库顺序新建 25 张卡片与对应 `sources/<目录>/_meta.md`；统一回写 `index.csv`、`batches/progress.csv`。未实测、未写 Flag。
- **101** Spring MVC RFD（CVE-2020-5398）：`filename` 引号注入；来源 4。
- **102** S2-062（CVE-2021-31805）：multipart `id` BeanMap；来源 4。
- **103** S2-012（CVE-2013-1965）：redirect `${name}`；来源 4。
- **104** S2-013（CVE-2013-1966）：`includeParams` / `link.action?a=`；来源 4。
- **105** S2-015（CVE-2013-2135，公告同时登记 CVE-2013-2134）：通配符 Action 名 OGNL；来源 4。
- **106** S2-016（CVE-2013-2251）：`redirect:` 前缀；来源 4。
- **107** S2-001：NVD CVE-2007-4556 为 XWork/Struts altSyntax 递归 OGNL，**不采用**后来误绑到 Python tarfile 的同编号链；来源 4。
- **108** S2-005（CVE-2010-1870）：参数名 `\u0023`；来源 4。
- **109** S2-007：Apache 公告当时 CVE 为 “-”，NVD 登记 **CVE-2012-0838**，与题库一致；来源 4。
- **110** Subrion（CVE-2017-11444）：`/search/members.json` GET **键名**注入；来源 3。
- **111** Supervisord（CVE-2017-11610）：`POST /RPC2` + `linecache.os.system`；来源 4。
- **112** Tapestry（CVE-2019-0195）：classpath `AppModule.class`，不是 `/etc/passwd`，不混用 CVE-2021-27850；来源 3。
- **113** ThinkPHP lang：无 CVE；`lang` LFI + pearcmd `config-create`；镜像 `vulfocus/thinkphp:6.0.12`；来源 4。
- **114** Tomcat（CVE-2020-9484）：FileStore，`JSESSIONID` 不要带 `.session` 后缀；来源 4。
- **115** Typesetter（CVE-2020-25790）：后台 ZIP 解压绕过；来源 4。
- **116** UCMS（CVE-2020-25483）：后台 `sadmin_fileedit` 写 PHP；来源 3。
- **117** `vulfocus/717-3`：Hub 实际为 `717_3`、描述为空；**待补链路**，不套 Twonky/phpstudy；来源 1。
- **118** 题名 `apache-40438`：校正为 **CVE-2021-40438**；Hub 镜像 `httpd_cve-2021-40438`；`unix:` 超长路径 SSRF；来源 4。
- **119** CVE-2018-11759：`/jkstatus;` 绕过；来源 4。
- **120** CVE-2021-41773：仅 2.4.49、`.%2e`、必须 `--path-as-is`，不与第001题 `.%%32%65` 混用；来源 4。
- **121** `armel22`：ARM EABI 环境识别（端口 5535），区别 armhf/arm64；来源 5。
- **122** bWAPP：教学靶场，`bee`/`bug`、portal/low；来源 4。
- **123** CuppaCMS（CVE-2020-26048）：认证上传 jpg 再改 rename 的 `to:`；不采用后续未授权上传 issue；来源 3。
- **124** Discuz!ML（CVE-2019-13956）：`{cookiepre}language=en'.phpinfo().';`；来源 3。
- **125** wooyun-2010-080723：Cookie 覆盖 `GLOBALS[_DCACHE][smilies]` + `preg_replace /e`；来源 3。

## 本轮新增/核对记录（2026-09-29｜第126–150题）

按题库顺序整理 25 道待整理题（跳过 079–125）。未实测、未写 Flag、不下载整篇原文。编号/题名与公开资料不一致时按 CVE 校正，不编造利用链。

### 第126题｜Drupal CVE-2018-7602

- 完成已认证 Drupalgeddon3：`destination` 二次编码 `%2523` + `_triggering_element_name=form_id` 缓存表单，再 `file/ajax` 触发 `#post_render`。与未登录 7600 `user/register` 区分。
- 来源 5 个。

### 第127题｜GreenCMS CVE-2018-12604

- 完成未授权 `Data/Log/YY_MM_DD.log` 日志读取；标明不是 RCE、也不是 CVE-2018-19376。
- 来源 4 个。

### 第128题｜Gxlcms CVE-2018-14685

- 与第039题同一 CVE：`s=Admin-Tpl-ADD-id-` + `|`/`*` 占位读 Runtime 配置/安装 SQL。为本镜像另建卡片。
- 来源 2 个。

### 第129题｜Hackademic（无 CVE）

- 按 OWASP 10 关练习整理，不编单一 RCE。未找到 Vulfocus 专属 WP；与 VulnHub RTB1 区分。
- 来源 9 个。

### 第130题｜Hadoop（无 CVE）

- 题库无端口。Hub compose 与平台题解确认 YARN RM REST `8088`：new-application 再提交 `am-container-spec.commands`。
- 来源 5 个。

### 第131题｜JSPWiki CVE-2021-44140

- 官方定性为 Logout `JSPWikiUID` 任意文件删除，不是上传/RCE。镜像 workDir 待补，不套公开 Docker 路径。
- 来源 6 个。

### 第132题｜Juice Shop（无 CVE）

- 先找隐藏 Score Board，再按本实例清单做登录注入 / 后台 / DOM XSS。不编单一 RCE。
- 来源 5 个。

### 第133题｜Log4j CVE-2021-4104

- 只整理 Log4j **1.2** `JMSAppender` + 写配置；禁止抄 Log4Shell `${jndi:...}`。本题镜像 HTTP 入口待补。
- 来源 5 个。

### 第134题｜log4j2-rce-2021-12-09

- 题库无 CVE。按镜像日期与 Vulfocus 复现校正为 **CVE-2021-44228**；入口 `POST /hello`、`payload=`。与第133题 4104 区分。
- 来源 4 个。

### 第135题｜Monstra CVE-2020-13384

- 完成后台 Files Manager 认证上传。本题 Vulfocus 复现 `.php7` 不解析、改 `.phar`。
- 来源 6 个。

### 第136题｜Mutillidae（无 CVE）

- 多漏洞练习：Setup/降安全级别、登录用户名 SQLi、DNS Lookup 命令注入。未找到 Vulfocus 专属 WP。
- 来源 6 个。

### 第137题｜Nagios XI CVE-2018-8733

- 8733 只覆盖 `settings.php` 未授权改库；公开根权限还需 8734→加用户→8735/8736。与 067/068/069 入口区分。
- 来源 4 个。

### 第138题｜OFBiz CVE-2018-8033

- 官方是 `/webtools/control/httpService` 两段式 XXE，不是 XML-RPC；补丁 16.11.05。与 081 SOAP 反序列化区分。
- 来源 3 个。

### 第139题｜OpenTSDB

- 镜像名 `cev` 笔误，校正为 **CVE-2020-35476**。题库无端口；公开复现 4242、`yrange` 的 `system()`。
- 来源 3 个。

### 第140题｜php-ssrf（待补）

- Docker Hub 有镜像、无 overview。未找到本题入口/参数/协议，不编造 gopher/file 链。
- 来源 1 个。

### 第141题｜Rails CVE-2018-3760

- 与第091题同一 Sprockets `%252e%252e/` 链。为本镜像另建卡片。
- 来源 3 个。

### 第142题｜Rails CVE-2019-5418

- `Accept: ../../../../../../../../etc/passwd{{` 打 `/robots`；不要抄 PoC demo 的 `/chybeta`。
- 来源 4 个。

### 第143题｜Shiro CVE-2016-4437

- Shiro-550 默认密钥 `rememberMe` 反序列化。与 1957/11989/32532 路径绕过区分；ysoserial 重定向需二进制安全写法。
- 来源 4 个。

### 第144题｜Spring Security OAuth CVE-2016-4977

- `/oauth/authorize?response_type=${}`；题库无端口，公开复现 8080。必须认证且带齐 OAuth 参数。
- 来源 4 个。

### 第145题｜Spring Messaging CVE-2018-1270

- SockJS `/gs-guide-websocket` 的 STOMP `selector` SpEL；只 SUBSCRIBE 不够，必须再 `SEND /app/hello`。与 CVE-2018-1273 区分。
- 来源 5 个。

### 第146题｜Spring Cloud Config CVE-2020-5410

- HTTP `8888` 的 `..%252F` + `%23` 穿越；`9999` 未在该 CVE 复现中作为入口。与 5405 `(_)` 链区分。
- 来源 5 个。

### 第147题｜sqli-labs（无 CVE）

- 多关卡靶场；题库未指定 Less。整理 Less-1 至 Less-10 闭合/类型速查，先看页面编号再套。
- 来源 4 个。

### 第148题｜OpenSSH CVE-2020-15778

- 已认证客户端 scp 目的路径反引号，命令在远端 sshd 执行。题库未给账号；OpenSSH 9.0+ 需 `-O`。NVD DISPUTED。
- 来源 6 个。

### 第149题｜Struts2 CVE-2017-5638

- S2-045 `Content-Type` OGNL，头内仍须含 `multipart/form-data`。PowerShell 单引号避免 `%{` 当脚本块。
- 来源 4 个。

### 第150题｜ThinkPHP 5.0.24（待补）

- 5.0.24 是官方对 5.0.0–5.0.23 `Request::method` RCE 的修复版。不套 `invokefunction` / `_method=__construct`。公开 POP 反序列化需应用层 `unserialize()`，本题镜像 sink 未证实。
- 来源 6 个。

### 第223–232题｜本批整理（2026-09-29）

- 223 Shiro-721：题库无 CVE，对应 CVE-2019-12422；合法 rememberMe + Padding Oracle，非 550 默认密钥、非路径绕过。来源 6。
- 224 ShowDoc CNVD-2020-26585：`/index.php?s=/home/page/uploadImg`，`test.<>php`，版本 2.8.2/≤2.8.6。来源 6。
- 225 SkyWalking CVE-2020-9483：`POST /graphql` 的 `getLinearIntValues.metric.id`，不用 `queryLogs.metricName`。来源 5。
- 226 Spring CVE-2017-4971：Web Flow 确认页 `_` 参数名 SpEL，非 144 题 OAuth 4977。来源 5。
- 227 Spring CVE-2017-8046：PATCH `application/json-patch+json` 的 `path` SpEL。来源 5。
- 228 spring-boot-whitelabel-spel：无 CVE；路径 `/article?id=`，题库端口 9090。来源 5。
- 229 Struts2 CVE-2020-17530：S2-061 multipart `id`，非 S2-059。来源 5。
- 230 ThinkAdmin CVE-2020-25540：`api.Update/node` 与 `get/encode`。来源 5。
- 231 ThinkCMF CVE-2019-7580：后台 `alias` 写 `route.php`，不是 `a=fetch`。来源 6。
- 232 ThinkPHP 3.2.x：日志 + `value[_filename]`，不套 TP5 invokefunction / TP2 preg_replace `/e`。来源 6。

## 本轮新增/核对记录（2026-09-29｜第201–249题）

基于最新 `main`（已含 126–150）新建分支，整理 201–249。冻结 **202 / 219 / 233 / 238 / 248** 未返工。未实测、未写 Flag、不下载整篇原文。`index.csv` / `progress.csv` 只改本批行。

### 编号校正

- **207**：CVE-2018-7314 官方是 PrayerCenter `sessionid`，不是核心 `com_fields`（CVE-2017-8917）。
- **212**：CVE-2019-7238 是 Nexus `previewAssets` JEXL，不是 GitLab ExifTool。
- **213**：题库标「命令执行」；官方是 nginx `resolver` DNS off-by-one，不是 HTTP 命令注入。
- **214**：CVE-2021-26295 是 SOAP + RMI，不是 XML-RPC（215 / 9496），也不是 30128 / 8033。
- **216**：用户名枚举，不是 RCE。
- **217**：`render` locals 键名注入，不是 Marshal / `__proto__`。
- **220**：CNVD-2019-21763 是 4.x+ module/rogue replica，不是 crontab，不是 CVE-2015-4335。
- **221**：ZeroMQ ClearFuncs，不是 salt-api（093 / 222）。
- **223**：题库无 CVE，对应 **CVE-2019-12422** / SHIRO-721。
- **231**：后台 `alias` 写 `route.php`，不是 2.x `a=fetch`。
- **236**：`ws_utc` 上传，不是 wls-wsat / 14882。
- **237**：T3 StreamMessageImpl 走 7001，不是 5556 Node Manager。
- **239**：官方是已登录 CSRF→`/proc/run.cgi`，不是未授权 RCE（亦非 15107/15642/0824）。
- **247**：无 CVE；是 9.1.2 `block orderBy`，不是 16.5 登录框 CNVD-2022-42853。
- **249**：注入点是 `search`，不是 `path`。

### 待补

- **207**：镜像是否含 PrayerCenter 未证实。
- **213**：无公开 HTTP/命令执行链，不编造。
- **217**：本题镜像具体参数名（`ender`/`loc` 等）未找到。
- **231**：后台默认口令未由本题资料给出。
- **236**：本题镜像控制台口令待补。
- **239**：镜像是否 `setup.pl`（referrer 关闭）待补。
- **240**：Author 账号待补；完整 RCE 常需拼 8942。
- **241**：WP 用户名与 MTA 待补。
- **243**：Hub 镜像名与 HTTP 路由未找到；仅有官方 XML。
- **244**：题库端口 8008 在公开复现中未作为入口。

### 第201–222、234–249题｜要点

- **201** GetSimple 11231：XML 泄露 + Cookie 伪造 + theme-edit。来源 5。
- **203** Jackson 7525：TemplatesImpl；`/exploit` 仅 Vulhub 演示入口。来源 6。
- **204 / 205** JBoss：`/invoker/readonly` vs `/invoker/JMXInvokerServlet`。来源 4 / 5。
- **206** Joomla 7857：`list[select]`，`list[ordering]` 必须空。来源 5。
- **208 / 209** Laravel：`/.env` vs Ignition PHAR。来源 4 / 6。
- **210** libssh：paramiko `USERAUTH_SUCCESS`。来源 5。
- **211** Hystrix `proxy.stream?origin=`。来源 5。
- **215** OFBiz XML-RPC CommonsBeanutils1。来源 5。
- **218** 与第142题同 CVE-2019-5418，`/robots` + Accept。来源 4。
- **222** `/run` + `ssh_priv`，串 25592。来源 4。
- **234 / 235** DVWA / Pikachu 多漏洞练习，不编造单条 RCE。来源 5 / 5。
- **242 / 244** XStream 21351 JNDI vs 29505 JRMP（勿用官网错误 XML）。来源 4 / 4。
- **245 / 246** Zabbix trapper 10051；11800 用 IPv6 `ffff:::`，2824 用 `;cmd`。来源 4 / 4。

## 工作约定

- 卡片只总结直接相关技术复现、PoC 与官方资料；不保存原文、不做靶场实测、不写 Flag。
- 每题步骤与特有排坑标注来源编号；同一时间并行不超过两题；主线程负责同步索引、进度和工作记录。
