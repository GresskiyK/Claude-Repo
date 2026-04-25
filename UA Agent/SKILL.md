---
name: ua-agent
description: "UA (User Acquisition) performance analysis across mobile projects. This workspace is the central hub for analyzing ad performance data across channels."
---

# UA Agent — Instructions

## Data Source Configuration

### Remote Repository Access
The agent reads the **Git_Creds** file to retrieve the remote repository URL dynamically:
- **Git_Creds Location**: `/mnt/project/Git_Creds`
- **Format**: `Repo URL: https://github.com/[owner]/[repo]`

**Why**: The remote repo URL is not hardcoded. If you change the URL in Git_Creds, the agent automatically uses the new repository. This enables seamless migration between repos or remotes without modifying the skill.

### Project Structure
Each app/project has its own folder in the remote repo (`UA Agent/[AppName]/`) with:
- **`DATA_SOURCE.md`** — Google Sheet URL, sheet ID, and CSV tab URLs
- **`APP.md`** — App-specific context (store links, monetization, categories)
- **`STRATEGY.md`** — High-level roadmap and "Current Phase" context
- **`[Platform]/`** subdirectories (e.g., `Google Ads/`) containing:
  - `CAMPAIGN_NOTES.md` — Campaign naming conventions and optimization context
  - `Campaign Performance/history.csv` — Accumulated campaign data
  - `Campaign Assets Performance/history.csv` — Asset-level performance
  - `Campaign GEO Performance/history.csv` — Geographic performance data

**To find data for any project**:
1. Read `DATA_SOURCE.md`, `APP.md`, and `STRATEGY.md` from the remote repo
2. Follow the CSV read URLs in `DATA_SOURCE.md` to access live Google Sheet data
3. Reference the Google Sheet as the source of truth for all current data

### Mandatory Research Step
Before performing any analysis, the agent **must**:
1. **Analyze App Store & Competitor Ads**: Use the links in `APP.md` to research the app's niche and competitors. Focus **purely on real, actual competitor ads currently running** (e.g., what headlines, creatives, ad copy they're actually using in Google Ads). Ignore theoretical/ASO strategies and only report verified, actionable intel on competitor UA tactics.
2. **Platform Research**: Use the platform name (inferred from the directory hierarchy: `[App Name]/[Platform Folder]/...`) to research latest confirmed trends and algo updates for that specific network (e.g., Google Ads UAC updates for 2026). Always verify against official platform documentation.

### Platform Inference
The platform being analyzed is determined by the directory name containing the report files (e.g., if files are in `Habitoria/Google Ads/`, the platform is **Google Ads**).

### Naming Convention Structure
The user uses the following structure for campaign naming:
`app_OS_source_geo_opt mode_attr window_date`

**Example Parser Logic**:
- `HB` = **App Name** (e.g., Habitoria)
- `AND` / `iOS` = **Operating System**
- `GA` / `FB` / `TikTok` = **Source**
- `US` / `HK` / `WW` = **GEO**
- `xCPE` / `tCPI` / `tROAS` = **Optimization Mode**
- `d7` / `d1` = **Attribution Window**
- `YY-MM-DD` = **Start/Creation Date**

---

## Data Persistence

### Why we need local history files
The Google Sheet may only contain recent data (e.g., last 30-60 days). **History files preserve ALL data indefinitely**, including:
- Campaigns that have scrolled off the Google Sheet
- Asset performance that is no longer visible
- GEO data from early phases
- **Active campaigns**: Always updated from Google Sheet (source of truth)
- **Inactive campaigns**: Preserved from history, never deleted

To preserve historical data AND maintain accuracy, the agent performs intelligent merging (not just append).

### Data flow
1. Agent reads `DATA_SOURCE.md`, `APP.md`, and any source-level `CAMPAIGN_NOTES.md` from the remote repo
2. Agent fetches latest data from Google Sheet tabs (via CSV URLs in `DATA_SOURCE.md`)
3. Agent merges new rows with existing `history.csv` in remote repo (deduplicating by key columns)
4. Agent commits updated `history.csv` back to remote repo
5. All analysis runs against the merged full history

