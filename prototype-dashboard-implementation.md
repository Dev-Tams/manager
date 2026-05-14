# Pulse Dashboard Prototype Implementation Plan

This plan translates `prototype-dashboard-critique.md` into build steps for the next prototype pass. The goal is not backend integration. The goal is to make the static prototype behave like a believable finance assistant through local data, clickable states, and clear cause-and-effect interactions.

## Implementation Scope

Primary file:

- `home.html`

Supporting files:

- No new framework required.
- No build system required.
- Keep the prototype as a self-contained HTML/CSS/JS demo unless asset needs change later.

Core outcome:

- Users can click banks, budget categories, subscriptions, and persona traits.
- Each click reveals specific financial evidence and a recommended action.
- The prototype communicates aggregation, diagnosis, and action.

## Guiding Product Story

The implementation should reinforce this flow:

1. User connects multiple banks.
2. Dashboard aggregates balances and spending.
3. User can inspect each bank separately.
4. AI flags a budget mistake with projected consequence.
5. Budget layer lets user inspect and adjust spending limits.
6. Subscriptions can be filtered, inspected, and prepared for cancellation.
7. Persona traits explain financial behavior and recommend Wema-linked actions where justified.

## Phase 1: Shared Demo Data

Create a small local data model in the existing `<script>` block.

Suggested structures:

```js
const banks = {
  all: {
    label: 'All banks',
    balance: '₦1,247,500',
    income: '₦520,000',
    spent: '₦311,240',
    saved: '40.1%',
    subtitle: 'Wema · GTBank · Kuda · via Open Banking'
  },
  wema: {
    label: 'Wema',
    balance: '₦620,000',
    income: '₦520,000',
    spent: '₦86,000',
    saved: '48%',
    subtitle: 'Salary, savings, and Wema offers'
  },
  gtbank: {
    label: 'GTBank',
    balance: '₦410,500',
    income: '₦0',
    spent: '₦143,200',
    saved: '22%',
    subtitle: 'Netflix, food, and recurring payments'
  },
  kuda: {
    label: 'Kuda',
    balance: '₦217,000',
    income: '₦0',
    spent: '₦82,040',
    saved: '18%',
    subtitle: 'Bolt, food delivery, and daily spending'
  }
};
```

Also create arrays for:

- `budgetCategories`
- `subscriptions`
- `personaTraits`
- `bankActivity`

Keep this data near the bottom of `home.html` so the prototype remains easy to edit.

## Phase 2: Dashboard Bank Drill-Down

Current dashboard balance area should become interactive.

UI changes:

- Replace or supplement the static bank subtitle with bank filter chips:
  - `All`
  - `Wema`
  - `GTBank`
  - `Kuda`
- Add a small "Bank activity" card below the balance or in Overview.
- Show selected bank state visually.

JS behavior:

- Add `selectBank(bankId)`.
- Update:
  - Balance label
  - Balance amount
  - Subtitle
  - Income
  - Spent
  - Saved
  - Bank activity card
  - Any relevant subscription/budget hints

Acceptance check:

- Clicking `GTBank` changes the balance to GTBank-only values.
- Clicking `All` restores total values.
- A reviewer can tell which bank is currently selected.

## Phase 3: Stronger AI Red Flag On Overview

Current AI insight should become a more explicit warning.

UI changes:

- Add a red or amber risk treatment for the AI insight.
- Include:
  - Risk label
  - Current spend
  - Budget limit
  - Days left
  - Projected overspend
  - Suggested correction

Suggested copy:

```text
Red flag: Food spending is at ₦85,000 of your ₦100,000 budget with 12 days left.
If you continue like this, you may end around ₦115,000, which is ₦15,000 over budget.
```

Suggested action text:

```text
Reduce food delivery by ₦1,250/day or move ₦15,000 from flexible shopping.
```

Acceptance check:

- The overview immediately communicates a budget mistake and consequence.
- The warning feels like a diagnosis, not a generic tip.

## Phase 4: Overview Recommendation

Add a basic recommendation card below the overview stats.

UI content:

- Title: `Recommended saving option`
- Recommendation: `Move ₦50,000 to Wema Fixed Savings after salary day.`
- Reason: `Your salary pattern and current bills leave enough buffer.`
- Actions:
  - `Start saving`
  - `View calculation`

Prototype behavior:

- `Start saving` can change the card state to `Savings plan drafted`.
- `View calculation` can expand a small explanation.

Acceptance check:

- The overview has one clear next step.
- The recommendation is tied to observed behavior, not just product promotion.

## Phase 5: Dedicated Budget Layer

Upgrade the Budget tab from static rows to a fuller budgeting workspace.

Sections to add:

- Monthly summary
- Interactive category list
- Chart area
- Category evidence
- Set/edit budget control

Recommended UI structure:

```text
Monthly Budget
₦129,000 / ₦165,000 used

[Donut or segmented bar chart]

Food & Dining    ₦85,000 / ₦100,000    85%
Transport        ₦25,000 / ₦40,000     62%
Entertainment    ₦19,000 / ₦25,000     76%

Selected: Food & Dining
Restaurants: ₦42,000
Food delivery: ₦28,000
Groceries: ₦15,000

[Edit Budget]
```

