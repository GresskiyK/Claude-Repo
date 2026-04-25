# Habitoria — Data Source

## Google Sheet
**Name**: Habitoria UA Antigravity
**URL**: https://docs.google.com/spreadsheets/d/1wQgdYyeR-EPeD8xc_AKgBrReMUs_z23NdOY46XlJKmw/edit?usp=sharing
**Sheet ID**: `1wQgdYyeR-EPeD8xc_AKgBrReMUs_z23NdOY46XlJKmw`

## Tabs

| Tab Name | GID | Read URL |
|----------|-----|----------|
| Campaign Performance | 0 | `https://docs.google.com/spreadsheets/d/1wQgdYyeR-EPeD8xc_AKgBrReMUs_z23NdOY46XlJKmw/gviz/tq?tqx=out:csv&sheet=Campaign%20Performance` |
| Campaign Assets Performance | 857571599 | `https://docs.google.com/spreadsheets/d/1wQgdYyeR-EPeD8xc_AKgBrReMUs_z23NdOY46XlJKmw/gviz/tq?tqx=out:csv&sheet=Campaign%20Assets%20Performance` |
| Campaign GEO Performance | 1064265557 | `https://docs.google.com/spreadsheets/d/1wQgdYyeR-EPeD8xc_AKgBrReMUs_z23NdOY46XlJKmw/gviz/tq?tqx=out:csv&sheet=Campaign%20GEO%20Performance` |

## Local History
Each tab's data is accumulated in the matching subfolder's `history.csv`:
```
Habitoria/
├── DATA_SOURCE.md              ← this file
└── Google Ads/
    ├── Campaign Performance/
    │   └── history.csv
    ├── Campaign Assets Performance/
    │   └── history.csv
    └── Campaign GEO Performance/
        └── history.csv
```
