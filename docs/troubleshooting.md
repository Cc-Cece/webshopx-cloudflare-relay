# Troubleshooting / 故障排查

## English

Open `/setup` first. It reports whether the Worker, Durable Object, and plugin connection are healthy.

### Common Checks

- Plugin offline: verify `deployment.mode: cloudflare-relay`, endpoint, server id, and token.
- Token error: regenerate the token in `/setup` and paste the new snippet into `config.yml`.
- Wrong endpoint: use the exact workers.dev or custom domain shown on `/setup`.
- Network blocked: the Minecraft server does not need inbound ports, but it must be allowed to make outbound `https://` and `wss://` connections to Cloudflare, normally over TCP `443`.
- Panel-hosted server: ask the host whether plugin processes can access external HTTPS/WSS URLs. No public IP, reverse proxy, or inbound port forwarding is required for this relay.
- Durable Object missing: run `wrangler deploy` again and confirm that the migration succeeded.
- Old frontend assets: clear the browser cache or redeploy Static Assets.

The Worker only relays allowlisted RPC methods. It does not execute Minecraft commands or SQL.

## 中文

请先打开 `/setup`。这个页面会显示 Worker、Durable Object 和插件连接是否正常。

### 常见检查项

- 插件离线：检查 `deployment.mode: cloudflare-relay`、endpoint、server id 和 token。
- token 错误：在 `/setup` 重新生成 token，并把新的配置片段粘贴到 `config.yml`。
- endpoint 填错：使用 `/setup` 页面显示的准确 workers.dev 地址或自定义域名。
- 网络受阻：Minecraft 服务器不需要开放入站端口，但必须允许主动出站访问 Cloudflare 的 `https://` 和 `wss://`，通常是出站 TCP `443`。
- 面板服：询问面板商是否允许插件进程访问外部 HTTPS/WSS 地址。使用这个 relay 不需要公网 IP、反向代理或入站端口转发。
- Durable Object 缺失：重新运行 `wrangler deploy`，并确认 migration 已成功生效。
- 前端资源过旧：清理浏览器缓存，或重新部署 Static Assets。

Worker 只会中转白名单内的 RPC 方法，不会执行 Minecraft 命令，也不会执行 SQL。
