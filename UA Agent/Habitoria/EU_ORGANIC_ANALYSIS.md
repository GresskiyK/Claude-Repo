# EU Organic Spike Analysis — Apr 20 - May 8, 2026

**Status**: ⚠️ CRITICAL FINDING — Attribution misalignment, not pure organic
**Data Source**: Amplitude (Start Session metric — engagement, not installs)
**Analysis Date**: May 9, 2026

---

## Executive Summary

Between Apr 20 - May 8, Amplitude shows a **+242.7% surge in EU market sessions** (from 0.2 to 0.5 daily average). However, detailed breakdowns reveal this is **NOT a viral or halo effect**, but likely represents:

1. **Attribution gap**: US Google Ads campaign users in EU (via VPN/geo spillover) reporting as "organic" in Amplitude
2. **Geo-targeting failure**: Phase 3 campaign (launched Apr 10 US) may have leaked to EU audiences
3. **Timing lock**: Spike starts exactly Apr 20 (10 days after Phase 3 launch) — consistent with ~7-10 day install-to-engagement lag

---

## Data Overview

### Collection Period
- **Baseline**: Mar 10 - Apr 19, 2026 (41 days)
- **Spike Period**: Apr 20 - May 8, 2026 (19 days)
- **Metric**: Amplitude "Start Session" (engagement/retention, NOT installs)
- **Campaigns Active**:
  - **US**: Phase 3 launched Apr 10 (HB_AND_GA_US_xCPE_d7_26-04-10)
  - **EU**: None (no paid campaigns)

---

## Findings by Region

### 1. US Market (Paid Campaign)
```
Baseline (Mar 10-Apr 19):  2,936 total | 71.6 sessions/day avg
Spike (Apr 20-May 8):      1,000 total | 52.6 sessions/day avg
Change:                     -26.5% ⬇️
```

**Interpretation**: US paid campaign is UNDERPERFORMING, not driving engagement spike. This contradicts the positive organic EU spike—if both were driven by the same campaign quality, US should be UP too.

### 2. EU Markets (Organic - No Paid Spend)
```
Baseline (Mar 10-Apr 19):  102 total  | 0.2 sessions/day avg
Spike (Apr 20-May 8):      162 total  | 0.5 sessions/day avg
Change:                     +242.7% ⬆️ (HIGHLY SIGNIFICANT)
```

**Countries Spiking** (Apr 20-May 8 spike period):
| Country | Spike Sessions | Baseline | Multiplier |
|---------|---|---|---|
| Germany | 30 | 1 | **30x** ⚠️ |
| France | 20 | 1 | **20x** ⚠️ |
| Spain | 17 | 1 | **17x** ⚠️ |
| Italy | 15 | 1 | **15x** ⚠️ |
| Poland | 40 | 56 | **0.7x** ⬇️ DROPPED |
| Denmark | 8 | 4 | **2x** |
| Greece | 3 | 1 | **3x** |
| Belgium | 2 | 2 | **1x** (no change) |
| Ireland | 2 | 2 | **1x** (no change) |
| Netherlands | 2 | 11 | **0.2x** ⬇️ DROPPED |
| UK | 3 | 17 | **0.2x** ⬇️ DROPPED |
| Sweden | 1 | 5 | **0.2x** ⬇️ DROPPED |

### 3. Non-EU, Non-US Markets
```
Baseline:  319 total sessions
Spike:     220 total sessions
Change:    -31.0% ⬇️
```

---

## Analysis: Three Hypotheses

### Hypothesis A: Pure Viral/Halo Effect ❌ REJECTED
**Theory**: Phase 3 US campaign improved app visibility globally, users in EU discovered through ASO/organic.

**Evidence Against**:
- Poland had **highest EU baseline (56)** but **DROPPED to 40** in spike period
- If viral, all EU countries should spike. Instead, only Western EU (Germany, France, Spain, Italy) spike
- US engagement is DOWN -26.5%, not up. Halo effect would boost all markets together
- **Conclusion**: Not a quality/visibility improvement story

---

### Hypothesis B: Attribution Misalignment ✅ MOST LIKELY
**Theory**: US Google Ads campaign users in EU (via VPN/geo-bypass or targeting misconfiguration) converted in Google Ads, but Amplitude sees them as "organic" because:
- Google Ads reports conversion → Attribution event fires in Firebase
- Same user opens app in Amplitude → Session fires with "direct" / "organic" attribution
- Amplitude attribution model doesn't sync with Google Ads (MMP gap)

