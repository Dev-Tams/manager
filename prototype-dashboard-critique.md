# Pulse Prototype Critique

This critique treats the current app as a valid prototype, not a finished product. The visual direction is clear: Pulse is trying to be a bank-connected personal finance assistant with budgeting, subscriptions, persona insights, and Wema recommendations. The main issue is that several screens show the right concepts but do not yet prove the product behavior strongly enough.

## High-Level Read

The prototype currently communicates the idea of open banking aggregation, AI insight, spending persona, subscription detection, and Wema cross-sell. That is a good base.

The weak point is interactivity. A reviewer can see static cards, but they cannot yet click through enough cause-and-effect moments to believe the assistant is using real financial context. The next version should make the prototype feel more diagnostic: when the user taps a bank, category, subscription, or persona trait, the app should reveal specific evidence and a next action.

## Dashboard

Current state:

- The dashboard shows a total balance across Wema, GTBank, and Kuda.
- It lists income, spent, and saved.
- The bank names are shown as text under the total balance, but they are not actionable.

Critique:

The dashboard is too aggregated. If the product is about open banking, the user should be able to inspect each linked bank. Right now, "Total balance" proves aggregation, but it does not prove transparency.

Recommended prototype behavior:

- Make each bank clickable from the dashboard balance area.
- Tapping `Wema`, `GTBank`, or `Kuda` should switch the balance view to that bank.
- The selected bank should show:
  - Bank balance
  - Recent inflows and outflows
  - Active subscriptions charged from that bank
  - Budget categories most affected by that bank
- Include an `All banks` state so users can return to the combined view.

Example:

- All banks: `₦1,247,500`
- Wema: `₦620,000`, salary inflow, savings recommendation
- GTBank: `₦410,500`, Netflix paid here, food spending detected
- Kuda: `₦217,000`, Bolt and food delivery spend detected

This would make the open banking claim more believable.

## AI Insight

Current state:

- The overview already says: "You're on track to exceed your food budget by ₦15,000 this month."

Critique:

This is the right kind of insight, but it should feel more urgent and explain why. The current statement is good, but it reads like a static warning. A stronger prototype would show a red flag state and a simple projection.

Recommended prototype behavior:

- Use a warning treatment when budget risk is high.
- Show the mistake clearly: spending pace is too high compared to budget and days left.
- Include a recommended correction.

Example copy:

> Red flag: Food spending is at ₦85,000 of your ₦100,000 budget with 12 days left. If you continue at this pace, you may end the month around ₦115,000, which is ₦15,000 over budget.

Suggested action:

> Reduce food delivery by ₦1,250 per day or move ₦15,000 from flexible shopping budget.

This makes the AI feel useful because it identifies the mistake, explains the forecast, and gives a next step.

## Overview

Current state:

- Overview contains the AI insight, spent-this-month card, and persona card.
- Recommendations are mainly on the separate Offers screen.

Critique:

The overview should be the user’s financial command center. It needs one basic recommendation immediately visible, not only after navigating to Offers.

Recommended prototype behavior:

- Add a small recommendation section below the overview stats.
- Keep it focused on one saving option.
- Make it actionable but not overwhelming.

Example:

> Recommended saving option  
> Move ₦50,000 to Wema Fixed Savings after salary day. Your current spending pattern still leaves enough buffer for bills.

Possible action:

- `Start saving`
- `View calculation`

This connects insight to Wema value without making the dashboard feel like an ad.

## Budget Layer

Current state:

- Budget exists as a tab.
- It lists Food & Dining, Transport, and Entertainment with usage percentages.

Critique:

The budget section is too shallow for the importance of the product. Budgeting should have a dedicated layer with set-budget, observe-spending, and drill-down interactions. Right now it only shows progress rows.

Recommended prototype behavior:

- Keep the Budget tab, but give it a dedicated section structure:
  - Monthly budget summary
  - Category breakdown
  - Set or edit budget
  - Spending trend
  - Transactions causing pressure
- Add an interactive chart, either pie, donut, or bar chart.
- When the user taps a category, populate the chart and transaction list for that category.

Example interaction:

- Tap `Food & Dining`
- Chart updates to show food spending split:
  - Restaurants
  - Food delivery
  - Groceries
  - Snacks
- Below the chart, show the transactions causing the overspend.
- Include a `Set budget` or `Edit budget` action.

