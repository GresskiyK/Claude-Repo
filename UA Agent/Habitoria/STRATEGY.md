# Habitoria — UA Strategy

## Project Stage
We have just started our paid marketing efforts for Habitoria. 

## Strategic Roadmap

### Phase 1: Mid-Funnel Volume (March 2026)
- **Campaign**: `HB_AND_GA_US_xCPE_d7_26-03-16`
- **Goal**: Target `habit_toggle_today` event.
- **Logic**: Users who download and create at least one habit.
- **Result**: Successful volume and good CPI. Established a baseline for user resonance.

### Phase 2: Regional Testing (March 2026)
- **Campaign**: `HB_AND_GA_HK_xCPE_d7_26-03-26`
- **Goal**: Test the same US setup in Hong Kong (HK).
- **Result**: **Unsuccessful**. Market did not resonate or scale efficiently compared to the US.

### Phase 3: Monetization Focus (Current - April 2026)
- **Campaign**: `HB_AND_GA_US_xCPE_d7_26-04-10`
- **See**: [CAMPAIGN_NOTES.md](Google%20Ads/CAMPAIGN_NOTES.md) for optimization context, tracking details, and campaign operational setup
- **Goal**: Target **Firebase In-App Events**. Note: This Firebase event currently tracks both "Purchase" and "Start Trial", but the "Start Trial" does not contain a revenue value yet. Do not mistakenly suggest using "Start Trial" as a fallback proxy event, as it is already being targeted.
- **Logic**: It's time to shift from volume to literal revenue.
- **Observation**: Because this event is much deeper in the funnel (lower conversion rate), we expect much lower conversion volume (and many days of 0) compared to Phase 1. 

## Monetization Model
- Users can use the app for free.
- Premium features are unlocked via subscriptions (Weekly / Monthly / Annual).
- Current goal is to reach those who are willing to pay.
