# UK Personal Finance Flowchart Tool — Checkpoint-by-Checkpoint Calculation Spec

## 1. Purpose

This document defines an implementation-ready calculation and insight layer for an interactive website based on the UK Personal Finance Flowchart.

The goal is **not** to replace the flowchart with a giant calculator. The goal is to preserve the original sequencing and decision logic while making each checkpoint more useful through:

- small but meaningful calculations,
- plain-English interpretation,
- progress visibility from step to step,
- and a richer sense of momentum, trade-offs, and urgency.

The product should feel like:

- a **guided financial journey**,
- a **decision support tool**,
- and a **progressive educational experience**.

It should **not** feel like:

- a tax return,
- a regulated advice engine,
- or a generic budgeting checklist.

---

## 2. Core Product Principles

### 2.1 Faithful Backbone
The original flowchart remains the backbone. The website should preserve:

- the sequence of steps,
- the major branch points,
- the early focus on stability before optimisation,
- the distinction between starter and full emergency funds,
- the separate treatment of mortgage and student loans,
- and the split between money needed before and after pension access age.

### 2.2 Insight at Every Checkpoint
Each checkpoint should answer three questions for the user:

1. **Where am I right now?**
2. **Why does this step matter?**
3. **What specifically should I do next?**

### 2.3 Progressive Disclosure
The tool should support three usage modes so users can choose how much detail to provide.

### 2.4 Numerical Momentum
The user should see that they are progressing numerically, not just ticking boxes. Each step should reveal:

- a measurable baseline,
- a target or threshold,
- a gap,
- and a next action.

### 2.5 Human-Centred Tone
The experience should be calm, practical, non-judgmental, and clear. It should explain why a step matters without making the user feel behind or financially incompetent.

---

## 3. The Three Modes

## 3.1 Quick Mode
### Purpose
For users who want a fast route through the flowchart with minimal input.

### Input burden
Low.

### Behaviour
- Ask only the core branching questions.
- Use broad categories rather than precise numbers where possible.
- Show directional insight, not detailed modelling.

### Example inputs
- "Do you currently have cash savings?"
- "Are you using debt for essentials?"
- "Do you have high-interest debt?"
- "Are you contributing enough to get full employer pension match?"

### Output style
- High-level diagnostic labels
- Simple next-step actions
- Limited calculations

### Best for
- first-time visitors,
- financially stressed users,
- people who do not know their numbers.

---

## 3.2 Guided Mode
### Purpose
This should be the default experience.

### Input burden
Moderate.

### Behaviour
- Ask enough numeric information to create meaningful insights at each checkpoint.
- Use lightweight calculations to quantify stability, gaps, and priorities.
- Show contextual explanations and next actions.

### Example inputs
- monthly take-home income,
- monthly essential spending,
- accessible savings,
- debt balances/APRs/minimum payments,
- pension contribution and employer match details,
- goal amounts and target dates.

### Output style
- Insight cards
- Progress bars
- Gap-to-target numbers
- Priority recommendations

### Best for
- most users,
- anyone who wants actionable insight without full modelling.

---

## 3.3 Deep Mode
### Purpose
For users who want richer modelling, trade-off analysis, and a more complete financial picture.

### Input burden
Higher.

### Behaviour
- Ask for more granular breakdowns.
- Add sensitivity analysis and scenario testing.
- Compare alternative uses of surplus cash.

### Example additional inputs
- variable income patterns,
- dependants,
- job security,
- tax band,
- ISA usage,
- student loan plan,
- mortgage rate,
- expected property purchase timing,
- target retirement age.

### Output style
- Scenario cards
- Comparison tables
- Time-to-target modelling
- Wrapper suitability insights

### Best for
- financially engaged users,
- planners,
- people trying to optimise rather than simply stabilise.

---

## 4. Progression Model

The tool should make progression visible across the whole journey.

## 4.1 Progress Architecture
There are three progress layers:

### A. Step Progress
Shows which flowchart step the user is currently on.

Example:
- Step 1: Budget & stability
- Step 2: Starter emergency fund
- Step 3: Pension match
- Step 4: Costly debt / bad debt
- Step 5: Full emergency fund
- Step 6: Goals
- Step 7: Short-term savings
- Step 8: Long-term investing

### B. Financial Readiness Scoreboard
Shows the user’s current status across major pillars. This should update after each checkpoint.

Suggested pillars:
- Cash flow stability
- Crisis risk
- Starter buffer
- Full emergency buffer
- Pension capture
- Debt drag
- Goal clarity
- Short-term readiness
- Long-term readiness

