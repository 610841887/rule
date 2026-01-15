## 自用规则
很复杂，也不知道怎么写的，有的为了测试，不知道有没有人在用，也不敢删

## ✨ 核心特性(overwrite.yaml)

### 1. ⚙️ 基础环境配置
- **网络设置**: 默认混合端口 `7893` (HTTP `7890`, SOCKS `7891`)。
- **DNS**: 启用 `fake-ip` 模式，配合 `fake-ip-filter` 优化国内域名解析，防止 DNS 污染。
- **Sniffer**: 针对 TLS, HTTP, QUIC 开启流量嗅探，优化域名识别。

### 2. 🛡️ 智能策略组架构

本配置采用了 **"手动优先，自动兜底"** 的高可用策略：

- **`♻️ 自动选择`**
    - 类型: `url-test` (自动测速)
    - **逻辑**: 在所有可用节点中自动选择延迟最低的节点。

- **`🧭 手动选择`**
    - 类型: `select`
    - **逻辑**: 用户手动指定使用的节点。

### 3. 🧩 应用分组聚合
为了简化面板，我们将同类服务合并至 **`📲 App`** 分组，包括但不限于：
- **流媒体**: YouTube, Netflix, TikTok, Disney+ 等。
- **社交/通讯**: Telegram, X (Twitter), Instagram, WhatsApp 等。
- **生产力/开发**: GitHub, OpenAI (ChatGPT), Notion, Google 等。

### 4. 🎮 游戏模式优化
- **下载直连**: 引入 `GameDownload` 规则集，针对 Steam, Epic, Blizzard 等平台的**下载流量强制直连**，节省代理流量。
- **规则细节**:
    - ` steamcontent.com`, `steamserver.net` -> `DIRECT`
    - 国内游戏 / SteamCN -> `DIRECT`
    - 游戏联机 / 商店 / 社区 -> 走代理 (`🎮 Steam`)
该配置采用了精细化的分流策略 主要特点包括：

### 1. 精简的“📲 App”分组
为了简化界面，以下应用和服务被合并到了统一的 **`📲 App`** 分组中：
- Google, YouTube, Netflix, TikTok, Spotify 等流媒体
- Telegram, X (Twitter), Instagram, Facebook 等社交媒体
- GitHub, OpenAI (ChatGPT), Notion 等生产力工具
- Cloudflare 等基础设施

### 2. 游戏下载优化
- **强制直连**: 针对 Steam, Epic, Blizzard 等游戏平台的**下载流量**做了强制直连处理，避免消耗代理流量。
- **规则集**: 引入了 `GameDownload` 规则集 (`blackmatrix7`) 配合 `steamcontent.com` 等域名后缀匹配。
- **分流逻辑**:
    - 下载流量 -> `DIRECT`
    - SteamCN/国内游戏 -> `DIRECT`
    - 商店/社区/联机/非国区游戏 -> `🎮 Steam` (走代理)

### 3. 规则源 (Rule Providers)
- 配置引用了多个远程规则集（如 Adobe, Microsoft, Apple, Google 等），并映射到了本地的 `rule-providers` 配置中。