### Deduplication keys
- **Campaign Performance**: `date` + `campaign_id`
- **Campaign GEO Performance**: `date` + `campaign_id` + `country_code`
- **Campaign Assets Performance**: `date` + `campaign_id` + `asset_name`

---

## 🎯 Analysis Readiness Checklist

**When a user requests analysis (e.g., "analyze Habitoria"), IMMEDIATELY display this checklist BEFORE proceeding:**

The agent must verify each of the following mandatory points. Display as a clean bulleted list with ✅ or ❌ status:

### Mandatory Requirements:

1. **✅ App Identified** 
   - Extract app name from request
   - Example: "Habitoria" recognized from "analyze Habitoria"

2. **✅ Remote Repository Accessible**
   - Confirm Git_Creds file is readable and contains a valid remote repo URL
   - Example: "✅ Git_Creds found: https://github.com/GresskiyK/Claude-Repo"

3. **✅ Project Folder Located in Remote Repo**
   - Confirm location of [AppName] project folder in the remote repository
   - Example: "✅ Habitoria folder found at UA Agent/Habitoria"

4. **✅ DATA_SOURCE.md Accessible**
   - Can read DATA_SOURCE.md with Google Sheet ID and tab names
   - Example: "✅ Found: Google Sheet ID 1wQgdYyeR-EPeD8..."

5. **✅ Google Sheet Access Verified**
   - Confirm access to live Google Sheet (can fetch Campaign Performance, Assets Performance, GEO Performance tabs)
   - Example: "✅ Sheet accessible, 3 tabs readable"

6. **✅ APP.md Available**
   - Can access app metadata (store links, category, monetization type)
   - Example: "✅ APP.md found: Habit tracking, Android-focused"

7. **✅ STRATEGY.md Available**
   - Can read current phase, goals, and roadmap
   - Example: "✅ STRATEGY.md found: Phase 3 (Monetization Focus)"

8. **✅ Competitor Research Ready**
   - App Store links accessible for competitor analysis
   - Example: "✅ Google Play Store link available: [habitoria-app-link]"

9. **✅ Analysis History Checked**
   - Searched for existing ANALYSIS_RESULTS.md in remote repo
   - Example: "⚠️ No previous analysis found — starting fresh" OR "✅ Previous analysis from Apr 15 found"

### Result Display:
After displaying all statuses, the agent **PAUSES AND WAITS** for user response:

**If all ✅**: 
```
📋 ANALYSIS READINESS CHECKLIST — Habitoria

✅ App Identified: Habitoria
✅ Remote Repo: https://github.com/GresskiyK/Claude-Repo
✅ Project Folder: UA Agent/Habitoria (in remote repo)
✅ DATA_SOURCE.md: Accessible
✅ Google Sheet: Verified (3 tabs, last updated Apr 17)
✅ APP.md: Found (Google Play link available)
✅ STRATEGY.md: Found (Phase 3 active)
✅ Competitor Data: Google Play accessible
⚠️ Previous Analysis: Not found (fresh start)

🟢 ALL SYSTEMS GREEN — Ready to proceed

⏸️ AWAITING CONFIRMATION: Do you approve? Reply with:
   • "proceed" / "go" / "yes" → Start analysis
   • "fix [item]" → Provide missing info
   • "cancel" → Abort
```

**If any ❌**:
```
📋 ANALYSIS READINESS CHECKLIST — Bumpy

✅ App Identified: Bumpy
❌ Remote Repo: Git_Creds not accessible or URL invalid
❌ Project Folder: NOT FOUND in remote repo
❌ DATA_SOURCE.md: Inaccessible
✅ APP.md: (pending folder access)
❌ STRATEGY.md: (pending folder access)
❌ Competitor Data: Cannot verify
⚠️ Previous Analysis: N/A

🔴 BLOCKED — 3 critical items missing

⏸️ AWAITING YOUR RESPONSE:
   • Please verify: Git_Creds file and remote repo URL
   • Or: Confirm the [AppName] project folder exists in the remote repo
   • Or: Provide the remote repo URL directly
```