Each pillar can use a status scale such as:
- Critical
- Needs attention
- In progress
- Strong

### C. Numerical Journey Trail
A persistent strip or expandable panel showing the most important numbers gathered so far.

Suggested entries:
- Monthly surplus/deficit
- Emergency fund months
- Highest debt APR
- Monthly debt interest leakage
- Employer pension match captured or missed
- Number of goals defined
- Short-term goal funding gap
- Long-term pots identified (before vs after pension age)

This makes the journey feel cumulative.

---

## 4.2 Completion States
Each checkpoint should end in one of four states:

- **Blocked** — user must address this before continuing in spirit, even if they can still explore later steps.
- **Priority** — important current focus.
- **Stable enough** — user can proceed.
- **Optimisation** — user has moved beyond core stability.

The tool should not necessarily hard-stop exploration, but it must make true priorities visually clear.

---

## 5. Canonical Data Model

## 5.1 Shared Core Inputs
These fields are used across modes, though some may be optional in Quick Mode.

### User profile
- age
- employment status
- household type
- dependants count
- tax band (optional in Guided, stronger in Deep)
- pension access age estimate

### Income
- monthly take-home pay
- monthly gross pay (optional)
- variable income flag
- other regular income

### Spending
- monthly essential spending
- monthly total spending
- monthly discretionary spending (derived if not directly entered)
- priority bills in arrears flag

### Savings
- accessible cash savings
- earmarked short-term savings
- separate emergency fund pot flag/value

### Debts
For each debt:
- debt type
- balance
- APR
- minimum monthly payment
- secured/unsecured flag
- mortgage flag
- student loan flag
- currently in arrears flag

### Pension
- workplace pension available flag
- enrolled flag
- employee contribution rate or amount
- employer contribution rate or amount
- max employer match available

### Goals
For each goal:
- goal name
- target amount
- target date
- goal category
- whether flexible or fixed
- access timing (before pension age / after pension age / unknown)
- first-home flag

### Optional deeper fields
- mortgage rate
- mortgage balance
- student loan plan type
- property purchase price estimate
- ISA allowance used
- savings interest rate
- intended retirement age

---

## 5.2 Derived Core Metrics
These should be recalculated after every relevant input change.

- monthly_surplus = monthly_take_home_income - monthly_total_spending
- essentials_gap = monthly_take_home_income - monthly_essential_spending
- debt_minimum_total = sum(minimum_payments)
- debt_interest_monthly_estimate = sum(balance * APR / 12)
- starter_emergency_months = accessible_cash_savings / monthly_essential_spending
- full_emergency_months = same metric, but compared against higher target band
- highest_non_mortgage_apr = max(APR of non-mortgage, non-student-loan debts)
- weighted_average_debt_apr
- employer_match_gap
- short_term_goal_required_monthly
- short_term_goal_total_gap
- long_term_before_pension_target
- long_term_after_pension_target
- goals_on_track_flag

Where required, calculations should handle missing or partial inputs gracefully.

---

## 6. Cross-Cutting UI Patterns

Every checkpoint should have the same structural layout.

## 6.1 Checkpoint Layout
1. **Checkpoint title**
2. **Why this matters**
3. **Inputs**
4. **Your numbers**
5. **Insight interpretation**
6. **What good looks like**
7. **Recommended next action**
8. **Progress update**

---

## 6.2 Insight Card Types
Each checkpoint may use one or more of these card types.

### Status card
Explains current condition.
Example: "You are currently running a monthly deficit of £185."

### Gap card
Shows distance to target.
Example: "Your starter emergency fund gap is £1,420."

### Opportunity card
Shows missed value or upside.
Example: "You may be missing £95/month of employer pension contributions."

### Urgency card
Shows why a step matters now.
Example: "Your 19.9% debt is likely more urgent than increasing investments."

### Trade-off card
Shows competing priorities.
Example: "Mortgage overpayments improve guaranteed return but reduce liquidity."

### Progress card
Shows change since the start or prior checkpoint.
Example: "You have now defined 3 goals and classified 2 as short-term."

---

## 6.3 Progress Display Rules
After each checkpoint, the tool should update:

- current step,
- readiness scoreboard,
- numerical journey trail,
- and a small message such as:
  - "You’ve stabilised the foundations. Next: build your starter buffer."
  - "You’ve captured pension match. Next: clear expensive debt."

---

## 7. Checkpoint-by-Checkpoint Calculation Spec