Budget-setting flow to prototype:

- User taps `Set budget`
- User enters or adjusts amount
- App shows projected month-end result
- App confirms: "Food budget set to ₦100,000"

This would let reviewers understand both sides of budgeting: planning and monitoring.

## Subscriptions

Current state:

- Active subscriptions show Netflix and Spotify.
- Inactive subscriptions show Showmax and iCloud+.
- Netflix includes "Cancel from GTBank recurring payments"; Spotify includes "Cancel from Apple App Store subscriptions."

Critique:

The subscriptions section has useful content, but it needs stronger interaction. Subscriptions should be clickable, filterable, and tied to the bank account paying them.

Recommended prototype behavior:

- Make each subscription row clickable.
- Show a subscription detail view or expanded state.
- Include:
  - Amount
  - Billing cycle
  - Next charge date
  - Bank/payment source
  - Last charged date
  - Cancel path
  - Similar or duplicate services
- Add filters:
  - Active
  - Inactive
  - Paid from Wema
  - Paid from GTBank
  - Paid from Kuda
  - Highest cost
  - Due soon

Example subscription detail:

> Netflix  
> ₦4,200 monthly  
> Paid from GTBank  
> Next charge: May 28  
> Last charge: Apr 28  
> Cancel from GTBank recurring payments

The cancel action does not need to actually cancel in the prototype, but it should show a confirmation state:

> Cancellation guide opened. We will remind you before the next charge.

This proves the product is not just detecting subscriptions but helping users act.

## Persona

Current state:

- Persona shows "The Steady Builder."
- It includes scores for savings discipline, spending control, bill punctuality, and subscription efficiency.
- It has pattern and credit-signal insights.

Critique:

The persona is visually strong, but the trait cards need to be clickable. A persona score should explain itself with evidence and a recommendation. Without that, it risks feeling decorative.

Recommended prototype behavior:

- Make each trait clickable.
- Tapping `Savings discipline`, `Spending control`, `Bill punctuality`, or `Sub efficiency` should show:
  - Why the score is high or low
  - Which transactions or habits influenced it
  - One recommended action
  - One Wema-linked option where relevant

Example:

> Spending control: 54  
> You used more on Bolt this month than your normal transport pattern. Consider setting a car savings target with Wema.

Possible recommendation:

> Save ₦40,000 monthly toward a car fund with Wema Target Savings.

This turns persona from a label into a coaching layer.

## Product Logic To Make More Viable

The app should make a clear data chain:

1. The user connects multiple banks.
2. Pulse aggregates balances and transactions.
3. Pulse detects spending patterns and subscriptions.
4. Pulse flags budget risk.
5. Pulse recommends a specific saving, investment, or cancellation action.
6. The user can inspect the evidence by bank, category, subscription, or persona trait.

That chain is the prototype’s core story. Every major screen should reinforce it.

## Specific Prototype Improvements

- Add clickable bank chips under total balance.
- Add per-bank balance states.
- Make the AI insight red-flag budget mistakes with projection logic.
- Add one recommendation directly on Overview.
- Expand Budget into a fuller section with chart, category drill-down, and budget-setting.
- Make budget categories clickable.
- Make subscriptions clickable.
- Add subscription filters.
- Show which bank each subscription is paid from.
- Add a cancel flow or cancellation guidance state.
- Make persona trait cards clickable.
- Add persona-specific financial coaching, especially around savings discipline and overspending patterns.
- Tie recommendations to Wema only where the user behavior justifies it.

## Critique Of Current Prototype Direction

The current prototype looks polished enough to present, but it behaves more like a concept deck than a usable financial tool. The UI has the right screens, but the prototype needs more "tap and reveal" moments.

The strongest parts are:

- Clear Wema/Pulse positioning
- Smooth onboarding idea
- Open banking setup
- Persona concept
- Budget warning concept
- Subscription detection concept

The weakest parts are:

- Bank balances are not inspectable
- Budgeting is not yet interactive enough
- Recommendations are separated from the overview
- Subscriptions do not show enough payment-source detail
- Persona scores do not explain themselves
- The AI insight does not yet show evidence or consequences

For the next prototype pass, the priority should not be adding more screens. It should be making the existing screens respond to taps in ways that prove the product intelligence.