JS behavior:

- Add `selectBudgetCategory(categoryId)`.
- Update chart values.
- Update selected category detail.
- Update transaction evidence.
- Add `editBudget(categoryId)` or a lightweight modal/inline editor.

Budget-setting behavior:

- User taps `Edit Budget`.
- Inline control appears with current budget amount.
- User can choose a preset amount:
  - `₦80k`
  - `₦100k`
  - `₦120k`
- App updates the displayed budget and projection text.

Acceptance check:

- Clicking `Food & Dining` changes the chart/details.
- Clicking `Transport` changes the chart/details.
- Editing a budget visibly updates the selected category.

## Phase 6: Subscription Interaction

Make subscriptions clickable and filterable.

UI changes:

- Add filter chips:
  - `All`
  - `Active`
  - `Inactive`
  - `Wema`
  - `GTBank`
  - `Kuda`
  - `Due soon`
- Each subscription row should show payment source:
  - `Paid from GTBank`
  - `Paid from Wema`
  - `Paid from Kuda`
- Add selected subscription detail panel.

Subscription detail should include:

- Name
- Amount
- Billing cycle
- Bank/payment source
- Last charge date
- Next charge date
- Cancel path
- Related duplicate or saving note

JS behavior:

- Add `filterSubscriptions(filterId)`.
- Add `selectSubscription(subscriptionId)`.
- Add `startCancelSubscription(subscriptionId)`.

Cancel prototype behavior:

- Button label: `Cancel guidance`
- On click, detail panel changes to:
  - `Cancellation guide opened`
  - `We will remind you before the next charge.`

Acceptance check:

- Filter chips change visible subscription rows.
- Clicking Netflix opens Netflix details.
- Details show the bank the subscription is paid from.
- Cancel guidance changes state without pretending to perform a real cancellation.

## Phase 7: Persona Trait Drill-Down

Make persona traits clickable.

UI changes:

- Add selected state to trait cards.
- Add a detail card below the trait grid.
- Detail card should explain:
  - Score reason
  - Evidence
  - Recommended action
  - Wema option where relevant

Suggested trait examples:

```text
Savings discipline
You save consistently after salary day. Keep ₦50,000 automated into Wema Fixed Savings.
```

```text
Spending control
You used more on Bolt this month than your normal transport pattern. Save ₦40,000 monthly toward a car fund with Wema Target Savings.
```

```text
Sub efficiency
Netflix and DStv overlap. Cancelling one could save ₦117,600/year.
```

JS behavior:

- Add `selectTrait(traitId)`.
- Update trait detail card.
- Optional: add `Start plan` button that routes to Offers or changes the detail state.

Acceptance check:

- Clicking `Spending control` shows the Bolt/car savings recommendation.
- Clicking `Sub efficiency` shows duplicate subscription logic.
- Trait scores no longer feel decorative.

## Phase 8: Small Interaction Polish

Add enough polish to make states feel intentional.

Recommended polish:

- Active chips for selected bank/filter/category/trait.
- Hover and tap states for clickable rows.
- Avoid hidden interactive elements that do not visibly respond.
- Keep all cards within the 390px mobile frame.
- Keep copy short so it does not overflow.
- Use the existing visual style and spacing system.

Do not add:

- Backend calls
- Real cancellation behavior
- Authentication changes
- New pages unless the existing tab/detail pattern becomes too cramped

## Implementation Order

Recommended build sequence:

1. Add shared demo data.
2. Implement bank chips and selected bank balance updates.
3. Upgrade AI red-flag card.
4. Add overview recommendation card.
5. Rebuild Budget tab with category drill-down and edit budget behavior.
6. Rebuild Subscriptions tab with filters and details.
7. Add Persona trait drill-down.
8. Test all navigation and clickable states manually.

This order keeps the dashboard story working early, then deepens each major product layer.

## Manual Test Checklist

Dashboard:

- `All`, `Wema`, `GTBank`, and `Kuda` chips update balances.
- Selected bank chip is visually clear.
- Bank activity changes with selected bank.

Overview:

- AI insight reads as a warning.
- Recommendation card appears below stats.
- Recommendation action changes or expands state.

Budget:

- Category click updates chart/detail.
- Budget edit control updates values.
- Overspend projection remains visible.

Subscriptions:

- Filters work.
- Subscription rows are clickable.
- Detail panel shows payment source.
- Cancel guidance state appears.

Persona:

- Trait cards are clickable.
- Trait detail changes per trait.
- Spending control includes Bolt/car savings recommendation.

General:

- No console errors.
- Bottom navigation still works.
- Tabs still switch correctly.
- Content remains readable inside the mobile frame.

## Definition Of Done

The implementation is done when a reviewer can complete this prototype story:

1. Open Pulse and reach Dashboard.
2. Tap GTBank and see GTBank-specific balance/activity.
3. See an AI red flag explaining why the food budget will be exceeded.
4. View one saving recommendation on Overview.
5. Open Budget, tap Food, inspect chart/details, and adjust the budget.
6. Open Subscriptions, filter by GTBank, open Netflix, and view cancel guidance.
7. Open Persona, tap Spending Control, and see a Bolt-to-car-savings recommendation.

If those seven moments work, the prototype will feel materially more viable.