# Checkpoint 0 — Welcome, Mode Selection, and Journey Setup

## Purpose
Set expectations, choose interaction depth, and explain that the tool follows the flowchart while adding insight.

## Inputs
### Quick
- mode selection only

### Guided
- mode selection
- optional age
- optional employment status

### Deep
- mode selection
- age
- employment status
- household type
- dependants

## Calculations
None beyond initial setup.

## Outputs
- Explain the three modes.
- Show estimated completion time.
- Explain that the user can move through steps and refine numbers later.
- Initialise readiness scoreboard to "unknown".

## Progression effect
Create a visible journey header with all upcoming steps.

---

# Checkpoint 1 — Budget and Basic Stability

## Purpose
Establish whether the user has enough cash flow to support basic living costs before optimisation.

## Inputs
### Quick
- Do you know roughly whether you spend less than you bring in each month? (yes / no / unsure)
- Are any priority bills in arrears? (yes / no)

### Guided
- monthly take-home income
- monthly essential spending
- monthly total spending
- priority bills in arrears flag

### Deep
All Guided inputs plus:
- income volatility flag
- irregular major expenses estimate
- category breakdown of spending

## Calculations
### Guided / Deep
- monthly_surplus = income - total_spending
- essentials_surplus = income - essential_spending
- essential_spend_ratio = essential_spending / income
- discretionary_spend = total_spending - essential_spending

### Deep extras
- adjusted_monthly_surplus after smoothing irregular expenses
- spending concentration by category

## Insight logic
### Critical
- monthly_surplus < 0
- or priority bills in arrears

### Needs attention
- monthly_surplus is close to zero
- essential_spend_ratio very high

### Stable enough
- user has positive surplus and priority bills are current

## Output cards
### Status card
- "Your monthly cash flow is currently positive / negative / uncertain."

### Gap card
- "You appear to have a monthly surplus/deficit of £X."

### Urgency card
- "If priority bills are not current, stabilisation comes before savings or investing."

### Progress card
- "You now have a baseline for what your money is doing each month."

## Recommended actions
- If deficit: review spending, prioritise essentials, pause optimisation steps in messaging
- If positive: proceed to stability risk checks

## Progression effect
Update readiness scoreboard:
- Cash flow stability
- Crisis risk (initial estimate)

Update numerical trail:
- Monthly surplus/deficit
- Essential spend ratio

---

# Checkpoint 2 — State Support and External Help Signal

## Purpose
Prompt the user to explore support if they may be eligible or if finances are under strain.

## Inputs
### Quick
- Are you on a low income, unemployed, caring, sick, or otherwise potentially eligible for support? (yes / no / unsure)

### Guided
- employment status
- broad income band
- household composition
- dependants
- housing tenure

### Deep
All Guided inputs plus:
- disability/health impact flag
- childcare cost flag
- caring responsibilities flag

## Calculations
No hard eligibility determination unless you later integrate rules. For now use flags and prompts.

### Signal score (heuristic)
Create a support_exploration_score based on indicators such as:
- low income band
- dependants
- unstable employment
- housing stress
- childcare burden

## Insight logic
- If support_exploration_score exceeds threshold: prompt strongly
- If uncertain: encourage check rather than assume ineligibility

## Output cards
- "It may be worth checking whether you qualify for benefits or other support."
- "This tool does not determine benefit eligibility, but your profile suggests it may be worth exploring."

## Progression effect
No major numerical trail update unless displaying support flag.

---

# Checkpoint 3 — Reliance on Credit for Essentials / Distress Gate

## Purpose
Identify whether the user is borrowing to cover basic living costs, which indicates acute financial stress.

## Inputs
### Quick
- Are you using credit cards, overdrafts, or loans to pay for essentials? (yes / no)

### Guided
- same question
- amount of essential spending currently going onto credit each month (optional)

### Deep
All Guided inputs plus:
- number of months this has been happening
- whether overdraft is persistent
- arrears across any debt accounts

## Calculations
### Guided / Deep
- essentials_financed_by_debt_ratio = estimated essentials on credit / essential spending
- distress_flag = yes if any borrowing for essentials

### Deep extras
- duration_score for chronicity
- combined distress score using arrears + deficit + essentials on debt

## Insight logic
### Blocked / Critical
- any consistent borrowing for essentials

## Output cards
### Status card
- "You appear to be using debt to bridge essential spending."

### Urgency card
- "This is a financial distress signal. The priority is stabilisation, not optimisation."

### Progress card
- "This checkpoint helps distinguish a budgeting issue from a deeper affordability issue."

