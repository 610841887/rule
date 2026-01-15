## 自用规则
很复杂，也不知道怎么写的，有的写了测试，不知道有没有人在用，也不敢删
## 功能特性 (overwrite.yaml)

该配置采用了精细化的分流策略，不含DNS策略，主要特点包括：

### 1. 自动与故障转移机制
- **`♻️ 自动选择`**: 默认策略组。
    - **逻辑**: 优先使用 **`🧭 手动选择`** 中选定的节点。
    - **故障转移**: 当手动选定的节点不可用时，会自动降级使用 **`🔥 故障转移`** 组（原自动测速组），自动选择延迟最低的节点。
    - **优势**: 既保留了手动控制的灵活性，又具备自动容灾能力。

### 2. 精简的“📲 App”分组
为了简化界面，以下应用和服务被合并到了统一的 **`📲 App`** 分组中：
- Google, YouTube, Netflix, TikTok, Spotify 等流媒体
- Telegram, X (Twitter), Instagram, Facebook 等社交媒体
- GitHub, OpenAI (ChatGPT), Notion 等生产力工具
- Cloudflare 等基础设施

### 3. 游戏下载优化
- **强制直连**: 针对 Steam, Epic, Blizzard 等游戏平台的**下载流量**做了强制直连处理，避免消耗代理流量。
- **规则集**: 引入了 `GameDownload` 规则集 (`blackmatrix7`) 配合 `steamcontent.com` 等域名后缀匹配。
- **分流逻辑**:
    - 下载流量 -> `DIRECT`
    - SteamCN/国内游戏 -> `DIRECT`
    - 商店/社区/联机/非国区游戏 -> `🎮 Steam` (走代理)

### 4. 规则源 (Rule Providers)
- 配置引用了多个远程规则集（如 Adobe, Microsoft, Apple, Google 等），并映射到了本地的 `rule-providers` 配置中。
