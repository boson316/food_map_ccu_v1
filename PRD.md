# PRD — 校園美食地圖 CCU v1（國立中正大學）

> **v1 完整規劃：** [docs/v1-規格.md](docs/v1-規格.md)  
> **程式碼來源（Fork）：** `校園美食地圖_v2` / https://github.com/boson316/food_map_niu_v2  
> **目標 repo：** https://github.com/boson316/food_map_ccu_v1

## 1. 問題與目標

- **問題陳述**：中正大學生在民雄校本部周邊覓食時，餐廳分散、步行可達範圍外仍有選擇，難以依網路評價（星等＋評論量）、距離、預算與營業狀態快速排序與抽選。
- **目標使用者**：國立中正大學學生（機車／步行可達範圍為主）。
- **校園中心**：民雄校本部（大學路一段168號）約 `23.5615°N, 120.4808°E`。
- **成功條件**：
  - 可設定中心座標與搜尋半徑，列出半徑內餐廳。
  - 綜合分（黃氏星等 × 距離衰減）排序；15 類美食篩選；轉盤 Top 40。
  - CLI + Streamlit；離線 Google Places 快取為主。

## 2. 功能邊界（In Scope）

- **FR-1**：依中心點、半徑（公里）篩選餐廳。
- **FR-2**：最少評論數；綜合／貝氏／黃氏／距離四種排序。
- **FR-3**：CLI `table`／`json`；Google Maps 連結。
- **FR-4**：Streamlit 地圖表 + 轉盤；中心預設中正大校本部。
- **FR-5**：離線 JSON 快取（`places_cache.public.json`）。
- **FR-v1-1**：預設搜尋半徑 **3 km**；Slider 上限 **8 km**。
- **FR-v1-2**：資料池 fetch **8 km** 內盡量抓滿（格網 + 逐類型 + Text Search）。
- **FR-v1-3**：平價篩選、營業狀態、轉盤排除休息中（沿用 v2 邏輯）。
- **FR-v1-4**：轉盤候選 **Top 40**（正餐為主）。

## 3. 非目標（Out of Scope）

- **NFR-1**：每次查詢即時打 Google API（以離線快取為主）。
- **NFR-2**：帳號、收藏、路線導航。
- **NFR-3**：v1 不做多校共用單 codebase（獨立 repo；見 decision artifact）。
- **NFR-4**：嘉義市區第二中心點（v1.1 再加購）。

## 4. KPI（可量測，同步 `slo.config.json`）

- `pytest -q` 全綠；coverage ≥ 70%（Fork 後沿用 v2 測試）。
- 快取 ≤8 km 內 unique 餐飲 POI ≥ 300（實測目標，非硬性上限）。
- Streamlit 公開 demo 可開啟地圖 + 轉盤。

## 5. NO-GO 條件

- 核心模組 integrity 驗證失敗。
- 無 `places_cache.public.json` 且無 Mock 可 demo。
- 轉盤含休息中店家（回歸 v2 行為）。

## 6. 風險與假設

- **風險**：8 km fetch API 費用高、時間長；民雄稀疏區評論數偏少。
- **假設**：中心座標以校本部為準；學生可接受預設 3 km、手動拉到 8 km。
- **緩解**：分階段 fetch（先 grid 10 / target 1000）；`food_group_overrides.json` 人工校正。

## 7. 交付雙指標

| 指標 | 定義 | 目標 |
|------|------|------|
| code_complete | Fork + 常數 + 快取 + 測試綠 | 0% → 目標 80% |
| go_to_market | Streamlit 公開 URL + 作品集卡片 | 0% → 目標 40% |

## 8. Phase 與 Scope 鎖

- **Phase 1 MVP：** Fork `food_map_niu_v2`、改校園常數、fetch 8 km、部署 Streamlit。
- **v1.1（Out of Scope）：** 轉盤 pin、嘉義市次中心、core 抽共用 package。