**Agent Behavior - Full Loop**:
1. Display checklist with all statuses
2. **PAUSE AND WAIT** for user response
3. User provides: "fix [item]" with information
4. **RE-VERIFY THE ENTIRE CHECKLIST** (recheck all 9 items)
5. Display updated checklist with new statuses
6. **PAUSE AND WAIT** again
7. Repeat steps 3-6 until ALL items are ✅
8. Only when all items are 🟢 GREEN, ask for final "proceed" confirmation
9. Begin analysis

**Key Rule**: Never skip re-verification. After ANY user input to fix items, recheck everything before moving forward.

---

### Example Loop:

**User**: "analyze Habitoria"

**I display**:
```
📋 ANALYSIS READINESS CHECKLIST — Habitoria

✅ App Identified: Habitoria
❌ Remote Repo: Git_Creds not found or invalid
❌ Project Folder: PENDING (can't access without repo)
❌ DATA_SOURCE.md: PENDING
✅ APP.md: Pending repo access
❌ STRATEGY.md: Pending repo access
❌ Competitor Data: Pending
⚠️ Previous Analysis: N/A

🔴 BLOCKED — 1 critical item missing

⏸️ Please verify:
   • Git_Creds file exists at /mnt/project/Git_Creds
   • Remote repo URL is valid and accessible
```

**User**: "fix repo - verified Git_Creds has https://github.com/GresskiyK/Claude-Repo"

**I re-verify ALL items:**
```
✅ Reading Git_Creds file...
✅ Validating repo URL...
✅ Accessing remote repo...
✅ Checking for Habitoria project folder...
✅ Searching for DATA_SOURCE.md...
✅ Parsing Google Sheet ID from DATA_SOURCE.md...
✅ Testing Google Sheet access...
✅ Checking APP.md...
✅ Checking STRATEGY.md...
✅ Looking for competitor data sources...
✅ Checking for ANALYSIS_RESULTS.md...
```

**I display updated checklist:**
```
📋 ANALYSIS READINESS CHECKLIST — Habitoria (RE-VERIFIED)

✅ App Identified: Habitoria
✅ Remote Repo: https://github.com/GresskiyK/Claude-Repo
✅ Project Folder: UA Agent/Habitoria
✅ DATA_SOURCE.md: Accessible (Found)
✅ Google Sheet: Verified (1wQgdYyeR-EPeD8... - 3 tabs readable)
✅ APP.md: Found (Google Play: [habitoria-link])
✅ STRATEGY.md: Found (Phase 3 - Monetization)
✅ Competitor Data: Google Play accessible
⚠️ Previous Analysis: Not found (fresh start)

🟢 ALL SYSTEMS GREEN — Ready to proceed

⏸️ AWAITING FINAL CONFIRMATION:
   Reply with "proceed" or "go" to start analysis
```

**User**: "proceed"

**I start analysis immediately** ✅

---

## Analysis Routines

The agent performs analysis **on-demand** when the user updates the data source.

### Dynamic App Lookup
When a user requests analysis for an app (e.g., "analyze Bumpy"), the agent **MUST**:
1. **Extract app name** from the user's request
2. **Read Git_Creds** to get the remote repo URL dynamically
3. **Locate the [AppName] folder** in the remote repo (path: `UA Agent/[AppName]/`)
4. Once located, proceed with **Analysis Readiness Checklist** and data fetch steps below

**Note**: All project data is now stored in the remote repository (GitHub). The agent accesses files directly from the remote repo using the URL in Git_Creds, not from local PC paths. If you need to change the remote repo URL, simply update Git_Creds and the agent will use the new location automatically.

---

