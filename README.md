# Home Assistant Tailscale 遠端連線指南

12 章繁體中文靜態教學，帶 Home Assistant 使用者透過 Tailscale App 建立私有遠端存取，並包含 subnet router 基礎、路由核准與排錯。

**線上閱讀：<https://ha-tailscale-guide.woowtech.io/>**

## 範圍

- 包含：HA Tailscale App、tailnet、Machines、私有遠端存取、最小權限、Tailscale Serve 概念、單一 subnet router 基礎與 route approval。
- 不包含：exit node、DNS override、公開 Funnel 的設定教學。
- 目標讀者：已會安裝 HA App、看得懂基本 CLI／網路名詞，但不需要寫程式的 HA 使用者。

## 維護

`chapters.json` 是章節、導航、SEO 與 sitemap 的單一來源。變更內容後執行：

```bash
node scripts/build_nav.js
node scripts/check_links.js
```

截圖由 `scripts/annotations.json` 和 `scripts/capture.js` 產生；把 HA 帳密放進未追蹤的 `.env`。

本站內容以 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.zh-hant) 授權，保留 WoowTech 出處。教學模板源自 [Woow_ha_tutorial_site](https://github.com/WOOWTECH/Woow_ha_tutorial_site)。Home Assistant 與 Tailscale 為其各自權利人的商標，本站與其無隸屬關係。