## Recommended actions
- prioritise important bills
- seek debt support if needed
- pause investment-focused messaging

## Progression effect
Set Crisis risk to Critical if true.

Update numerical trail with:
- distress flag
- essentials financed by debt ratio if known

---

# Checkpoint 4 — Important Bills, Essential Insurance, and Minimum Payments

## Purpose
Ensure the user protects the immediate foundations: priority bills, essential cover, and minimum debt payments.

## Inputs
### Quick
- Are you behind on any priority bills? (yes / no)
- Can you afford minimum payments on all debts? (yes / no / unsure)
- Do you have essential insurance where relevant? (yes / no / unsure)

### Guided
- minimum monthly payment for each debt
- current arrears flags
- essential insurance checklist

### Deep
All Guided inputs plus:
- category of arrears (rent, mortgage, council tax, utilities, etc.)
- missed payments count

## Calculations
- debt_minimum_total = sum(minimum monthly payments)
- affordability_after_minimums = income - essential_spending - debt_minimum_total
- arrears_count

## Insight logic
### Critical
- cannot afford minimum payments
- or any severe priority arrears

### Needs attention
- affordability_after_minimums near zero

## Output cards
- "Minimum debt payments total £X per month."
- "After essential spending and minimum debt payments, you have £Y left / short."
- "If you cannot afford minimums, a debt advice route should take priority over later optimisation."

## Progression effect
Update readiness scoreboard:
- Crisis risk
- Debt drag

Numerical trail:
- Total minimum debt payments
- Affordability after minimums

---

# Checkpoint 5 — Starter Emergency Fund

## Purpose
Build the first layer of resilience before tackling more complex optimisation.

## Inputs
### Quick
- Do you have at least some accessible cash savings set aside for emergencies? (none / a little / a reasonable amount)

### Guided
- accessible cash savings
- monthly essential spending

### Deep
All Guided inputs plus:
- whether savings are truly accessible
- whether any savings are already earmarked for unavoidable short-term costs
- income stability flag

## Calculations
### Guided / Deep
- starter_emergency_months = accessible_cash_savings / essential_spending
- starter_target_months = 1 by default, potentially 2 or 3 if risk flags are elevated
- starter_target_amount = starter_target_months * essential_spending
- starter_gap = max(0, starter_target_amount - accessible_cash_savings)
- time_to_starter_target = starter_gap / monthly_surplus if monthly_surplus > 0

## Insight logic
### Critical
- accessible_cash_savings = 0 and user is under strain

### Needs attention
- starter_emergency_months below target

### Stable enough
- starter target reached

## Output cards
### Status card
- "You currently have X months of essential spending in accessible cash."

### Gap card
- "Your starter emergency fund target is £Y. Your gap is £Z."

### Opportunity card
- "At your current surplus, you could reach this target in about N months."

### Why it matters
- "This first buffer reduces the chance that a small shock becomes new debt."

## Progression effect
Update readiness scoreboard:
- Starter buffer

Numerical trail:
- Emergency fund months
- Starter target
- Gap to starter target

---

# Checkpoint 6 — Pension Match Capture

## Purpose
Ensure the user is not missing employer pension contributions if a workplace scheme is available.

## Inputs
### Quick
- Are you contributing enough to get the full employer pension match? (yes / no / unsure / not applicable)

### Guided
- workplace pension available
- enrolled flag
- employee contribution rate/amount
- employer contribution rate/amount
- max employer match available

### Deep
All Guided inputs plus:
- tax band
- salary sacrifice flag
- intended retirement age

## Calculations
### Guided / Deep
- employer_match_gap = max employer match - current employee contribution needed for full match
- monthly_missed_match_value
- annual_missed_match_value = monthly_missed_match_value * 12

### Deep extras
- rough tax-relief effect estimate
- salary sacrifice NI-effect note if applicable

## Insight logic
### Priority
- workplace pension available and full match not captured

### Stable enough
- full match captured

## Output cards
### Opportunity card
- "You may be missing approximately £X per month of employer pension contributions."

### Gap card
- "Increasing your contribution by roughly £Y per month may unlock the full match."

### Why it matters
- "This is often one of the highest-priority uses of long-term savings because it includes employer money."

## Progression effect
Update readiness scoreboard:
- Pension capture

Numerical trail:
- Employer match status
- Annual missed match value if relevant

---

# Checkpoint 7 — High-Interest Debt / Debt Over 10% APR

## Purpose
Identify whether expensive debt should take priority over building wealth elsewhere.