### Pre-Analysis Checkpoint: Review Previous Results
**Before starting any analysis**, the agent **MUST**:
1. Check if previous analysis results exist in the **remote [AppName] project folder** (look for `ANALYSIS_RESULTS.md`)
2. If found, **read the previous analysis** and note:
   - When it was conducted (date)
   - Key findings from that time
   - Recommendations made
   - Current status of those recommendations
3. **Compare context**: Note how the data has changed since the last analysis (new campaigns, asset fatigue, GEO shifts, etc.)
4. **Continuity note**: At the start of your new analysis, briefly reference what was observed last time and how the situation has evolved
5. If NOT found: **Note clearly**: "Unable to locate past analysis results — starting with no baseline data from previous analyses"

**Purpose**: Ensures analysis is continuous, not isolated; reveals trends and shows whether previous recommendations are working.

---

### 1. "performance analysis" / "latest updates"
**Purpose**: Comprehensive audit of current campaign health from multiple angles.

**Steps**:
0. **Review Previous Analysis** ⚡: Follow the **"Pre-Analysis Checkpoint"** above. Check for existing `ANALYSIS_RESULTS.md` file and summarize what was found last time.
1. **Data Prep** ⚡: Read `DATA_SOURCE.md`, `APP.md`, `STRATEGY.md`, any source-level `CAMPAIGN_NOTES.md` from remote repo, and fetch + merge latest data from all Google Sheet tabs.
2. **The Platform Angle**: Separate analysis by **OS (iOS vs Android)**.
   - Compare spend distribution and CPI efficiency across platforms.
   - Note: Never aggregate iOS and Android metrics unless specifically asked.
3. **The Value Angle**: If revenue/ROAS data is available:
   - Prioritize **ROAS** and **D7 Retention** over CPI.
   - Identify "Golden Cohorts" (low cost + high long-term value).
4. **The Auction Health Angle**: Analyze trends in **CPM** (is the market more expensive?) and **CVR** (is the creative/store conversion failing?).
5. **Flag Anomalies**:
   - CPI wow increase > 20%
   - CPM wow increase > 15% (Auction pressure)
   - CVR drop > 15% (Creative/Store issues)
6. **Top & Bottom Performers**: Rank using a weighted score of Scale (Spend) + Efficiency (ROAS/CPI).
7. **Deliver 3 actionable recommendations**.

**Step 8: Save Analysis Results** 💾
1. Create/overwrite the markdown file: `ANALYSIS_RESULTS.md` (same file each time)
2. Save it to the **[AppName] project folder in remote repo** (same level as `APP.md`, `DATA_SOURCE.md`, `STRATEGY.md`)
3. **File should contain**:
   - Analysis date and data cutoff date
   - Executive summary (top metrics, current status)
   - Key findings from this analysis
   - Previous analysis summary (brief reference to last findings for continuity)
   - Top 3 actionable recommendations
   - Any anomalies or alerts
4. Confirm save with user: "✅ Analysis results saved to remote repo: `UA Agent/[AppName]/ANALYSIS_RESULTS.md` (updated)"

---

### 2. "creative review" / "asset analysis"
**Purpose**: Identify winning/fatigued creatives and format gaps.

**Steps**:
1. **Review Previous Analysis** ⚡: Check for existing `ANALYSIS_RESULTS.md` file in remote repo and note what was found about asset performance last time.
2. **Asset Ranking**: Rank assets by CPI and ROAS (min 100 impressions).
3. **Creative Fatigue**: Identify assets with declining CTR/CVR over 2+ consecutive weeks.
4. **The Format Angle**: Analyze the **Format Mix** (Video vs Static vs HTML5).
   - Identify if the account is over-reliant on one format.
   - Audit video lengths and orientations (Vertical vs Horizontal).
5. **Recommendations**:
   - Assets to **Scale** (High volume, stable efficiency).
   - Assets to **Pause** (Fatigue or high CPI).
   - Creative **Gaps** (e.g., "Performance is good, but you have no Static assets running").

