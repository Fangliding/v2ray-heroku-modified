# 写在前面
本项目导入自bclswl0827/v2ray-heroku

支持了ws 0-RTT(v2fly与xray通用)  设置方法 v2ray设置方法 max early data设置为2048 前置数据标头设置为2048 xray设置方法为在路径最后加上"?ed=2048"

当然导入过来还有一个重要原因是因为我fork的仓库被封了()

# V2Ray Heroku

//**若需部署 V2Ray VLESS，请转到 [vless](https://github.com/fangliding/v2ray-heroku-modified/tree/vless) 分支。**

## 概述

本专案用于在 Heroku 上部署 V2Ray WebSocket，在合理使用的程度下，本镜像不会因为大量占用资源而导致封号。

部署完成后，每次启动应用时，运行的 V2Ray 将始终为最新版本

## 部署

### 步骤

 1. Fork 本专案到自己的 GitHub 账户（用户名以 `example` 为例）
 2. 修改专案名称，注意不要包含 `v2ray` 和 `heroku` 两个关键字（修改后的专案名以 `demo` 为例）
 3. 修改 `README.md`，将 `fangliding/v2ray-heroku-modified` 替换为自己的内容（如 `example/demo`）

> [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/fangliding/v2ray-heroku-modified)

 4. 回到专案首页，点击上面的链接以部署 V2Ray

### 变量

对部署时需设定的变量名称做如下说明。

| 变量 | 默认值 | 说明 |
| :--- | :--- | :--- |
| `ID` | `ad806487-2d26-4636-98b6-ab85cc8521f7` | VMess 用户主 ID，用于身份验证，为 UUID 格式 |
| `WSPATH` | `/` | WebSocket 所使用的 HTTP 协议路径 |

## 导入

模板分享链接
```
vmess://eyJhZGQiOiIxLjAuMC4xIiwiYWlkIjoiMCIsImhvc3QiOiJ4eHgueHh4LndvcmtlcnMuZGV2IiwiaWQiOiJhZDgwNjQ4Ny0yZDI2LTQ2MzYtOThiNi1hYjg1Y2M4NTIxZjciLCJuZXQiOiJ3cyIsInBhdGgiOiIiLCJwb3J0IjoiNDQzIiwicHMiOiJoZXJva3UiLCJzY3kiOiJ6ZXJvIiwic25pIjoieHh4Lnh4eC53b3JrZXJzLmRldiIsInRscyI6InRscyIsInR5cGUiOiIiLCJ2IjoiMiJ9
```
请自行将所有xxx.xxx.workers.dev修改为自己的cloudflare worker地址 path和uuid均为默认值如果修改了请作出同样的修改并且可以根据上述方法设置ws 0-RTT
地址默认为1.0.0.1 可以替换为自己优选的ip

## 接入 CloudFlare

可以将应用接入 CloudFlare Worker，从而在一定程度上提升速度。
worker配置为

addEventListener(
"fetch",event => {
let url=new URL(event.request.url);
url.hostname="xx.xxxx.xx";//你的heroku域名
let request=new Request(url,event.request);
event. respondWith(
fetch(request)
)
}
)
 

## 注意

 1. **请勿滥用本专案，类似 Heroku 的免费服务少之又少，且用且珍惜**
 2. 若使用域名接入 CloudFlare，请考虑启用 TLS 1.3
 3. AWS 绝大部分 IPv4 地址已被 Twitter 屏蔽
 4. heroku的地址似乎已经被墙，推荐使用cloudflare worker进行中转