## Inputs
### Quick
- Do you have any non-mortgage, non-student-loan debt over 10% APR? (yes / no / unsure)

### Guided
For each debt:
- debt type
- balance
- APR
- minimum payment

### Deep
All Guided inputs plus:
- promotional rate end dates
- refinance availability flag
- debt purpose/context flag

## Calculations
### Guided / Deep
- highest_non_mortgage_apr
- weighted_average_non_mortgage_apr
- monthly_interest_leakage
- annual_interest_leakage
- debt_priority_order sorted by APR then by behavioural urgency flags
- expensive_debt_balance_total

### Deep extras
- scenario payoff savings for extra monthly overpayments (e.g. +£100, +£250)
- promotional rate rollover warnings

## Insight logic
### Priority
- any applicable debt over 10% APR

### Stable enough
- no high-interest non-mortgage, non-student-loan debt

## Output cards
### Status card
- "Your highest-cost debt is currently X% APR."

### Gap card
- "Your expensive debt balance totals £Y."

### Urgency card
- "These debts may be costing roughly £Z per month in interest."

### Action card
- "If you overpay one debt first, the highest APR debt is usually the strongest starting point mathematically."

## Progression effect
Update readiness scoreboard:
- Debt drag

Numerical trail:
- Highest APR
- Monthly interest leakage
- Expensive debt balance

---

# Checkpoint 8 — Can the User Afford Debt Counselling / Distress Escalation

## Purpose
Separate users who need external debt help from those who can continue through the optimisation journey.

## Inputs
### Quick
- Can you afford to make minimum payments and cover essentials? (yes / no / unsure)

### Guided
Derived mostly from previous checkpoints.

### Deep
Derived plus any distress chronology.

## Calculations
- affordability_after_minimums
- distress escalation flag
- severe debt help signal if deficit persists after minimums and essentials

## Insight logic
### Blocked / Critical
- essentials and minimums cannot both be met

## Output cards
- "Your numbers suggest this is not yet an optimisation problem."
- "Stabilising essential spending and getting debt support may be the most useful next move."

## Progression effect
If escalated, later steps remain explorable but are visually marked as "future state" rather than current priority.

---

# Checkpoint 9 — Full Emergency Fund

## Purpose
Expand resilience once the immediate crisis/high-interest phase is under control.

## Inputs
### Quick
- Do you have several months of essential spending in accessible cash? (yes / no / unsure)

### Guided
- accessible cash savings
- monthly essential spending
- basic stability flags

### Deep
All Guided inputs plus:
- income volatility
- dependants
- single/dual income household
- housing security
- health-related instability

## Calculations
### Guided
- full_target_months = 3 by default, with optional range displayed
- full_target_amount = full_target_months * essential_spending
- full_gap = full_target_amount - accessible_cash_savings
- time_to_full_target = full_gap / monthly_surplus if positive

### Deep
- recommended_target_months using heuristic band such as:
  - 3 months for stable dual-income / strong security
  - 6 months for typical moderate-risk cases
  - 9–12 months for high uncertainty / dependants / variable income / single income
- target_range_low / high
- recommended_target_amount_low / high

## Insight logic
### Needs attention
- below recommended full emergency range

### Stable enough
- within or above range

## Output cards
### Status card
- "You currently hold X months of essential spending in accessible cash."

### Gap card
- "A reasonable full emergency fund target for your situation may be Y–Z months."

### Opportunity card
- "At your current surplus, your next milestone could be reached in N months."

### Why it matters
- "This buffer gives you room to absorb job, health, or housing shocks without immediate financial disruption."

## Progression effect
Update readiness scoreboard:
- Full emergency buffer

Numerical trail:
- Full emergency months
- Recommended target range
- Gap to next milestone

---

# Checkpoint 10 — Non-Mortgage / Non-Student-Loan Debt Review

## Purpose
After buffers and match capture, identify whether ordinary debt still remains and how it should interact with future goals.

## Inputs
### Quick
- Do you still have any debt other than a mortgage or student loan? (yes / no)

### Guided
Derived from debt list.

### Deep
Derived plus refinance or settlement options.

## Calculations
- remaining_non_special_debt_balance
- weighted APR on remaining debt
- guaranteed_return_from_repayment estimate = APR

## Insight logic
### Priority
- remaining debt with meaningful APR persists

### Stable enough
- no ordinary debt remains

## Output cards
- "You still have £X of non-mortgage, non-student-loan debt."
- "Repaying this debt offers a guaranteed return equivalent to its interest rate."
- "Whether it beats other uses of cash depends on rate, liquidity needs, and goals."

