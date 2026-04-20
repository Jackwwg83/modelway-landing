# Sub2API Admin 品牌替换指南

> **目标**：在不改 Sub2API 代码、不重新部署前端的前提下，把 api.modelway.dev 的 Sub2API 默认品牌全部替换成 **ModelWay**。
>
> **预计耗时**：10-15 分钟
>
> **前置条件**：你是 api.modelway.dev 的 admin，能登录 `/admin`。

---

## 替换清单（按优先级排序）

| # | 位置 | 动作 | 资产文件 | 耗时 |
|---|---|---|---|---|
| 1 | Settings · General · 站点 Logo | 上传 | `exports/logo-80.png` | 1 min |
| 2 | Settings · General · Favicon | 上传 | `exports/favicon-32.png` | 1 min |
| 3 | Settings · General · 站点名称 | 填 `ModelWay` | — | 30 s |
| 4 | Settings · General · 站点副标题 | 填 `Unified AI API gateway — Claude, GPT, Gemini` | — | 30 s |
| 5 | Settings · Email · 发件人 | 填 `noreply@modelway.dev` | — | 30 s |
| 6 | Settings · Homepage · home_content | 留空 或 填 `https://modelway.dev` | — | 1 min |
| 7 | Settings · Custom Pages · Privacy | 贴 HTML | `exports/privacy-en.html` / `privacy-zh.html` | 2 min |
| 8 | Settings · Custom Pages · Terms | 贴 HTML | `exports/terms-en.html` / `terms-zh.html` | 2 min |
| 9 | Settings · Footer · Privacy URL | 填 `/custom/privacy` | — | 30 s |
| 10 | Settings · Footer · Terms URL | 填 `/custom/terms` | — | 30 s |

---

## 详细步骤

### 1. 上传 Logo

**位置**：`https://api.modelway.dev/admin` → Settings → General → 站点 Logo

**要上传的文件**：
```
/Users/jackwu/modelway-landing/brand/exports/logo-80.png
```

**备用（如果 80×80 不清晰）**：
```
/Users/jackwu/modelway-landing/brand/exports/logo-256.png  # 更高清
```

**上传后检查**：
- [ ] 左上角 AppSidebar Logo 显示正确
- [ ] 登录页 Logo 显示正确
- [ ] 浏览器 tab 标题前的小图标（favicon，稍后替换）

---

### 2. 上传 Favicon

**位置**：Settings → General → Favicon（或直接放到 CDN `/favicon.ico`）

**要上传的文件**：
```
/Users/jackwu/modelway-landing/brand/exports/favicon-32.png
```

**如果 admin 有多尺寸上传**：
- 16×16 → `exports/favicon-16.png`
- 32×32 → `exports/favicon-32.png`（标准）
- 48×48 → `exports/favicon-48.png`
- 180×180 (Apple) → `exports/apple-touch-icon-180.png`

**如果只支持一个 .ico 文件**：
```
/Users/jackwu/modelway-landing/brand/exports/favicon.ico  # 16/32/48 多尺寸打包
```

**验证**：
- 刷新 api.modelway.dev（强刷 Cmd+Shift+R，favicon 有 30 天缓存）
- tab 标题前应该显示六边形 teal logo

---

### 3. 站点名称

**位置**：Settings → General → 站点名称

```
ModelWay
```

（用户反馈已经填了，可能还是 `Sub2API`，需要检查）

**自动传导位置**（改完立即生效，无需重启）：
- 浏览器 tab 标题
- AppSidebar 顶部文字
- 注册 / 验证邮件的主题
- 邮件落款

---

### 4. 站点副标题

**位置**：Settings → General → 站点副标题

```
Unified AI API gateway — Claude, GPT, Gemini
```

**出现位置**：登录页 header、HomeView hero 副标题、AppSidebar 小字。

---

### 5. 邮件发件人

**位置**：Settings → Email → 发件人

```
noreply@modelway.dev
```

**前提**：modelway.dev 的 DNS 里已经配好 SPF + DKIM 让邮件能发出。如果还没配，先做 DNS：
- SPF: `v=spf1 include:sendgrid.net -all`（或你用的邮件服务）
- DKIM: 由邮件服务商给出 TXT 记录
- MX: 可选（没收件需求可不配）

---

### 6. Homepage 覆盖（可选，等 Landing 上线后做）

