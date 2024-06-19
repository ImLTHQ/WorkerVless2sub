# 优选订阅生成器 WorkerVless2sub

### 这个是一个通过 Cloudflare Workers 搭建，自动生成优选线路 VLESS 节点订阅内容生成器

# Pages 部署方法

### 1. 部署 Cloudflare Pages：
   - 在 Github 上先 Fork 本项目，并点上 Star !!!
   - 在 Cloudflare Pages 控制台中选择 `连接到 Git`后，选中 `WorkerVless2sub`项目后点击 `开始设置`。
     
### 2. 设置变量：

  例如您的pages项目域名为：`sub.fuck.cloudns.biz`；
   - 添加 `TOKEN` 变量，默认值为: `auto` ，订阅器默认订阅地址即 `/auto` ，例如 `https://sub.fuck.cloudns.biz/auto`
   - 添加 `HOST` 变量，例如 `edgetunnel-2z2.pages.dev`；
   - 添加 `UUID` 变量，例如 `30e9c5c8-ed28-4cd9-b008-dc67277f8b02`；
   - 添加 `PATH` 变量，例如 `/?ed=2560`；
   - 添加 `PS` 变量，例如 `-[edgetunnel-2z2.pages.dev]`

   ```

<details>
<summary><code><strong>「 我不是小白！我有IP库！我知道IPtest是什么！我也有csv测速文件！ 」</strong></code></summary>

   - 添加变量 `ADDCSV` 为 **iptest测速结果csv文件地址** 的 URL。例如：
   ```js
   https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressescsv.csv
   ```
   - 添加变量 `DLS` ，意为`ADDCSV`满足最低速度的要求，不满足改数值以上的IP将不会添加至优选订阅内容。注意：不考虑单位，只看数值，请按照您的测速结果而定。例如：
   ```js
   8
   ```

 </details>

# 订阅生成器 使用方法

  例如您的workers项目域名为：`sub.cmliussss.workers.dev`；
  
### 1. 快速订阅

   - 添加 `TOKEN` 变量，快速订阅访问入口，默认值为: `auto` ，获取订阅器默认节点订阅地址即 `/auto` ，例如：
     ```url
     https://sub.cmliussss.workers.dev/auto
     ```
     
### 2. 自定义订阅 

   - **自定义订阅格式** `https://[你的Workers域名]/sub?host=[你的Vless域名]&uuid=[你的UUID]&path=[你的ws路径]`
   - **host**：您的 VLESS 伪装域名，例如 `edgetunnel-2z2.pages.dev`；
   - **uuid**：您的 VLESS 客户端 UUID，例如 `30e9c5c8-ed28-4cd9-b008-dc67277f8b02`；
   - **path**（可选）：您的 VLESS 的 WS 路径（没有可留空不填），例如 `/?ed=2048`。
   - 自定义订阅地址如下：
     ```url
     https://sub.cmliussss.workers.dev/sub?host=edgetunnel-2z2.pages.dev&uuid=30e9c5c8-ed28-4cd9-b008-dc67277f8b02&path=/?ed=2048
     ```
   - 注意路径必须包含 "/sub"。

### 3. 指定 clash、singbox 配置文件

   - 添加 `format=clash` 键值，获取 clash 订阅配置，例如：
     ```url
     https://sub.cmliussss.workers.dev/auto?format=clash
     https://sub.cmliussss.workers.dev/sub?format=clash&host=edgetunnel-2z2.pages.dev&uuid=30e9c5c8-ed28-4cd9-b008-dc67277f8b02&path=/?ed=2048
     ```
     
   - 添加 `format=singbox` 键值，获取 singbox 订阅配置，例如：
     ```url
     https://sub.cmliussss.workers.dev/auto?format=singbox
     https://sub.cmliussss.workers.dev/sub?format=singbox&host=edgetunnel-2z2.pages.dev&uuid=30e9c5c8-ed28-4cd9-b008-dc67277f8b02&path=/?ed=2048
     ```
     
### 变量说明
| 变量名 | 示例 | 备注 | 
|--------|---------|-----|
| TOKEN | auto | 快速订阅内置节点的订阅路径地址 /auto (支持多元素, 元素之间使用`,`作间隔)| 
| HOST | edgetunnel-2z2.pages.dev | 快速订阅内置节点的伪装域名 | 
| UUID | b7a392e2-4ef0-4496-90bc-1c37bb234904 | 快速订阅内置节点的UUID | 
| PATH | /?ed=2560 | 快速订阅内置节点的路径信息 | 
| ADD | icook.tw:2053#官方优选域名 | 对应`addresses`字段 (支持多元素, 元素之间使用`,`作间隔) | 
| ADDAPI | [https://raw.github.../addressesapi.txt](https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesapi.txt) | 对应`addressesapi`字段 (支持多元素, 元素之间使用`,`作间隔) | 
| ADDNOTLS | icook.hk:8080#官方优选域名 | 对应`addressesnotls`字段 (支持多元素, 元素之间使用`,`作间隔) | 
| ADDNOTLSAPI | [https://raw.github.../addressesapi.txt](https://raw.githubusercontent.com/cmliu/CFcdnVmess2sub/main/addressesapi.txt) | 对应`addressesnotlsapi`字段 (支持多元素, 元素之间使用`,`作间隔) | 
| ADDCSV | [https://raw.github.../addressescsv.csv](https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressescsv.csv) | 对应`addressescsv`字段 (支持多元素, 元素之间使用`,`作间隔) | 
| DLS | 8 |`addressescsv`测速结果满足速度下限 | 
| NOTLS | false | 改为`true`, 将不做域名判断 始终返回noTLS节点 | 
| TGTOKEN | 6894123456:XXXXXXXXXX0qExVsBPUhHDAbXXXXXqWXgBA | 发送TG通知的机器人token | 
| TGID | 6946912345 | 接收TG通知的账户数字ID | 
| SUBAPI | api.v1.mk | clash、singbox等 订阅转换后端 | 
| SUBCONFIG | [https://raw.github.../ACL4SSR_Online_Full_MultiMode.ini](https://raw.githubusercontent.com/cmliu/ACL4SSR/main/Clash/config/ACL4SSR_Online_Full_MultiMode.ini) | clash、singbox等 订阅转换配置文件 | 
| SUBNAME | WorkerVless2sub | 订阅生成器名称 | 
| PS | 【请勿测速】 | 节点名备注消息 | 
| PROXYIP | proxyip.fxxk.dedyn.io | 默认分配的ProxyIP, 多ProxyIP将随机分配(支持多元素, 元素之间使用`,`作间隔) | 
| CMPROXYIPS | proxyip.aliyun.fxxk.dedyn.io:HK | 识别HK后分配对应的ProxyIP(支持多元素, 元素之间使用`,`作间隔) | 

## Star 星星走起
[![Stargazers over time](https://starchart.cc/CF-Pageso/WorkerVless2sub.svg?variant=dark)](https://starchart.cc/CF-Pageso/WorkerVless2sub)

# 感谢
我自己的脑洞，[SAKURA-YUMI](https://github.com/SAKURA-YUMI)，[EzSync](https://github.com/EzSync)、[ACL4SSR](https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash/config)、[肥羊](https://github.com/youshandefeiyang/sub-web-modify)