## Progression effect
Update Debt drag status toward In progress or Strong.

---

# Checkpoint 11 — Define Financial Goals

## Purpose
Turn vague intentions into quantified targets and dates.

## Inputs
### Quick
- Do you have specific savings or spending goals in mind? (yes / no)
- Are any of them within the next 5 years? (yes / no)

### Guided
For each goal:
- goal name
- target amount
- target date
- importance level

### Deep
All Guided inputs plus:
- flexibility flag
- inflation sensitivity flag
- whether it is a hard deadline or optional aspiration
- whether access is needed before pension age

## Calculations
### Guided / Deep
For each goal:
- months_to_goal
- required_monthly_saving = remaining_amount / months_to_goal
- goal_horizon classification:
  - short-term: within 5 years
  - long-term: beyond 5 years
- aggregate_required_monthly_short_term
- aggregate_required_monthly_long_term
- total_required_monthly_all_goals

### Deep extras
- inflation-adjusted target ranges if user opts in
- priority-weighted feasibility assessment

## Insight logic
### Needs attention
- goals not yet defined
- or required monthly saving exceeds available surplus

### Stable enough
- goals defined and funding requirements broadly fit surplus

## Output cards
### Status card
- "You have defined N goals."

### Gap card
- "To hit all current goals on time, you would need to save about £X per month."

### Trade-off card
- "Your current available surplus is £Y, so some goals may need reprioritisation or extended timelines."

### Progress card
- "Your money now has destinations rather than just categories."

## Progression effect
Update readiness scoreboard:
- Goal clarity

Numerical trail:
- Number of goals
- Total required monthly savings
- Short-term vs long-term split

---

# Checkpoint 12 — Short-Term Goals On Track?

## Purpose
Assess whether money needed soon is properly funded and appropriately placed.

## Inputs
### Quick
- Are your short-term goals on track? (yes / no / unsure)

### Guided
Derived from goals plus:
- current earmarked savings for short-term goals

### Deep
All Guided inputs plus:
- expected purchase timing confidence
- first-home flag
- estimated property value

## Calculations
### Guided / Deep
- short_term_goal_total_target
- short_term_goal_total_saved
- short_term_goal_total_gap
- monthly_short_term_required
- months_to_nearest_short_term_goal
- short_term_on_track_flag based on current progress trajectory

### Deep extras
- Cash LISA relevance heuristic for first-home purchase
- cash suitability signal based on goal horizon

## Insight logic
### Priority
- short-term goals off track

### Stable enough
- short-term goals on track

## Output cards
### Status card
- "You have £X saved toward short-term goals, against a target need of £Y."

### Gap card
- "Your short-term funding gap is £Z."

### Why it matters
- "Money needed within a short horizon usually prioritises capital stability over long-term growth potential."

### Action card
- "If a first-home purchase is relevant and the property would qualify, a Cash LISA may be worth exploring."

## Progression effect
Update readiness scoreboard:
- Short-term readiness

Numerical trail:
- Short-term funding gap
- On-track/off-track status

---

# Checkpoint 13 — Any Debt Left?

## Purpose
Before moving fully into long-term investing, confirm whether debt still competes for surplus cash.

## Inputs
### Quick
- Do you have any debt left at all? (yes / no)

### Guided
Derived from debt list.

### Deep
Derived plus mortgage and student loan specifics.

## Calculations
- total_remaining_debt
- total_remaining_non_special_debt
- mortgage_rate if supplied
- student_loan_effective_tradeoff notes if supplied

## Insight logic
This checkpoint does not automatically say all debt must be cleared first. It should produce a nuanced trade-off explanation.

## Output cards
### Trade-off card
- "Debt is not all equal. Mortgage and student loan decisions often need to be treated differently from ordinary consumer debt."

### Status card
- "You currently have £X total debt remaining. £Y of this is mortgage/student loan and £Z is other debt."

## Progression effect
This checkpoint enriches the next branch rather than serving as a stop/go on its own.

---

# Checkpoint 14 — Money Needed Before Pension Access Age

## Purpose
Identify the long-term goals that require accessible capital before pension age.

## Inputs
### Quick
- Will you need some of this long-term money before pension access age? (yes / no / unsure)

### Guided
For each long-term goal:
- before pension age / after pension age / unknown

### Deep
All Guided inputs plus:
- estimated access dates
- intended retirement age
- pension access age estimate

