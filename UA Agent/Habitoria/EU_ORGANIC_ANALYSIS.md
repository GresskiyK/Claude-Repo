# EU Sessions Spike Analysis - Habitoria

**Date**: May 9, 2026  
**Data Source**: Amplitude (Sessions = Daily Active Users opening app)  
**Period**: Mar 10 - May 8, 2026

---

## Executive Summary

A significant spike in sessions appeared across multiple EU countries starting **May 1-3, 2026**. This represents engagement from **existing app users**, not new installs. **All EU countries moved from 0 to 1-6+ daily sessions simultaneously**, suggesting either:

1. **Halo Effect** — US paid campaign boosted app visibility/ASO, EU users dormant from Mar now activating
2. **Attribution Gap** — EU paid campaign running undetected (mislabeled as organic)
3. **Feature Launch** — In-app event/notification triggered global engagement on May 1

---

## Key Data Points

### US Baseline (Control)
| Period | Daily Avg | Trend |
|--------|-----------|-------|
| Mar 10-31 | ~71 sessions/day | Stable |
| Apr 1-30 | ~68 sessions/day | Stable, slight decline late Apr |
| May 1-8 | ~50 sessions/day | **Declining** (-26%) |

**Interpretation**: US engagement is **declining**, not increasing. Rules out viral/word-of-mouth from US users.

---

### EU Countries - New Engagement (May 1-8)

| Country | Mar-Apr Activity | May 1-8 Activity | Change |
|---------|------------------|-----------------|--------|
| **Germany** | 0/day | 4-6/day | **∞ (NEW)** |
| **France** | 0/day | 3-4/day | **∞ (NEW)** |
| **Spain** | 0/day | 2-4/day | **∞ (NEW)** |
| **Italy** | 0/day | 2-3/day | **∞ (NEW)** |
| **Poland** | 1-2/day | 4-5/day | **+200-300%** |
| **Denmark** | 0/day | 1/day | **∞ (NEW)** |
| **Czech Republic** | 0/day | 1-2/day | **∞ (NEW)** |
| **Turkey** | 0/day | 1/day | **∞ (NEW)** |
| **Netherlands** | 0-1/day | 1/day | **Slight increase** |
| **United Kingdom** | 0-1/day | 0-2/day | **Slight increase** |

**Critical Pattern**: Every major EU market went from **silent (0/day) to active (2-6/day) on the exact same dates** (May 1-3).

---

## Timeline Correlation

```
Mar 16:   Phase 1 launched (US, Google Ads, habit_toggle_today event)
          └─ No EU activity detected

Apr 10:   Phase 3 launched (US, Google Ads, subscription event)
          └ Still: EU = 0 sessions/day

Apr 25:   Phase 3 campaign paused
          └ US sessions begin declining (~68 → 50/day)
          └ EU remains silent

May 1-3:  SPIKE EVENT 🔥
          └ All EU countries suddenly show 1-6+ sessions/day
          └ Timing: 6 days after Phase 3 pause, 46 days after Phase 1 launch
```

---

## Root Cause Analysis

### Scenario A: Halo Effect (ASO Boost)
**Mechanism**: Phase 1 campaign (Mar 16) improved app store ranking, EU users discovering app organically.  
**Issue**: If true, why 46-day delay? Why synchronized spike across all EU on May 1-3?  
**Probability**: 🟡 **Medium** (timing doesn't align)

### Scenario B: Attribution Gap ⚠️ **HIGHEST RISK**
**Mechanism**: EU paid campaign running but mislabeled as organic.  
**Evidence**:
- Synchronized activation across all EU markets (typical of paid scaling)
- Zero activity through Apr 30, then immediate 2-6x increase May 1
- Patterns match "campaign launch" not "organic discovery"

**Action Required**:
1. ✅ Check Google Ads account for undetected EU campaigns (geo-targeting leak?)
2. ✅ Check Firebase Event reporting — are these actually from EU or mislabeled US?
3. ✅ Check Singular (MMP) dashboard for attribution source of these sessions

### Scenario C: Feature Launch / Push Notification
**Mechanism**: Something launched May 1 that triggered EU user re-engagement.  
**Evidence**: All regions activate simultaneously  
**Check**: App release notes for May 1, push notification logs, feature toggles

---

## What This IS NOT

❌ **Viral spread from US campaign** — US sessions declining, not correlated  
❌ **New installs spike** — This is sessions from existing app users  
❌ **Delayed install attribution** — Would show gradual increase, not synchronized spike  

---

## Phase 4 Strategy Implications

### IF Scenario B (Paid Running): 
⚠️ **CRITICAL**: You may be burning budget on untracked EU campaigns.
- **Action**: Immediately audit Google Ads geo-targeting
- **Impact on Phase 4**: Dangerous to launch EU phase 4 if Phase 3 EU is already running unseen

### IF Scenario A (Halo/Organic):
✅ **OPPORTUNITY**: Pre-warmed EU market ready for paid acquisition
- **Action**: Test Phase 4 in Germany, France, Spain (lowest CAC likely)
- **Timing**: Capitalize while organic momentum is high (May-June)
- **Budget**: 30-40% of Phase 4 spend could test EU markets

### IF Scenario C (Feature Launch):
✅ **GOOD NEWS**: Feature proved engagement driver
- **Action**: Document what launched & replicate in other regions
- **Phase 4**: Use same feature/push timing to drive conversions

---

## Next Steps (48 Hours)

### Priority 1: Audit (Now)
- [ ] Google Ads: Check all campaigns for accidental EU spend (Mar-May)
- [ ] Google Ads: Check geo-targeting settings on all active campaigns
- [ ] Firebase: Verify event source of these sessions (should show campaign source if paid)
- [ ] Singular: Compare Google Ads reporting vs Singular for EU activity

### Priority 2: Clarify (By May 11)
- [ ] App release notes: What launched May 1?
- [ ] Push notification logs: Any global push sent May 1?
- [ ] Amplitude: Filter to see if users are repeat sessions or new to app

### Priority 3: Decide (By May 15)
- [ ] If paid leak found: Pause, recalculate Phase 3 ROI
- [ ] If organic confirmed: Design EU Phase 4 test strategy
- [ ] If feature-driven: Plan Phase 4 to include that feature/push

---

## Recommendation

**Hold Phase 4 launch until Scenario B is ruled out.** 

If you're unknowingly spending on EU, launching Phase 4 could result in:
- Double-counting conversions (Phase 3 EU + Phase 4 EU simultaneously)
- False ROAS calculations
- Wasted budget on overlapping audiences

**Once EU attribution is verified**, Phase 4 should allocate 20-30% to top EU markets (Germany, France, Spain) given this organic momentum.

---

## Questions for Clarification

1. **Did you intentionally launch any EU campaigns between Apr 25-May 1?** (paused Phase 3, launched anything else?)
2. **Any app releases/features on May 1?**
3. **Access to Firebase raw data?** (Can you see campaign source of these sessions?)
4. **Access to Google Ads account?** (Can you check all campaign geo-targeting settings?)

---

**Analysis by**: Claude UA Agent  
**Status**: Pending verification of Scenario B  
**Next Review**: May 11, 2026 (after audit)