**位置**：Settings → Homepage → home_content

**方式 B（推荐，Landing 上线后启用）**：
```
https://modelway.dev
```

Sub2API 会把 `home_content` 当 iframe src 嵌入 `api.modelway.dev/home`，未登录用户访问 api 域名时自动看到 Landing。

**前提条件**：
- Landing 部署完成（modelway.dev 可访问）
- Landing 的 `X-Frame-Options` 不是 `DENY`（Cloudflare Pages 默认允许同域 iframe，需要验证 api.modelway.dev 可嵌入）
- Landing 的 CSP `frame-ancestors` 允许 `api.modelway.dev`

如果 Landing 还没上，先留空 → 访客看 Sub2API 默认 HomeView。

---

### 7-8. Privacy / Terms Custom Pages

**位置**：Settings → Custom Pages → 新建两个页面

| 路由 | 标题 | HTML 来源 |
|---|---|---|
| `/custom/privacy` | Privacy Policy | `exports/privacy-en.html` |
| `/custom/terms` | Terms of Service | `exports/terms-en.html` |

**双语版本**（如果 Sub2API admin 支持按语言配置）：
- `/custom/privacy` → EN → `privacy-en.html`
- `/custom/privacy-zh` → ZH → `privacy-zh.html`（或同路由，用浏览器语言自动切）

**注意**：Sub2API 的 Custom Pages **不走 Tailwind 编译**，HTML 只能用内联 style 或 `<style>` 块。我给的模板已经处理好。

---

### 9-10. 页脚链接

**位置**：Settings → Footer → Privacy URL / Terms URL

```
Privacy URL:  /custom/privacy
Terms URL:    /custom/terms
```

（相对路径即可，Sub2API 会自动拼到当前域名下）

如果页脚还有"联系我们"之类：
```
Contact: mailto:support@modelway.dev
```

---

## 验证清单（替换完跑一遍）

- [ ] 浏览器 tab 标题前显示 ModelWay 六边形 logo
- [ ] 浏览器 tab 标题是 `ModelWay - AI API Gateway`（或类似）
- [ ] 未登录访问 `api.modelway.dev` → 看到 ModelWay 品牌 + 副标题
- [ ] 访问 `/login` → Logo 和站名都是 ModelWay
- [ ] 访问 `/register` → 同上，注册后收到发件人是 `noreply@modelway.dev` 的邮件
- [ ] 访问 `/custom/privacy` → 显示 Privacy HTML，不是 404
- [ ] 访问 `/custom/terms` → 显示 Terms HTML
- [ ] 页脚链接点进去能正确打开 `/custom/privacy` 和 `/custom/terms`
- [ ] 登录后 AppSidebar 左上 Logo 是 ModelWay（不是 Sub2API）
- [ ] 切换 dark / light 模式 Logo 都清晰可见（SVG 或透明 PNG）

---

## 常见问题

**Q: Logo 上传后 AppSidebar 仍是旧图？**
A: 强刷浏览器缓存 `Cmd+Shift+R`。如果还不行，查看 Network tab 里 logo 请求的 304 或 200 状态 + Cache-Control。可能需要改 Logo 文件名强制破缓存。

**Q: Favicon 改完看不到变化？**
A: favicon 缓存最顽固。关浏览器所有 api.modelway.dev 标签页 → 清理 "Hosted app data" → 重开。或者隐身窗口验证。

**Q: Custom Page 里插入的样式被 Sub2API 覆盖？**
A: 用 `style="..."` 内联，避免被全局 CSS overrule。我给的模板已经全部用内联 style。

**Q: iframe 嵌入 Landing 看不见？**
A: 打开 DevTools Console 看 `frame-ancestors` 或 `X-Frame-Options` 报错。到 Cloudflare Pages 控制台加 `_headers` 文件：
```
/*
  X-Frame-Options: SAMEORIGIN
  Content-Security-Policy: frame-ancestors 'self' https://api.modelway.dev
```

---

## 回滚

如果替换出问题，回滚方式：
1. Settings → General → 站点 Logo → 清除（回到 Sub2API 默认 logo）
2. Settings → General → 站点名称 → 改回 `Sub2API`
3. Custom Pages → 删除 privacy / terms
4. Footer URL → 清空

Sub2API 的 admin 设置都是热生效，不需要重启后端。
