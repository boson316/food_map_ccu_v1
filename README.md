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

## Static site (GitHub Pages, no cold start)

Streamlit Community Cloud's free tier sleeps idle apps. `web/` is a **static** Leaflet port with the same features (filters, distance, composite score, open-now, wheel) running entirely in the browser, so it never sleeps. The frontend is shared across campuses; school settings live in `SCHOOL` in `scripts/export_static.py`.

- URL (once enabled): https://boson316.github.io/food_map_ccu_v1/
- Data: `python scripts/export_static.py` writes `web/data/places.json` and `web/data/config.json`.
- Deploy: `.github/workflows/pages.yml` re-exports and deploys on push to `main`. **One-time: Settings → Pages → Source → "GitHub Actions".**
- Local preview: `python scripts/export_static.py && python -m http.server -d web 8000`

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
