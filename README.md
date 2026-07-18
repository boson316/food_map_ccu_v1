# Campus Food Map CCU v1

**Languages:** [English](README.md) · [中文](README.zh-TW.md)

> **Status:** Implemented (forked from NIU v2) · **Spec:** [docs/v1-規格.md](docs/v1-規格.md)  
> **Source:** [food_map_niu_v2](https://github.com/boson316/food_map_niu_v2) · **Demo:** https://food-map-ccu-v1.streamlit.app

## Overview

Campus food map for **National Chung Cheng University (Minxiong)**. Offline Google Places cache, Huang-weighted rating × distance ranking, 15 food categories, wheel **Top 40**.

| Item | Value |
|------|-------|
| Center | `23.5615, 120.4808` |
| Default search radius | 1.5 km |
| Slider max | 3 km |
| Fetch pool | 8 km |
| Wheel | Top 40 |

## Quick start

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

## Docs

[PRD.md](PRD.md) · [ROADMAP.md](ROADMAP.md) · [SUMMARY.md](SUMMARY.md)
