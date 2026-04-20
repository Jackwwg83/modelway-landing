# ModelWay Brand — Constraints (from Sub2API integration)

这份文档吸收了 Sub2API 的技术约束，是所有 Logo / Landing / 品牌决策的 ground truth。任何设计决策都必须先通过这里的 checklist。

---

## 1. Logo 技术规格

| 字段 | 要求 |
|---|---|
| 格式 | PNG / JPG / **SVG（首选，透明底）** |
| 最大大小 | 300 KB |
| 建议尺寸 | 80×80 正方形 |
| 透明度 | SVG 透明背景最优，自动适应 light/dark |
| 使用位置 | `AppSidebar.vue`（左上圆角正方形）· `AuthLayout.vue`（登录/注册页）· `HomeView.vue`（未登录 hero 左上） |

**必须交付：**
- [x] 主 Logo SVG（icon only, 正方形, 透明背景）← 当前 6 变体已满足
- [ ] **Wordmark 横版 SVG**（icon + "ModelWay" 文字, 适合 header） ⚠️ 待补
- [ ] **80×80 PNG**（主 Logo 的栅格版, 给 Sub2API 上传用） ⚠️ 待导出
- [ ] **32×32 Favicon**（PNG 或 ICO） ⚠️ 待导出
- [ ] 验证 light 和 dark 两个背景都清晰

**设计约束：**
- 所有 SVG 必须用 `currentColor`（fill + stroke）→ 自动适应主题色 ✅ 已满足
- Icon 版本必须在 16×16 和 80×80 都清晰
- Wordmark 版本文字字重需 500-600，间距对齐 icon baseline

---

## 2. 色彩策略（关键决策点）

### Sub2API 默认
```
primary:  teal / cyan   (#14b8a6 → #0ea5e9)
surface:  white / slate
text:     slate-800 / slate-100 (dark mode)
```

### 冲突与选项

| 方案 | 主色 | Sub2API 修改 | 成本 | 品牌气质 |
|---|---|---|---|---|
| **A. 对齐 Cyan** | `#0ea5e9` Sky 系 | 无需改动 | 0 | API/infra 感（偏 Vercel/HashiCorp） |
| **B. 对齐 Teal** | `#14b8a6` Teal 系 | 无需改动 | 0 | 平衡冷静（偏 Linear） |
| **C. 双色组合** | `#0ea5e9` 主 + `#8b5cf6` accent | 无需改动 | 低 | API 感 + 保留 AI 紫点缀 |
| **D. 纯电气紫** | `#8b5cf6` Violet 系 | 改 `tailwind.config.js` + 重编译 | 中 | 最 AI 前卫 |
| **E. CF Worker 注入 CSS 覆盖** | 任意色 | 新增 Worker | 中高 | 最灵活但多一层基础设施 |

**推荐：方案 C（双色组合）**
- 主色用 **Cyan `#0ea5e9`**（对齐 Sub2API primary，零成本）
- 强调色用 **Violet `#8b5cf6`**（CTA 按钮、hover 状态、关键数据点 → 保留 AI 趋势感）
- Logo 单色（currentColor）→ 在 Sub2API 里显示 cyan，在 Landing hero 可以显示 violet 或 gradient
- **双方视觉基本一致，但 Landing 有差异化的 AI 感**

### 暗色模式
- Sub2API 有完整 dark mode
- Landing 必须支持 dark mode（默认 dark，可切 light）
- dark bg: `#0a0a0f` / `#12121a` （我们已在 showcase 里使用）
- light bg: `#fafafa` / `#ffffff`

---

## 3. 域名与路由

```
modelway.dev         →  Cloudflare Pages (Landing)    ← 我们负责
www.modelway.dev     →  同上（CNAME 或 redirect）
api.modelway.dev     →  AWS EC2 / Sub2API (Dashboard)  ← 已部署
```

### CTA 链接（Landing 出口）
```
https://api.modelway.dev/register          # 注册 + 领 Free Credit
https://api.modelway.dev/login             # 登录
https://api.modelway.dev/admin/dashboard   # 已登录用户跳转
```

### api.modelway.dev/home 覆盖（可选）
- **方式 B 推荐**：`home_content` 填 `https://modelway.dev` → sub2api 自动 iframe 嵌入
- 要求：Landing **不能**设置 `X-Frame-Options: DENY`
- Cloudflare Pages 默认允许自己域名的 iframe ✅

