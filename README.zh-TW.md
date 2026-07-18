# 校園美食地圖 CCU v1

**Languages:** [English](README.md) · [中文](README.zh-TW.md)

> **狀態：** 已實作（自宜大 v2 Fork）· **規格：** [docs/v1-規格.md](docs/v1-規格.md)  
> **宜大 v2 來源：** https://github.com/boson316/food_map_niu_v2 · **Demo：** https://food-map-ccu-v1.streamlit.app

國立中正大學民雄校本部周邊美食地圖。離線 Google Places 快取、黃氏星等×距離排序、15 類篩選、轉盤 Top 40。

## 校園參數（已鎖定）

| 項目 | 值 |
|------|-----|
| 中心點 | `23.5615, 120.4808`（民雄校本部） |
| 預設搜尋半徑 | **0.5 km** |
| Slider 上限 | **3 km** |
| 資料池 fetch | **8 km** |
| 轉盤 | Top **40** |

## 本機執行

```powershell
cd food_map_ccu_v1
python -m pip install -r requirements.txt
$env:PYTHONPATH = "src"
python -m pytest -q --cov=src --cov-fail-under=70
streamlit run streamlit_app.py
```

## CLI

```powershell
$env:PYTHONPATH = "src"
python -m foodmap search --lat 23.5615 --lon 120.4808 --sort composite --data data/places_cache.public.json
```

## 文件索引

[PRD.md](PRD.md) · [ROADMAP.md](ROADMAP.md) · [SUMMARY.md](SUMMARY.md)