**Step 6: Save Analysis Results** 💾
1. Create/overwrite the markdown file: `ANALYSIS_RESULTS.md` in remote repo
2. Save it to the **[AppName] project folder**
3. **File should contain**:
   - Asset rankings (best/worst performers)
   - Fatigue alerts
   - Format analysis and gaps
   - Recommendations (scale/pause/create)
4. Confirm save with user: "✅ Creative analysis saved to remote repo: `UA Agent/[AppName]/ANALYSIS_RESULTS.md` (updated)"

---

### 3. "geo analysis" / "country review"
**Purpose**: Optimize geographic budget allocation and identify scaling opportunities.

**Steps**:
1. **Review Previous Analysis** ⚡: Check for existing `ANALYSIS_RESULTS.md` in remote repo and note what GEO recommendations were made last time.
2. **Efficiency Audit**: Rank countries by ROAS/CPI.
3. **The "Share" Angle**: Calculate each country's **Share of Spend** vs **Share of Installs/Value**.
   - Identify countries getting "too much" budget for their efficiency.
4. **Scaling Opportunities**: Find low-CPI countries with low spend share where the auction is less competitive.
5. **Budget Reallocation**: Provide specific % suggestions for shifting budget from inefficient to efficient GEOs.

**Step 6: Save Analysis Results** 💾
1. Create/overwrite the markdown file: `ANALYSIS_RESULTS.md` in remote repo
2. Save it to the **[AppName] project folder**
3. **File should contain**:
   - Country rankings by efficiency
   - Budget allocation analysis
   - Scaling opportunities
   - Specific budget reallocation recommendations (with % shifts)
4. Confirm save with user: "✅ GEO analysis saved to remote repo: `UA Agent/[AppName]/ANALYSIS_RESULTS.md` (updated)"

---

### 4. "full report"
**Purpose**: The most comprehensive audit, executed when major changes are needed.
**Steps**: Combines all 3 routines above into a prioritized strategic document.

**Final Step: Save Full Report** 💾
1. Create/overwrite the markdown file: `ANALYSIS_RESULTS.md` in remote repo
2. Save it to the **[AppName] project folder**
3. **File should contain**:
   - Complete performance analysis (sections 2-7 from "performance analysis" above)
   - Creative/asset analysis with recommendations
   - GEO analysis with budget allocation suggestions
   - Combined strategic roadmap (5-7 prioritized tasks)
   - Comparison with previous full report (what changed, what improved)
4. Confirm save with user: "✅ Full report saved to remote repo: `UA Agent/[AppName]/ANALYSIS_RESULTS.md` (updated)"

---

## Reporting Format

When delivering analysis, use this structure:
1. **📊 Summary** — Top-line metrics (Spend, Installs, ROAS). Briefly summarize the current activity state (e.g., "Currently, we have 1 active campaign with xCPE optimization in the US"). Ensure you analyze and present data for each Ad Source completely separately. Do not mix them into a general average.
2. **📈 Holistic Metrics** — Do not just report CPI. Explain the *broader picture* by connecting metrics together (e.g., how **CPM** auction costs, **CTR** creative interest, and **CVR** funnel efficiency are currently driving the CPI). Show how they depend on each other.
3. **🗺️ Niche & Category Context** — Insights from actual competitor research. **Report only verified, real competitor ads and UA tactics.** Focus on what competitors are actually running (headlines, creatives, ad copy, ad formats) observed in Google Ads or other platforms. Do not provide ASO suggestions. Highlight competitor ad strategies and where your app's current ads stand in comparison.
4. **🏆 Creative & GEO Winners** — Best performing assets and markets.
5. **🚨 Strategic Gaps & Testing** — Missing formats, platform imbalances, or fatigue alerts. Always propose a **Testing Plan** for new setups (e.g., trying a different proxy event if current one is too deep, `d0` vs `d7` windows). *Note: While recommendations should generally align with the current phase's goal in `STRATEGY.md`, if you observe that nothing is currently active, a string of past campaigns failed, or past setups were tested incorrectly, proactively analyze those historical failures. Propose a completely new strategy, combination of variables, or setup to test next.*
6. **⚖️ Cross-Source Comparison** — Briefly compare the active ad sources head-to-head (e.g., "Google is currently outperforming Meta because..."). Provide clear, source-level verdicts.
7. **💡 Actionable Roadmap** — 3 to 5 prioritized tasks for the UA Manager.

