# Habitoria — Campaign Notes & Context

This file contains specific context for Habitoria's UA campaigns to help the agent interpret performance data.

## Campaign Descriptions

| Campaign Name | Objective / Description |
|---------------|-------------------------|
| `HB_AND_GA_HK_xCPE_d7_26-03-26` | Mid-funnel goal: "habit toggle today" event. Target GEO: Hong Kong (HK). |
| `HB_AND_GA_US_xCPE_d7_26-03-16` | Mid-funnel goal: "habit toggle today" event. Target GEO: USA (US). |
| `HB_AND_GA_US_xCPE_d7_26-04-10` | Current campaign. Goal: In-app event targeting (Firebase events). Uses `xCPE` naming. |

### Naming Convention Structure
`app_OS_source_geo_opt mode_attr window_date`

**Key**:
- **App**: `HB` (Habitoria)
- **OS**: `AND` / `iOS`
- **Source**: `GA` (Google Ads)
- **GEO**: `US`, `HK`, `WW`
- **Opt Mode**: `xCPE` (Maximize Conversions for event occurrences)
- **Attr Window**: `d7` / `d1`
- **Date**: `YY-MM-DD`

## Optimization Context
- For campaigns with `xCPE` (like the current one), we are looking for high volume of events. 
- Even if "Conversion Value" is 0 initially, we track "In-app actions" (Firebase events) as the primary indicator of success.