## Calculations
### Guided / Deep
- long_term_before_pension_target = sum(goals marked before pension age)
- long_term_before_pension_required_monthly
- years_to_first_before_pension_goal

## Insight logic
### Priority path
- if any meaningful amount is needed before pension age, accessible wrappers become relevant

## Output cards
### Status card
- "You have £X of long-term goals that appear to need access before pension age."

### Why it matters
- "Money that must remain accessible usually should not be locked entirely into pensions."

### Action card
- "This naturally points toward accessible long-term vehicles such as ISAs, depending on the goal."

## Progression effect
Update readiness scoreboard:
- Long-term readiness (part 1)

Numerical trail:
- Before-pension target amount

---

# Checkpoint 15 — Money Needed After Pension Access Age

## Purpose
Identify long-term goals that can be locked away longer and may benefit from pension efficiency.

## Inputs
### Quick
- Is some of your long-term money for life after pension access age? (yes / no / unsure)

### Guided
- after-pension goal flags
- workplace pension details already captured

### Deep
All Guided inputs plus:
- tax band
- estimated retirement age
- current pension contribution adequacy perception
- salary sacrifice flag

## Calculations
### Guided / Deep
- long_term_after_pension_target = sum(goals marked after pension age)
- long_term_after_pension_required_monthly

### Deep extras
- wrapper efficiency note using simple heuristic:
  - workplace pension first where matched,
  - pension often more tax-efficient for post-pension goals, especially at higher tax rates,
  - ISA may still matter for flexibility.

## Insight logic
### Opportunity
- if after-pension goals exist and pension capture is not optimised

## Output cards
### Status card
- "You have £X of long-term goals that can likely remain invested until after pension age."

### Opportunity card
- "For post-pension goals, pensions may be especially relevant because of employer contributions and tax treatment."

### Trade-off card
- "The more flexibility you need, the more useful non-pension wrappers may still be."

## Progression effect
Update readiness scoreboard:
- Long-term readiness (part 2)

Numerical trail:
- After-pension target amount

---

# Checkpoint 16 — Mortgage Overpayment and Student Loan Special Cases

## Purpose
Provide nuance where the flowchart treats these as special categories rather than ordinary debt.

## Inputs
### Quick
- Do you have a mortgage? (yes / no)
- Do you have a student loan? (yes / no)

### Guided
- mortgage rate
- mortgage balance (optional)
- student loan present flag

### Deep
All Guided inputs plus:
- student loan plan type
- expected repayment trajectory estimate
- fixed mortgage end date
- overpayment allowance

## Calculations
### Guided
- mortgage_guaranteed_return = mortgage_rate
- mortgage_interest_avoided_estimate for hypothetical extra payment amounts

### Deep
- simple student loan overpayment relevance score:
  - more likely relevant when high earner / likely to repay in full
  - less likely relevant if unlikely to clear balance before write-off

## Insight logic
### Mortgage
- explain guaranteed return vs liquidity trade-off

### Student loan
- explain that overpayment often depends on whether it behaves like a true repayable debt in practice

## Output cards
### Trade-off card
- "Mortgage overpayments offer a guaranteed return equal to your mortgage rate, but reduce access to cash."

### Context card
- "Student loans often behave differently from ordinary debt, so overpaying them needs separate analysis."

## Progression effect
No direct readiness pillar unless you add a Special Cases pillar. Mostly educational enrichment.

---

# Checkpoint 17 — Final Allocation Summary

## Purpose
Translate the full journey into a ranked action plan.

## Inputs
Derived from all previous checkpoints.

## Calculations
Create a ranked priority stack using the full state.

### Example priority ordering logic
1. financial distress / important bills / minimum payments
2. starter emergency fund
3. capture employer pension match
4. repay high-interest debt
5. full emergency fund
6. fund short-term goals
7. allocate to before-pension long-term investing
8. allocate to after-pension long-term investing
9. optional mortgage overpayments / student loan review / extra optimisation

## Output structure
### A. Your current stage
- "You are currently at Step X of the journey."

### B. Your top priorities now
Ranked cards with explanation.

### C. Your numbers at a glance
- Monthly surplus/deficit
- Emergency fund months
- Highest APR debt
- Monthly interest leakage
- Pension match missed/captured
- Short-term goal gap
- Before-pension target
- After-pension target

### D. What has improved through the journey
A narrative summary showing movement:
- "You started with unclear goal structure. You now have 4 defined goals."
- "You were unsure about your pension match. You now know whether you are capturing it."
- "You now know your emergency fund gap and your short-term savings gap."

