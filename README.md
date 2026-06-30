# WebShopX Cloudflare Relay

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/Cc-Cece/webshopx-cloudflare-relay)

## English

WebShopX Cloudflare Relay keeps the WebShopX plugin as the business backend. Cloudflare Workers provide the public HTTPS entry, static assets, setup page, and RPC relay.

The Minecraft server does **not** need a public IP address and does **not** need any inbound port opened. It only needs outbound access to Cloudflare over HTTPS / WebSocket Secure, which normally means outbound TCP `443`.

This relay does not replace the WebShopX plugin. The Minecraft server must run WebShopX and connect outbound to Cloudflare.

Panel-hosted servers are usually supported. If your hosting panel allows the Minecraft server process to access external `https://` and `wss://` URLs, you normally do not need to ask the host to open extra ports.

### Quick Start

1. Click **Deploy to Cloudflare**.
2. Open `/setup` after deployment.
3. Generate the plugin config.
4. Paste it into `plugins/WebShopX/config.yml`.
5. Restart or reload WebShopX.
6. Return to `/setup` and confirm that the plugin is connected.

### Local Development

```bash
npm install
npm run dev
npm run typecheck
```

### Configuration Snippet

`/setup` generates a snippet like this:

```yaml
deployment:
  mode: cloudflare-relay

cloudflare-relay:
  enabled: true
  endpoint: "https://webshopx-relay.example.workers.dev"
  server-id: "main"
  connector-token: "wsxcr_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  websocket-path: "/connector/ws"
  heartbeat-seconds: 30
  reconnect-min-seconds: 3
  reconnect-max-seconds: 60
  rpc-timeout-seconds: 10
```

### Relay Routes

- `GET /health`
- `GET /setup`
- `POST /api/setup/init`
- `POST /api/setup/rotate-token`
- `GET /connector/ws?server_id=main`
- `GET /api/relay/status`
- `POST /api/relay/test`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `POST /api/auth/logout`
- `GET /api/products`
- `POST /api/orders`
- `GET /api/orders/list`
- `POST /api/admin/auth/login`
- `GET /api/admin/auth/me`
- `GET /api/admin/relay/status`
- `GET /api/admin/products/list`
- `GET /api/admin/orders/list`

Cloudflare Free can be enough to start, but it is not unlimited. Avoid high-frequency admin polling and unnecessary dynamic requests.

## 中文

WebShopX Cloudflare Relay 会继续让 WebShopX 插件作为业务后端运行。Cloudflare Workers 负责公网 HTTPS 入口、静态资源、初始化页面和 RPC 中转。

Minecraft 服务器**不需要公网 IP**，也**不需要开放任何入站端口**。它只需要能主动出站连接 Cloudflare 的 HTTPS / WebSocket Secure，通常就是允许出站 TCP `443`。

这个 Relay 不会替代 WebShopX 插件。Minecraft 服务器仍然必须安装并运行 WebShopX，由插件主动连接 Cloudflare。

面板服通常也支持这个方案。只要面板允许 Minecraft 服务器进程访问外部 `https://` 和 `wss://` 地址，一般就不需要向面板商申请开放额外端口。

### 快速开始

1. 点击 **Deploy to Cloudflare**。
2. 部署完成后打开 `/setup`。
3. 生成插件配置片段。
4. 将配置片段粘贴到 `plugins/WebShopX/config.yml`。
5. 重启或 reload WebShopX。
6. 回到 `/setup`，确认插件已连接。

### 本地开发

```bash
npm install
npm run dev
npm run typecheck
```

### 配置片段

`/setup` 会生成类似下面的配置：

```yaml
deployment:
  mode: cloudflare-relay

cloudflare-relay:
  enabled: true
  endpoint: "https://webshopx-relay.example.workers.dev"
  server-id: "main"
  connector-token: "wsxcr_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  websocket-path: "/connector/ws"
  heartbeat-seconds: 30
  reconnect-min-seconds: 3
  reconnect-max-seconds: 60
  rpc-timeout-seconds: 10
```

### Relay 路由

- `GET /health`
- `GET /setup`
- `POST /api/setup/init`
- `POST /api/setup/rotate-token`
- `GET /connector/ws?server_id=main`
- `GET /api/relay/status`
- `POST /api/relay/test`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `POST /api/auth/logout`
- `GET /api/products`
- `POST /api/orders`
- `GET /api/orders/list`
- `POST /api/admin/auth/login`
- `GET /api/admin/auth/me`
- `GET /api/admin/relay/status`
- `GET /api/admin/products/list`
- `GET /api/admin/orders/list`

Cloudflare Free 可以用于起步，但不是无限额度。请避免高频后台轮询和不必要的动态请求。
