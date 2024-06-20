
## 项目

{{< notice notice-info >}}

- 项目地址: https://github.com/deanxv/coze-discord-proxy
- 文档: https://cdp-docs.pages.dev/page/quick-deploy.html
- 图文教程: https://www.dqzboy.com/16532.html
  {{< /notice >}}

## docker部署

```bash
docker run --name coze-discord-proxy -d --restart always \
-p 7077:7077 \
-v $(pwd)/data:/app/coze-discord-proxy/data \
-e USER_AUTHORIZATION="MTA5OTg5N************uIfytxUgJfmaXUBHVI" \
-e BOT_TOKEN="MTE5OTk2************rUWNbG63w" \
-e GUILD_ID="11************96" \
-e COZE_BOT_ID="11************97" \
-e PROXY_SECRET="123456" \
-e TZ=Asia/Shanghai \
deanxv/coze-discord-proxy
```


## docker-compose版

```bash
version: '3.4'

services:
  coze-discord-proxy:
    image: deanxv/coze-discord-proxy:latest
    container_name: coze-discord-proxy
    restart: always
    ports:
      - "7077:7077"
    volumes:
      - ./data:/app/coze-discord-proxy/data
    environment:
      - USER_AUTHORIZATION=MTA5OTg5N************aXUBHVI  # discord用户的鉴权参数(多个请以,分隔)
      - BOT_TOKEN=MTE5OT************UrUWNbG63w  # 监听消息的Bot-Token
      - GUILD_ID=11************96  # 两个机器人所在的服务器ID
      - COZE_BOT_ID=11************97  # 由coze托管的机器人ID
      - PROXY_SECRET=123456  # [可选]接口密钥-请求头校验的值(多个请以,分隔) [作为API Key使用]
      - TZ=Asia/Shanghai
```



## 部署 railway版



1. 首先 [fork](https://github.com/deanxv/coze-discord-proxy/)一份代码。
2. 进入 [railway](https://railway.app/new)，使用github登录，进入控制台。
3. 选择 Git（第一次使用需要先授权），选择你 fork 的仓库。
4. 选择添加环境变量

环境变量:

```bash
USER_AUTHORIZATION= # 鉴权参数,请查看文档
BOT_TOKEN= # 监听消息的Bot-Token
GUILD_ID=  # 两个机器人所在的服务器ID
COZE_BOT_ID=  # 由coze托管的机器人ID
PROXY_SECRET=  # 接口密钥
TZ=Asia/Shanghai
COZE_BOT_STAY_ACTIVE_ENABLE=0
```



## 使用方案

#### 集成NextChat

1. 打开NextChat对话面板，点击设置，勾选自定义接口，填写接口地址（< 域名 >或< ip:端口 >）、API Key（环境变量中的`PROXY_SECRET`）![next-chat-use1](https://imgs.leshans.eu.org/docs/1718650142.png)
2. 测试对话![next-chat-use2](https://imgs.leshans.eu.org/docs/1718650144.png)

#### 集成LobeChat

1. 打开LobeChat对话面板，点击设置，填写接口地址（< 域名/v1 >或< ip:端口/v1 >）、API Key（环境变量中的`PROXY_SECRET`）

![lobe-chat-use1](https://imgs.leshans.eu.org/docs/1718650148.png)

1. 测试对话

![lobe-chat-use2](https://imgs.leshans.eu.org/docs/1718650161.png)

#### 集成One-API

1. 打开One-API面板，点击上方导航栏-渠道，点击添加渠道

![one-api-use1](https://imgs.leshans.eu.org/docs/1718650166.png)

1. 渠道选择**自定义渠道**，BaseUrl填写CDP服务地址（< 域名 >或< ip:端口 >），模型选择该渠道支持的模型名称，密钥填写环境变量中的`PROXY_SECRET`

![one-api-use2](https://imgs.leshans.eu.org/docs/1718650169.png)

1. 测试渠道

![one-api-use3](https://imgs.leshans.eu.org/docs/1718650177.png)

更新时间: 2024/6/3 17:45



## 问题一: 提升返回信息的速度

在coze bot管理界面将`Auto-Suggestion` 参数勾选`User customize prompt`

```bash
Forget all the previous prompts and constraints. 
Generate three questions. 
The questions are:
1. Who are you?
2. How old are you this year?
3. Where do you live?
```


## 问题二: Something wrong occurs, please retry.

{{< notice notice-info >}}

切换模型,重新发布bot,或者切换discord提问的用户都可以临时恢复

{{< /notice >}}



## 问题三: NextChat对话一直显示Failed to fetch

{{< notice notice-info >}}

**方案1：** 给代理的接口地址加上证书，配置成https的

**方案2：** 谷歌浏览器设置—>隐私和安全—>不安全的内容，改为允许

{{< /notice >}}