### E. What to revisit later
- items marked future optimisation

## Progression effect
Mark completed checkpoints and store a snapshot of the user’s journey state.

---

## 8. Longitudinal Progress Features

To make the experience feel cumulative rather than one-off, add these features.

## 8.1 Journey Timeline
A vertical or horizontal timeline showing:
- Step reached
- Key number unlocked at each stage
- Current focus

Example timeline labels:
- Baseline cash flow established
- Distress risk assessed
- Starter buffer quantified
- Pension match checked
- High-interest debt prioritised
- Goals quantified
- Long-term pots separated

---

## 8.2 Milestone Badges
These should be informative, not childish.

Examples:
- Budget baseline created
- Crisis risk clarified
- Starter buffer quantified
- Full pension match captured
- Expensive debt identified
- Goals mapped
- Before-pension pot identified
- After-pension pot identified

---

## 8.3 Snapshot Comparisons
If the user returns later, compare against prior state.

Examples:
- "Your emergency fund has increased from 0.6 to 1.4 months."
- "Your highest debt APR has dropped from 19.9% to 0% in consumer debt."
- "Your short-term goal gap has reduced by £2,100."

This is one of the strongest ways to make the tool feel useful over time.

---

## 9. Handling Missing Data Gracefully

The tool must not become brittle when users do not know exact figures.

## Rules
- Allow estimates.
- Label estimates clearly.
- If a number is missing, show a partial insight rather than no insight.
- Distinguish between:
  - confirmed,
  - estimated,
  - and unknown.

Example:
- "Based on your estimate, your starter emergency fund is around 0.8 months."
- "We cannot yet estimate your pension match gap because employer contribution details are missing."

---

## 10. Messaging Rules for Trustworthiness

## 10.1 Do not imply regulated personalised financial advice
Prefer wording like:
- "This usually points toward…"
- "This may be a stronger priority because…"
- "This tool is designed to help you think through the sequence and trade-offs."

Avoid wording like:
- "You should definitely…"
- "The best investment for you is…"

## 10.2 Explain the maths plainly
Every formula-backed message should be translatable into plain English.

## 10.3 Never show precision without meaning
Do not overwhelm the user with complex tables unless they opt into Deep Mode or expand details.

---

## 11. Implementation Notes for Engineering

## 11.1 Recommendation Engine Pattern
Use a rules engine with four layers:

1. **Raw inputs**
2. **Derived metrics**
3. **Checkpoint state evaluation**
4. **Message and action generation**

Each checkpoint should output a structured object like:

```json
{
  "checkpoint_id": "starter_emergency_fund",
  "status": "needs_attention",
  "metrics": {
    "starter_emergency_months": 0.7,
    "starter_target_amount": 1500,
    "starter_gap": 900,
    "time_to_target_months": 4.5
  },
  "insights": [
    {
      "type": "status",
      "message": "You currently have 0.7 months of essential spending in accessible cash."
    },
    {
      "type": "gap",
      "message": "Your starter emergency fund gap is £900."
    }
  ],
  "next_actions": [
    "Prioritise building your starter emergency fund before moving further into optimisation."
  ],
  "progress_updates": [
    "Starter buffer quantified"
  ]
}
```

## 11.2 UI Storage Model
Store:
- active mode,
- entered inputs,
- derived metrics,
- checkpoint statuses,
- journey timeline state,
- last completed checkpoint,
- historical snapshots if persistence is enabled.

## 11.3 Auditability
Each recommendation should be traceable back to:
- the flowchart checkpoint,
- the inputs used,
- the formulas used,
- and the message template used.

This matters for user trust and maintainability.

---

## 12. Minimum Viable Product Scope

For the first meaningful version, implement these with full numerical insight:

1. Budget and basic stability
2. Distress / borrowing for essentials
3. Minimum debt affordability
4. Starter emergency fund
5. Pension match capture
6. High-interest debt review
7. Full emergency fund
8. Goal definition
9. Short-term goals on-track assessment
10. Before vs after pension-age long-term split
11. Final ranked action plan

That MVP is already much more actionable than a static checklist while still staying true to the source journey.

---

## 13. End State

A strong implementation of this spec should leave the user with:

- a clear sense of where they are,
- a quantified understanding of their current financial position,
- a ranked sequence of what matters next,
- a clear view of their gaps,
- and a feeling that they have progressed through a meaningful journey rather than merely reading a flowchart.

The experience should feel like this:

**The flowchart gave me the order.**
**The tool gave me my numbers, my gaps, and my next moves.**