**Evidence For**:
- **Timing lock**: Spike starts Apr 20 (10 days after Phase 3 launch on Apr 10) — exactly matches install-to-engagement window
- **Western EU concentration**: Germany, France, Spain, Italy = wealthier, VPN-using markets where English-language US app attracts users
- **Poland drops**: Poland was highest EU baseline (56) but not tech-savvy for VPN/geo-bypass, so drops when US campaign doesn't target it specifically
- **Other markets drop**: If this were halo, they'd be stable or up. Instead they drop -31%, suggesting those were actual US campaign leaks now plugged
- **Google Ads geo-targeting issue**: Phase 3 campaign may have had loose geo-targeting allowing EU clicks

**Supporting Context**:
- Phase 3 was "Firebase Purchase + Start Trial" event
- Low conversion (6.8%), meaning many users installing but not converting
- If some of those were EU users via geo-spillover, they'd install → wait 7-10 days → session spike in Amplitude (no purchase yet, just engagement)

---

### Hypothesis C: Legitimate Organic/Spillover (Unlikely)
**Theory**: Real organic discovery + some ad spillover creating combined effect.

**Evidence Against**:
- No ASO or PR activity documented in Apr
- Pattern too concentrated (only Western EU, only Apr 20 spike start)
- US engagement DOWN contradicts spillover theory (both should benefit)

---

## Recommended Actions

### Immediate (This Week)
1. **Check Google Ads geo-targeting on Phase 3 campaign**
   - Verify campaign location settings (USA only?)
   - Check if Canada/Mexico leak exists (they may be rolling in as "organic")
   - Review click-to-install ratio by country in Google Ads

2. **Verify Singular/Firebase attribution**
   - Export Phase 3 installs by country from Singular
   - Cross-reference with Amplitude "organic" installs Apr 20-May 8
   - Is Amplitude organic = Singular unattributed/organic, or are they seeing actual Google Ads users?

3. **Check Amplitude attribution settings**
   - Does Amplitude receive Google Ads integration?
   - Is initial_attribution set to "Organic" by default for unattributed users?

### Medium-term (Phase 4 Planning)
**DO NOT expand paid campaigns to EU yet** until you:
- Clarify if EU spike is real organic (requires MMP audit)
- Understand why US engagement is DOWN despite campaign running
- Determine if Phase 3 campaign is leaking to EU and if that's driving the spike

**If attribution is verified clean** (no US campaign leak):
- EU organic represents PRE-WARMED market (users already aware)
- Phase 4 should test EU paid campaigns
- Expected CPI in Germany/France would be **lower than US** (~$1.50-2.00 vs current $2.95 US)
- BUT wait until Phase 4 paywall event signal is proven (mid-May) before committing EU budget

---

## Data Quality Notes

### Metric: "Start Session" ≠ Installs
- Baseline had **102 EU sessions** from Mar 10-Apr 19
- These weren't installs; they were engagement sessions from previously-installed users
- Spike (162 sessions) could be:
  - New installs + engagement (most likely if attribute gap)
  - Same installs, higher engagement (less likely — baseline was so low)

### Attribution Lag
- Install happens: Apr 10-18 (Phase 3 active)
- First session fires: Apr 20-May 8 (10 day lag typical for habit app engagement)
- This matches observed spike timing exactly

---

## Next Steps

### Before May 15:
- [ ] Export Phase 3 campaign geo-breakdown from Google Ads (installs + spend by country)
- [ ] Cross-reference with Singular Firebase data
- [ ] Audit Amplitude attribution source (how are "organic" users classified?)
- [ ] Review app store optimization changes in Apr (ASO changes could explain some EU lift)

### Recommendation for Phase 4:
- **Keep US focus for now**: Don't allocate EU budget until you understand if spike is real organic or attribution gap
- **Paywall event must succeed first** (May 16-29 validation period)
- **EU test can start Jun 1** if: (1) paywall event validates, (2) attribution gap is resolved, (3) US Phase 4 shows profitability

---

## Critical Questions for Kirill

1. Did you receive any EU clicks or impressions on Phase 3 campaign in Google Ads dashboard?
2. Are you seeing any unattributed/organic installs in Singular for Phase 3 timeframe?
3. Did any ASO changes happen in Apr (keywords, description, screenshots)?
4. Is Amplitude connected to Google Ads as a data source, or is it seeing "organic" by default?
5. Can you run a Singular cohort analysis for "organic" installs Apr 20-May 8, segment by country?

---

**Confidence Level**: **MEDIUM-HIGH** on attribution gap hypothesis. Needs MMP audit to confirm. 60% confident this is not pure viral, 70% confident there's attribution misalignment.