---

## Visualization Strategy

**Always include multiple visualization types** when delivering analysis. Charts reveal patterns that prose alone cannot convey. Use different visualization types for different insights:

### Recommended Chart Types

1. **Bar Charts** — Phase comparisons, CPI/CPM by campaign, efficiency rankings
   - Use when comparing discrete categories (Phase 1 vs Phase 2 vs Phase 3)
   - Shows relative performance at a glance

2. **Line Charts** — Trends over time, daily CPI evolution, moving averages
   - Use for campaigns running 7+ days to reveal trend direction
   - Shows momentum, stabilization, or deterioration

3. **Pie/Donut Charts** — Budget allocation, spend distribution by source/campaign
   - Use to show "share of spend" and visual proportions
   - Makes it clear which campaigns consume most budget

4. **Combination Charts** — CTR + CPI over time, installs vs spend trend
   - Use to show relationship between two metrics across time
   - Reveals correlation (e.g., "as CTR drops, CPI rises")

5. **Heatmaps** — Daily performance grids, geo-by-campaign matrices
   - Use for large datasets (30+ data points) that need pattern recognition
   - Hot/cold coloring instantly reveals anomalies

### Visualization Best Practices

- **Dashboard Layout**: Start with summary metrics (spend, installs, CPI), then present 3-5 charts
- **Chart Density**: Each chart should answer ONE specific question. Don't overcrowd.
- **Interactivity**: Include metrics cards above charts (total spend, active campaigns, etc.)
- **Color Coding**: Use red for underperforming phases/regions, blue for healthy performers
- **Annotation**: Label anomalies directly on charts (e.g., "HK launch dip" on Day 1)
- **Trend Lines**: On line charts, include a moving average to smooth daily volatility
- **Context in Text**: Prose explains WHY the pattern exists; charts show THAT the pattern exists

### When NOT to Use Charts

- Single data points (one campaign, one day) — use a metric card instead
- Simple yes/no answers — use text
- Very small datasets (< 3 data points) — use a table

---

## Important Notes

- **Currency**: All monetary values are in USD unless stated otherwise.
- **Timezone**: Data dates are primarily in UTC+2. Check for discrepancies between platforms.
- **Data Freshness** ⚡: **ALWAYS fetch latest data before any analysis.** Google Sheet is the source of truth. Verify data access through the Analysis Readiness Checklist — never assume data hasn't changed since the last session.
- **On-Demand**: Analysis only happens when requested. Always ingest all new data first.
- **Active vs. Inactive**:
  - **Active**: Any campaign with spend in the last 3 days. Focus all primary alerts/anomalies here.
  - **Inactive**: No spend for the last 3 days. Exclude from current analysis alerts, but **always** use them to determine what failed or was tested incorrectly. If nothing is working or active, check what is best to combine from past performance and propose a new setup.
- **Evaluate All Data**: Be cautious but thorough even with low-spend items; look for early signals in new campaigns or creatives.
- **Fact-Checking Mandate**: Whenever addressing a question that requires external knowledge or research (e.g., verifying how an ad platform or SDK behaves), **always** perform a web search to verify against official documentation and clearly state the official source in the response. Do not rely exclusively on internal knowledge.
- **Always show your math**: When making recommendations, show the data that supports them.
- **Ask before acting**: If data looks unusual, confirm with the user before overwriting history.
- **Take Your Time**: There is no rush. Always pause, look at the data holistically, explicitly connect different metric correlations in your "scratchpad/thought process", and deliver deep, considered analysis rather than surface-level fast answers.
