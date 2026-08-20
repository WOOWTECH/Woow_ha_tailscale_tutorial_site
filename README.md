# Home Assistant Tailscale 資源總站（教學 · 銷售 · 提示詞 · Skill）

[HA Tailscale add-on](https://github.com/home-assistant/addons/tree/master/tailscale) 的四本手冊集中地，繁體中文靜態網站：

| 分類 | 頁面 | 給誰 | 下載 |
|---|---|---|---|
| **入住教學** | [`tutorial.html`](https://ha-tailscale-guide.woowtech.io/tutorial.html) ＋ 12 章 | 用戶 | 整站 zip（GitHub archive） |
| **銷售手冊** | [`sales.html`](https://ha-tailscale-guide.woowtech.io/sales.html) | 客戶與經銷商 | 自包含單檔 HTML |
| **提示詞庫** | [`prompts.html`](https://ha-tailscale-guide.woowtech.io/prompts.html) | 使用 AI agent 的進階用戶（40+ 條可複製） | 自包含單檔 HTML |
| **Skill 手冊** | [`skills.html`](https://ha-tailscale-guide.woowtech.io/skills.html) | 進階用戶（型錄＋速查） | 自包含單檔 HTML |

四類共用一個對外入口 [`index.html`（資源總覽）](https://ha-tailscale-guide.woowtech.io/)，hub 上提供各分冊的線上閱讀與下載載點。

- **讀者**：會用 Home Assistant 但不需要寫程式的智慧家庭愛好者
- **前提**：Home Assistant 已裝好可以登入
- **語言**：繁體中文（台灣用語）
- **授權**：CC BY 4.0

## 範圍

- **教學**：HA Tailscale App、tailnet、Machines、私有遠端存取、最小權限、Tailscale Serve 概念、單一 subnet router 基礎與 route approval。
- **銷售**：兩種代交付模式—HAOS add-on 代設定（官方 Tailscale）與 WoowTech Headscale 雲端 PaaS。
- **提示詞**：透過 REST API／CLI／MCP 用自然語言操作 Tailscale。
- **Skill**：Tailscale／Headscale／網路自動化與 home-lab 相關的 AI agent skill 型錄。

## 部署

GitHub Pages ＋ 自訂網域：**https://ha-tailscale-guide.woowtech.io/**（DNS 為 Cloudflare 上的 CNAME → `woowtech.github.io`）

## 站內結構（hub 模式）

```
index.html          資源總覽 hub    ← 人手維護，build_nav 不碰
tutorial.html       教學目錄        ← build_nav 產生（chapters.json 的 hub.catalog）
ch*.html            教學內容頁      ← head/側欄/pager/footer 由 build_nav 產生
sales.html          銷售手冊        ← 自包含單檔（自帶樣式與圖示，可直接下載）
prompts.html        提示詞庫        ← 自包含單檔，同上
skills.html         Skill 手冊      ← 自包含單檔，同上
chapters.json       單一來源        ← 章節順序/文案/SEO + hub 設定（catalog、pages）
```

規則：

- 教學章節照舊由 `chapters.json` ＋ `<section data-nav>` 驅動，改完跑 `node scripts/build_nav.js`；目錄卡片輸出到 `tutorial.html`，側欄自帶「◂ 資源總覽」回 hub。
- `sales.html` / `prompts.html` / `skills.html` 是**自包含單檔**（樣式、圖示全部內嵌，離線可開），列在 `chapters.json` 的 `hub.pages`，會納入 sitemap 與 `check_links` 白名單，但不吃內容頁房規（kicker/FAQ/data-icon 對 style.css 的檢查）。
- 新增第五本手冊：寫好自包含 HTML → `hub.pages` 加一筆 → `index.html` 加卡片 → 重跑 build_nav。

## 本地開發

```bash
git clone https://github.com/WOOWTECH/Woow_ha_tailscale_tutorial_site
cd Woow_ha_tailscale_tutorial_site

node scripts/build_nav.js --check   # 導覽與 chapters.json 是否同步
node scripts/check_links.js         # 站內連結/錨點/sitemap 健檢
node scripts/build_nav.js           # 產生 head、側欄、pager、footer、sitemap
```

所有 `<head>`、側欄、上下章導覽、教學目錄卡片、`sitemap.xml` 都是 `scripts/build_nav.js` 產生的——手動改會在下一次 CI 被覆蓋回去（`index.html` 與三本單檔手冊除外）。

新章節寫作規範：見 [`STYLE.md`](STYLE.md)。

## 這個站是怎麼建起來的

Fork 自姊妹站《[HA 入住指南](https://github.com/WOOWTECH/Woow_ha_tutorial_site)》與《[Pi Agent 入住指南](https://github.com/WOOWTECH/Woow_ha_pi_agent_tutorial_site)》，共用同一套 build_nav / check_links / capture 管線與 WoowTech 品牌樣式；銷售手冊、提示詞庫、Skill 手冊為 WoowTech 品牌規範（Brand Prompt Library v2）下的自包含單檔版型。

## 授權與致謝

《Home Assistant Tailscale 遠端連線指南》與三本分冊由 [WoowTech](https://github.com/WOOWTECH) 製作，以 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.zh-hant) 授權釋出——可自由分享與改作，請保留出處。

Skill 手冊中的第三方 skill 集合各依其原始授權；集合規模數據為 2026-08-20 調查當日之 GitHub 公開資訊。

截圖取自 Home Assistant 官方介面。Home Assistant 為 Open Home Foundation 的商標；Tailscale™ 為 Tailscale Inc. 商標；Headscale 為社群開源專案。本站與其均無隸屬關係。