---

## 4. 文字内容（已在 admin 配置）

| 字段 | 值 |
|---|---|
| 站点名称 | ModelWay |
| 站点副标题 | Unified AI API gateway — Claude, GPT, Gemini |
| API 端点 | https://api.modelway.dev |
| 客服联系 | support@modelway.dev |

**Landing 文案必须对齐这个 voice。**

---

## 5. 字体与图标

**Sub2API 实际使用（2026-04-19 从 `frontend/src/style.css` 核实）**：
- **纯 system-ui stack，不引 Google Fonts**
- 理由：亚太（中国）用户无墙、速度快、零 layout shift
- Landing 必须对齐，不能用 Inter / Geist 等 Google Fonts 字体

```css
font-family: system-ui, -apple-system, BlinkMacSystemFont,
             'Segoe UI', Roboto, 'Helvetica Neue', Arial,
             'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei',
             sans-serif;

/* 代码 / 数字 */
font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
```

| 资产 | Sub2API | Landing 对齐值 |
|---|---|---|
| Sans 字体 | system-ui stack | **相同** ✅ |
| Mono 字体 | ui-monospace stack | **相同** ✅ |
| UI 图标 | `@lobehub/icons@4.x` | Lucide（可接受偏差），或用 @lobehub/icons 完全对齐 |

---

## 6. Landing 技术栈决策（确认）

```
框架：     Astro 4.x
UI 层：    React Islands + Tailwind CSS v4 (darkMode: 'class')
组件：     shadcn/ui (关键组件) + 自定义
图标：     Lucide React（或 @lobehub/icons 对齐 Sub2API）
i18n：     URL 子路径（/ = EN default, /zh/ = 中文）
字体：     system-ui stack（sub2api 对齐，不引 Google Fonts）
部署：     Cloudflare Pages (git push 自动部署)
域名：     modelway.dev + www.modelway.dev
```

### X-Frame-Options 配置
Landing 必须配 `X-Frame-Options: SAMEORIGIN` 或不设此 header（默认允许）。不能设 `DENY`，否则 api.modelway.dev 无法 iframe 嵌入。

---

## 7. 最终交付清单（给 Landing 方的"完工条件"）

- [ ] 主 Logo SVG（icon-only 正方形 + 透明背景）
- [ ] Wordmark SVG（icon + 文字横版）
- [ ] Logo PNG 80×80（给 Sub2API admin 上传）
- [ ] Logo PNG 512×512（高分辨率版本）
- [ ] Favicon 32×32 PNG + favicon.ico
- [ ] Apple Touch Icon 180×180 PNG
- [ ] OG Image 1200×630 PNG（社交分享）
- [ ] 品牌主色 HEX + 副色 + accent
- [x] 字体确认（system-ui + ui-monospace stack，sub2api 对齐）
- [ ] Landing 部署到 Cloudflare Pages（modelway.dev）
- [ ] `X-Frame-Options` 正确配置（允许 iframe）
- [ ] 中英文 i18n 运转正常
- [ ] Dark / Light 双模式切换正常

---

## 8. 锁定决策 (2026-04-19)

### ✅ Logo: V4C Hexagon Lock
- 六边形外轮廓 + 6 辐节点 + 中心 hub
- 文件: `logos-v4/v4c-hexagon.svg` → 会被复制为 canonical `logos/primary-icon.svg`
- 语义: 平台边界 + 统一 gateway + 多模型路由

### ✅ 色彩策略: 跟随 Sub2API (方案 B)
主色锁定 **Teal**，精确值来自 `sub2api/frontend/tailwind.config.js:primary.500`：

```css
--primary:       #14b8a6;  /* teal-500  — 主色 */
--primary-600:   #0d9488;  /* teal-600  — 深态/gradient 暗端 */
--primary-400:   #2dd4bf;  /* teal-400  — 亮态/hover */
--gradient:      linear-gradient(135deg, #14b8a6 0%, #0d9488 100%);
```

Landing 和 Sub2API 视觉完全一致，零 CSS 覆盖成本。之前 showcase 里的 violet `#8b5cf6` **已废弃**，将被 teal 替换。

### 还未定但可用默认值推进
- [ ] **Landing 是否嵌入 api.modelway.dev/home iframe**：默认暂不嵌入，Landing 部署后再决定
- [ ] **UI 图标库**：默认 Lucide（零成本），Sub2API 视觉切换不致命
