
# UK Personal Finance Flowchart — Implementation-Ready Flow Spec

Version: draft based on UKPF Flowchart v3.0.10  
Source canonical pages:
- Interactive flowchart: https://ukpersonal.finance/flowchart/
- Image flowchart: https://flowchart.ukpersonal.finance/

## 1. Purpose

This specification defines how to turn the UK Personal Finance Flowchart into an interactive, trustworthy, user-helpful website while staying authentic to the original flowchart’s purpose, order, and spirit.

The tool should:

1. Preserve the original sequence and branching of the flowchart.
2. Ask users only for information actually needed to move them through the flow.
3. Distinguish clearly between:
   - facts provided by the user,
   - values calculated by the tool,
   - guidance derived from the flowchart,
   - educational context pulled from the linked UKPF wiki pages.
4. Avoid pretending to give regulated personal financial advice.
5. Produce outputs that are actionable, explainable, and easy to revisit later.

This tool is not a robo-adviser. It is a guided implementation of the UKPF flowchart and related educational pages.

---

## 2. Product philosophy

The website should feel like:
- a structured financial triage and prioritisation engine,
- an educational guide,
- a progress tracker.

It should **not** feel like:
- an investment recommendation engine picking specific securities,
- a debt consolidation sales funnel,
- a tax or benefits filing tool,
- a substitute for regulated financial advice.

The original flowchart is intentionally a prioritisation framework. The interactive version should preserve that.

---

## 3. Design principles for authenticity

### 3.1 Preserve original step order

The core order must remain:

1. Budget / immediate financial stability
2. Initial emergency fund
3. Pension enrolment / employer match
4. Assess debts
5. Full emergency fund
6. Define goals
7. Short-term goals (<5 years)
8. Long-term goals (>5 years)

### 3.2 Preserve original branch logic

The key branch questions from the flowchart must stay explicit:

- Do you rely on credit cards or loans for essentials?
- Can you afford minimum debt payments?
- Do you have any debt over 10% APR?
- Do you have any debt other than a mortgage or student loan?
- Are your short-term goals on track?
- Do you have any debt?
- Are savings required before pension access age?
- Are savings required after pension access age?

### 3.3 Keep “actions” separate from “questions”

Some flowchart boxes are not branch conditions. They are actions:
- Create a budget
- Check benefit entitlement
- Prioritise important bills
- Insure essentials
- Make minimum debt payments
- Seek debt counselling
- Build emergency fund
- Enrol in pension and get employer match
- Overpay expensive debt
- Define goals
- Save in cash for near-term goals
- Invest for long-term goals

In the website, actions should become recommendation cards or tasks, not yes/no questions unless a completion check is necessary.

### 3.4 Keep it useful, not literalist

The flowchart is a map, not a line-by-line questionnaire. The interactive product should ask enough questions to route accurately, but no more than needed. Do not force the user to manually answer questions that can be derived from prior inputs.

Example:
- If the user enters debts with APRs, the tool should derive whether they have debt over 10% APR.
- If the user enters savings goals with target dates, the tool should derive whether goals are within 5 years.
- If the user enters age/date of birth, the tool should estimate pension-access-age relevance.

---

## 4. Legal, trust, and licensing requirements

### 4.1 Educational-not-advice positioning
The site must clearly state that:
- it is for information and education,
- it is not personal financial advice,
- users should do their own research,
- users may need regulated advice for complex or high-stakes decisions.

### 4.2 Credit and licensing
The source flowchart is published under Creative Commons Attribution-NonCommercial-ShareAlike (CC BY-NC-SA 4.0).  
The site must:
- give clear attribution to UKPersonalFinance,
- link to the source flowchart and wiki,
- remain non-commercial unless permissions are separately obtained,
- license derivative content under compatible terms if applicable.

### 4.3 Crisis / harm prevention
If a user indicates:
- they cannot afford minimum payments,
- they are using debt for essentials,
- they are in rent/mortgage/council tax arrears,
- they are in severe financial distress,

then the interface must immediately elevate debt-charity / crisis support guidance before continuing.

---

## 5. Recommended technical architecture

This product should be built as a website with a **data-driven decision engine**.

Recommended stack:
- SvelteKit or Astro with TypeScript front-end
- content layer in Markdown/JSON/YAML
- decision engine in JSON/TypeScript rules
- optional local persistence in browser storage
- optional account sync later, but not required for MVP

### 5.1 Separate these concerns

1. **Content**
   - explanations
   - educational notes
   - source links
   - glossary text

2. **Rules**
   - questions
   - field definitions
   - conditions
   - branching
   - recommended next actions

3. **Presentation**
   - forms
   - cards
   - progress UI
   - dashboards
   - printable summary

### 5.2 Why this matters
The UKPF flowchart will evolve. A clean rules/content split allows:
- version updates,
- A/B testing of UI copy,
- easier validation against source flowchart versions,
- multilingual or simplified-language variants later.

---

## 6. Product scope

## 6.1 MVP scope

The MVP should do the following well:
- guide a user through the full flowchart
- ask for the minimum viable set of financial inputs
- derive the branch outcomes
- generate a prioritised action plan
- explain why each action is recommended
- link to the corresponding UKPF wiki pages
- save the user’s progress locally
- allow later revisit/edit

## 6.2 Out of scope for MVP
Do not include initially:
- product comparison marketplaces
- bank account aggregation
- live credit checks
- pension tracing integrations
- investment portfolio construction
- benefits eligibility calculations done internally
- tax optimisation calculators beyond simple explanatory logic

Those can be later modules.

---

## 7. Core user journeys

There are three primary user journeys:

### 7.1 New user journey
A new user wants to understand:
- what to prioritise first,
- where they are financially vulnerable,
- what they should do next.

### 7.2 Returning user journey
A returning user wants to:
- update balances/savings,
- re-run the flow,
- see whether they moved to the next stage.

### 7.3 Educational explorer journey
A user wants to:
- inspect a specific step,
- understand “why this before that,”
- jump into relevant wiki explanations.

---

## 8. Canonical domain model

The tool should use the following normalized entities.

### 8.1 UserProfile
- user_id (optional if anonymous/local only)
- created_at
- updated_at
- locale (default UK)
- dob_or_age
- employment_status
- tax_band_estimate
- housing_status
- has_dependants
- partner_joint_finances_flag

### 8.2 IncomeItem
- id
- owner (user / partner / household / unknown)
- type
  - salary
  - self_employment
  - pension_income
  - benefits
  - rental_income
  - dividends
  - other
- gross_amount_monthly
- net_amount_monthly
- frequency
- stability
  - stable
  - variable
  - seasonal
  - unknown

### 8.3 ExpenseItem
- id
- type
  - housing
  - utilities
  - council_tax
  - food
  - transport_to_work
  - childcare
  - insurance
  - debt_minimums
  - subscriptions
  - discretionary
  - other
- amount_monthly
- essential_flag
- priority_bill_flag

### 8.4 DebtItem
- id
- type
  - credit_card
  - overdraft
  - personal_loan
  - car_finance
  - buy_now_pay_later
  - store_card
  - mortgage
  - student_loan
  - family_loan
  - tax_debt
  - council_tax_arrears
  - rent_arrears
  - utility_arrears
  - other
- balance
- apr
- minimum_payment_monthly
- promotional_rate_flag
- secured_flag
- arrears_flag
- priority_debt_flag
- refinance_possible_unknown_flag

### 8.5 SavingsAccount
- id
- type
  - easy_access_cash
  - notice_account
  - fixed_term_cash
  - cash_isa
  - premium_bonds
  - current_account_cash
  - lisa_cash
  - lisa_stocks_shares
  - s_and_s_isa
  - gia
  - pension
  - other
- balance
- accessible_now_flag
- purpose_tag
  - emergency
  - short_term_goal
  - long_term
  - mixed
  - unknown

### 8.6 PensionProfile
- workplace_pension_enrolled_flag
- employee_contribution_pct
- employer_contribution_pct
- employer_max_match_pct
- salary_sacrifice_flag
- higher_rate_taxpayer_flag
- pension_access_age_estimate

### 8.7 Goal
- id
- title
- category
  - emergency_fund
  - first_home_deposit
  - home_purchase
  - holiday
  - wedding
  - vehicle
  - education
  - retirement
  - early_retirement
  - mortgage_overpayment
  - child_savings
  - general
- target_amount
- target_date
- priority
- notes
- goal_horizon
  - under_1_year
  - one_to_five_years
  - over_five_years
  - unknown
- requires_cash_flag
- may_accept_investment_risk_flag

---

## 9. Minimum required user inputs

To route someone through the flowchart, the site needs the following minimum inputs.

## 9.1 Household basics
Required:
- age or date of birth
- monthly take-home income
- monthly essential spending
- monthly total spending
- accessible cash savings
- employment type
- whether finances are individual or household-level

Helpful:
- dependants
- housing status
- whether income is stable or variable

## 9.2 Debt inputs
For each debt:
- type
- balance
- APR or interest rate
- monthly minimum payment
- whether in arrears

## 9.3 Pension inputs
- workplace pension enrolled? yes/no/unknown
- current employee contribution %
- employer contribution %
- maximum employer match available? yes/no/unknown
- higher-rate tax payer? yes/no/unknown
- salary sacrifice available? yes/no/unknown

## 9.4 Goal inputs
For each goal:
- title
- target amount
- target date or time horizon
- whether it is flexible or fixed

## 9.5 Distress / affordability flags
Required:
- are essentials being paid with credit?
- can minimum debt payments be made?
- are any priority bills in arrears?
- is emergency support / benefit check needed?

---

## 10. Derived fields the engine should calculate

The site should calculate these automatically.

### 10.1 Budget metrics
- surplus_or_deficit = net_monthly_income - monthly_total_spending
- essentials_coverage = accessible_cash_savings / essential_monthly_spending
- minimum_debt_payment_burden = sum(minimum debt payments) / net income

### 10.2 Debt metrics
- highest_apr
- any_debt_over_10_apr
- any_non_mortgage_non_student_debt
- any_debt_at_all
- total_unsecured_debt
- total_priority_arrears
- can_use_avalanche_ordering

### 10.3 Emergency fund metrics
- initial_emergency_fund_target_months = configurable default 1 to 3
- full_emergency_fund_target_months = configurable default 3 to 6, extendable to 9 or 12
- current_emergency_months = accessible_emergency_cash / essential_monthly_spending

### 10.4 Goal metrics
- months_to_goal
- required_monthly_saving_per_goal
- short_term_goals_total
- long_term_goals_total
- short_term_goals_on_track_flag
- before_pension_access_goal_amount
- after_pension_access_goal_amount

### 10.5 Pension metrics
- is_missing_employer_match
- estimated_pension_access_age
- pre_pension_need_flag
- post_pension_need_flag

---

## 11. Product states

Each user should have a current state:

- `distress`
- `stabilising`
- `building_initial_buffer`
- `capturing_employer_match`
- `clearing_expensive_debt`
- `building_full_emergency_fund`
- `goal_planning`
- `funding_short_term_goals`
- `balancing_debt_vs_long_term`
- `funding_pre_pension_long_term_goals`
- `funding_post_pension_long_term_goals`
- `mixed_long_term_strategy`

This gives the product a clean way to display “where you are on the flowchart.”

---

## 12. Node taxonomy

Every node in the implementation should be one of:

- `question`
- `action`
- `calculation`
- `info`
- `outcome`
- `warning`
- `external_support`

Example:
- “Do you have any debt over 10% APR?” = question
- “Overpay debts, focusing on highest interest rates” = action
- “Emergency fund months = savings / essential spending” = calculation
- “This is not financial advice” = info
- “Seek debt counselling from a reputable charity” = external_support

---

## 13. Full flow spec by node

This is the core implementation section.

## 13.1 Start node

### Node ID
`start`

### Type
info

### Purpose
Orient the user and frame expectations.

### UI content
- This tool follows the UK Personal Finance Flowchart.
- It helps prioritise the order of financial actions.
- It is educational, not personal financial advice.

### Next
`collect_basics`

---

## 13.2 Collect household basics

### Node ID
`collect_basics`

### Type
question bundle

### Required inputs
- age/date of birth
- take-home income per month
- essential expenses per month
- total expenses per month
- accessible cash savings
- employment status / income stability

### Optional inputs
- dependants
- partner/household mode
- housing status

### Derived outputs
- monthly surplus/deficit
- emergency fund months

### Next
`check_benefit_entitlement_prompt`

---

## 13.3 Check benefit entitlement

### Node ID
`check_benefit_entitlement_prompt`

### Type
action/info

### Purpose
Faithfully reflect the Step 1 instruction to check eligibility for state support.

### UX behaviour
Do not force a long internal benefits questionnaire in MVP.
Instead:
- ask whether the user wants a benefit entitlement check
- offer external links/resources
- allow a flag: `benefit_check_pending`

### Inputs
- none required for branching

### Next
`credit_for_essentials_check`

---

## 13.4 Credit for essentials check

### Node ID
`credit_for_essentials_check`

### Type
question

### Question
Are you currently relying on credit cards, overdrafts, BNPL, or loans to pay for essentials such as food, rent, bills, or commuting?

### Answers
- yes
- no
- not sure

### Meaning
This is a financial distress signal.

### Branching
- yes -> `prioritise_important_bills`
- no -> `insure_essentials`
- not sure -> show help text, then proceed conservatively to `prioritise_important_bills`

---

## 13.5 Prioritise important bills

### Node ID
`prioritise_important_bills`

### Type
action/warning

### Purpose
Reflect the flowchart’s “Prioritise important bills, e.g. council tax, food, mortgage/rent, transport for work.”

### Inputs
- priority bill arrears
- monthly essentials
- user free text on urgent arrears

### Output
Show a priority ordering:
1. housing/rent/mortgage
2. council tax
3. food/basic living
4. work transport / essential utilities
5. everything else

### Next
`insure_essentials`

---

## 13.6 Insure essentials

### Node ID
`insure_essentials`

### Type
action/info

### Purpose
Reflect “Insure essentials (car, home, etc). Also consider insurance for life, income, etc.”

### Inputs
- car owner?
- renter/homeowner?
- dependants?
- main breadwinner?
- employer income protection?

### Output
A guidance card, not a hard gate:
- consider car/home cover where applicable
- if dependants or income reliance exists, highlight life/income protection

### Next
`collect_debts`

---

## 13.7 Collect debts

### Node ID
`collect_debts`

### Type
question bundle

### Required inputs
For each debt:
- type
- balance
- APR
- minimum payment
- arrears yes/no

### Derived outputs
- total minimums
- highest APR
- any >10% APR
- any non-mortgage/non-student debt
- any debt at all
- debt affordability signal

### Next
`minimum_payment_affordability_check`

---

## 13.8 Minimum payment affordability check

### Node ID
`minimum_payment_affordability_check`

### Type
question + calculation check

### Question
Can you afford the minimum payments on all debts this month?

### Inputs
- explicit user answer
- calculated budget surplus/deficit
- debt minimum total

### Rule
If user says “no”, trust the user over the model.

### Branching
- no -> `debt_charity_support`
- yes -> `make_minimum_payments_action`
- not sure -> ask follow-up or route conservatively to `debt_charity_support`

---

## 13.9 Debt charity support

### Node ID
`debt_charity_support`

### Type
external_support / high-priority warning

### Purpose
Faithfully represent the flowchart’s “Seek debt counselling from a reputable charity” path.

### Trigger conditions
Any of:
- cannot afford minimum payments
- using credit for essentials
- priority arrears
- user feels overwhelmed / cannot realistically repay

### Output
- strong recommendation to contact a debt charity
- save progress and pause the rest of the flow if necessary
- allow continuing to educational content, but mark all later suggestions as secondary until immediate crisis is addressed

### Next
Optional:
- `make_minimum_payments_action`
or end-state summary for crisis mode

---

## 13.10 Make minimum payments action

### Node ID
`make_minimum_payments_action`

### Type
action

### Purpose
Reflect the rule: always make minimum payments on all debts before overpaying.

### Output
Task card:
- maintain minimum payments on all debts
- avoid missing contractual payments
- note arrears separately

### Next
`initial_emergency_fund_stage`

---

## 13.11 Initial emergency fund stage

### Node ID
`initial_emergency_fund_stage`

### Type
calculation + action

### Purpose
Reflect Step 2: build an initial emergency fund of 1–3 months of outgoings.

### Inputs
- essential monthly spending
- accessible emergency cash

### Derived fields
- current_emergency_months
- target_initial_months (configurable default = 1 month minimum, recommended range 1–3)

### Branching
- if current_emergency_months < initial target -> recommend `build_initial_emergency_fund`
- else -> move to `pension_match_check`

### Important implementation note
The site should let the user choose within a guided range:
- 1 month if very high-interest debt is pressing
- up to 3 months if income is unstable or risk tolerance requires it

### Next
`pension_match_check`

---

## 13.12 Build initial emergency fund

### Node ID
`build_initial_emergency_fund`

### Type
action

### Output
- show target amount
- show gap amount
- show monthly saving needed to reach target in chosen timeframe
- recommend easy-access cash, not volatile investments

### Next
`pension_match_check`

---

## 13.13 Pension match check

### Node ID
`pension_match_check`

### Type
question + calculation

### Question
Are you enrolled in a workplace pension, and are you contributing enough to receive the full employer match, if affordable?

### Inputs
- workplace pension enrolled yes/no
- employee contribution %
- employer contribution %
- max employer match %
- affordability context

### Derived output
- missing employer match yes/no/unknown

### Branching
- if missing match and affordable -> `increase_pension_to_match`
- otherwise -> `debt_over_10_check`

### Implementation note
This should be treated as a very strong recommendation, not a universal command if the user is in severe cashflow stress.

---

## 13.14 Increase pension to employer match

### Node ID
`increase_pension_to_match`

### Type
action

### Output
- explain employer match as high-priority free compensation
- estimate additional employee contribution needed
- show simple monthly contribution delta if inputs allow

### Next
`debt_over_10_check`

---

## 13.15 Debt over 10% APR check

### Node ID
`debt_over_10_check`

### Type
question (derived)

### Question
Do you have any debt over 10% APR?

### Inputs
- DebtItem list

### Rule
Derived automatically from debt APRs.
If debt APR unknown, treat as unresolved and ask user to confirm.

### Branching
- yes -> `overpay_expensive_debt`
- no -> `full_emergency_fund_stage`
- unknown -> `resolve_unknown_debt_apr`

---

## 13.16 Resolve unknown debt APR

### Node ID
`resolve_unknown_debt_apr`

### Type
question

### Purpose
Avoid silent misrouting because APR data is missing.

### Question
Do any of your debts have interest above 10% APR, or are you unsure?

### Branching
- yes/unsure -> `overpay_expensive_debt`
- no -> `full_emergency_fund_stage`

---

## 13.17 Overpay expensive debt

### Node ID
`overpay_expensive_debt`

### Type
action

### Purpose
Reflect the flowchart and UKPF debt page:
- reduce rates where possible
- overpay highest-interest debt first

### Inputs
- debt list
- APR
- promo expiry dates if known

### Output
- ordered avalanche list of debts
- refinance reminder if relevant
- monthly overpayment target
- payoff illustrations optional

### Rules
- always maintain minimum payments on all debts
- direct extra cash to highest APR debt first
- suggest refinance/transfer check where realistic
- do not prioritise student loan here unless specifically modelled later

### Next
`full_emergency_fund_stage`

---

## 13.18 Full emergency fund stage

### Node ID
`full_emergency_fund_stage`

### Type
calculation + action

### Purpose
Reflect Step 5: build emergency fund to 3–12 months depending on circumstances.

### Inputs
- essential spending
- accessible cash
- income stability
- dependants
- single/dual income context
- health/job volatility confidence
- housing / obligation intensity

### Derived recommendation
Suggested target months:
- 3 months: relatively secure situation
- 6 months: common baseline for many users
- 9–12 months: variable income, single earner with dependants, uncertainty

### Output
- recommended full EF target
- rationale
- current gap
- suggested monthly build rate

### Next
`define_goals`

---

## 13.19 Define goals

### Node ID
`define_goals`

### Type
question bundle

### Purpose
Reflect Step 6: define goals, amounts needed, target dates.

### Required inputs
For each goal:
- name
- amount
- date/time horizon

### Optional inputs
- priority
- flexibility
- emotional importance
- must_be_cash yes/no

### Derived outputs
- short-term vs long-term classification
- monthly savings required
- before/after pension access classification

### Next
`short_term_goals_check`

---

## 13.20 Short-term goals check

### Node ID
`short_term_goals_check`

### Type
question + calculation

### Question
Are your short-term goals (<5 years) on track?

### Preferred implementation
Do **not** ask this as a vague yes/no only.
Calculate it:
- compare required monthly savings for all goals within 5 years
- compare against available monthly surplus after higher-priority steps

### Output states
- on_track
- off_track
- insufficient_data

### Branching
- off_track -> `fund_short_term_goals`
- on_track -> `non_mortgage_non_student_debt_check`
- insufficient_data -> ask user to confirm

---

## 13.21 Fund short-term goals

### Node ID
`fund_short_term_goals`

### Type
action

### Purpose
Reflect Step 7.

### Recommendations
Primary:
- savings accounts / cash accounts
- premium bonds as an option in relevant cases
- cash LISA for first-home deposit under qualifying rules if applicable

### Inputs
- goal list under 5 years
- first-home flag
- target property value if relevant
- age if using LISA
- accessibility needs

### Guardrails
- do not default to investing for <5-year goals
- explain that cash is preferred for near-term goals

### Next
`non_mortgage_non_student_debt_check`

---

## 13.22 Non-mortgage non-student debt check

### Node ID
`non_mortgage_non_student_debt_check`

### Type
question (derived)

### Question
Do you have any debt other than a mortgage or student loan?

### Inputs
- debt list

### Branching
- yes -> `debt_repayment_schedule`
- no -> `review_budget_and_discretionary_spending`

---

## 13.23 Debt repayment schedule

### Node ID
`debt_repayment_schedule`

### Type
action

### Purpose
Reflect Step 4 action after short-term goals are on track:
build a debt repayment schedule taking into account debt interest and savings rates.

### Inputs
- remaining debt balances
- APRs
- goal funding status
- monthly surplus

### Output
- payoff plan
- suggested order
- estimated payoff date
- compare debt APR vs savings rate where relevant

### Note
Student loans and mortgages should not be treated the same as consumer debt. Route them to dedicated context if overpayment consideration appears.

### Next
`review_budget_and_discretionary_spending`

---

## 13.24 Review budget and discretionary spending

### Node ID
`review_budget_and_discretionary_spending`

### Type
action/info

### Purpose
Reflect the flowchart box:
“Review your budget. You are now in a better position to increase your discretionary spending if you wish.”

### Output
- affirm progress
- show optional increase in guilt-free discretionary budget
- maintain progress against goals

### Next
`any_debt_check`

---

## 13.25 Any debt check

### Node ID
`any_debt_check`

### Type
question (derived)

### Question
Do you have any debt?

### Inputs
- any remaining debts at all

### Branching
- yes -> `assess_mortgage_student_overpayment`
- no -> `pre_pension_need_check`

---

## 13.26 Assess mortgage/student overpayment

### Node ID
`assess_mortgage_student_overpayment`

### Type
action/info

### Purpose
Reflect the flowchart note:
assess overpayment benefit based on goals and preferences, with dedicated treatment for student loans and mortgages.

### Inputs
- mortgage APR
- mortgage term
- overpayment flexibility
- student loan plan/type if available
- expected earnings trend (optional)
- user priorities: certainty, flexibility, psychological comfort, liquidity

### Output
Two separate analysis cards:
1. Mortgage overpayment considerations
2. Student loan overpayment considerations

### Guardrails
- student loans should not be treated like standard debt
- mortgage overpayments are illiquid; savings/investments remain liquid
- this node should be educational/comparative rather than prescriptive

### Next
`pre_pension_need_check`

---

## 13.27 Pre-pension need check

### Node ID
`pre_pension_need_check`

### Type
question (derived)

### Question
Will you need some of this long-term money before pension access age?

### Preferred implementation
Derive from goals:
- if any goal target date is before estimated pension access age and over 5 years away, this is yes

### Branching
- yes -> `fund_pre_pension_long_term`
- no -> `post_pension_need_check`
- both pre and post needs -> `fund_pre_pension_long_term` then `post_pension_need_check`

---

## 13.28 Fund pre-pension long-term

### Node ID
`fund_pre_pension_long_term`

### Type
action

### Purpose
Reflect the flowchart’s “Savings required before pension access age (~58)” branch.

### Recommendations
Focus on:
- Stocks & Shares ISA
- Stocks & Shares LISA for qualifying first-home or retirement use with caution
- General Investment Account if ISA allowance is used up

### Inputs
- long-term goals before pension access age
- ISA allowance use
- LISA eligibility
- property goal relevance
- tax band estimate

### Guardrails
- do not recommend a GIA before using sensible tax wrappers unless the user has already used ISA allowance
- warn that LISA has restrictions and penalties for non-qualifying withdrawal

### Next
`post_pension_need_check`

---

## 13.29 Post-pension need check

### Node ID
`post_pension_need_check`

### Type
question (derived)

### Question
Will you need long-term savings after pension access age?

### Preferred implementation
Usually yes for retirement unless user explicitly says otherwise.
Derive from retirement/late-life goals.

### Branching
- yes -> `fund_post_pension_long_term`
- no -> `final_summary`

---

## 13.30 Fund post-pension long-term

### Node ID
`fund_post_pension_long_term`

### Type
action

### Purpose
Reflect the flowchart’s “Savings required after pension access age (~58)” branch.

### Recommendations
Focus on:
- workplace pension
- SIPP where relevant
- Stocks & Shares LISA where suitable and drawbacks understood

### Inputs
- retirement goals
- tax band estimate
- workplace pension status
- salary sacrifice
- age
- need for flexibility

### Guardrails
- workplace pension should usually come before SIPP in basic implementation unless special circumstances
- explain tax relief vs access restrictions
- reflect that pensions are especially powerful if employer match or higher-rate relief applies

### Next
`final_summary`

---

## 13.31 Final summary

### Node ID
`final_summary`

### Type
outcome

### Purpose
Provide the user with a prioritised plan that mirrors the flowchart journey.

### Output sections
1. Where you are on the flowchart
2. Your current priorities
3. Actions to do now
4. Actions to do next
5. Items to revisit later
6. Relevant UKPF reading links
7. Warnings / unresolved uncertainties

---

## 14. Decision rules in plain language

This section is the logic contract for developers.

### Rule A: Crisis overrides optimisation
If the user is using debt for essentials or cannot make minimum payments, route to support/warnings before discussing investing.

### Rule B: Minimum payments always come before overpayments
Never propose debt overpayments while ignoring minimums on other debts.

### Rule C: Initial emergency buffer comes early
Before aggressive optimisation, build a basic cash buffer.

### Rule D: Employer pension match is high priority
If affordable and available, capture employer match early.

### Rule E: High-interest consumer debt beats mid/late-stage investing
Debt above 10% APR generally takes priority over later-stage emergency fund filling and investing.

### Rule F: Full emergency fund precedes long-term investing for most users
Except in edge cases the user should reach an appropriate full emergency fund before heavy long-term investing.

### Rule G: Short-term goals stay in cash
Goals within 5 years should default to cash-based saving.

### Rule H: Long-term goals may use investment wrappers
For long-term goals, use tax-efficient wrappers and low-cost diversified investing principles.

### Rule I: Mortgages and student loans are special cases
Do not lump them into ordinary high-interest debt logic.

---

## 15. Question catalogue

This is the implementation-ready question list.

## 15.1 Screen: Basics
- What is your age or date of birth?
- Are these finances just yours, or household finances?
- What is your average monthly take-home income?
- What are your average monthly essential expenses?
- What are your average monthly total expenses?
- How much do you currently have in accessible cash savings?
- Is your income stable, variable, or uncertain?

## 15.2 Screen: Financial strain
- Are you currently using credit to pay for essentials?
- Are any priority bills or arrears causing immediate pressure?
- Can you afford the minimum payments on all debts this month?
- Would you like to check whether you may be eligible for benefits or support?

## 15.3 Screen: Debts
For each debt:
- What type of debt is it?
- What is the balance?
- What is the APR / interest rate?
- What is the minimum monthly payment?
- Is it in arrears?
- Is this a promotional or temporary rate?

## 15.4 Screen: Pension
- Are you enrolled in a workplace pension?
- What percentage do you contribute?
- What does your employer contribute?
- Do they offer a higher maximum match?
- Are you a higher-rate taxpayer?
- Is salary sacrifice available?

## 15.5 Screen: Goals
For each goal:
- What are you saving for?
- How much do you need?
- When do you need it?
- How important is it?
- Is that date flexible?
- Would you be comfortable investing this money if the goal is far away?

## 15.6 Screen: Protection / context
- Do you have dependants?
- Are you the main breadwinner?
- Do you own a car?
- Do you rent or own your home?
- Do you already have relevant insurance cover?

---

## 16. Mapping inputs to flowchart decisions

### 16.1 “Do you rely on credit cards or loans for essentials?”
Use:
- explicit yes/no user answer
- optionally infer if monthly deficit exists and revolving debt is growing

### 16.2 “I can’t afford to…”
Use:
- explicit answer on minimum debt affordability
- arrears and persistent deficit as supporting evidence

### 16.3 “Do you have any debt over 10% APR?”
Use:
- max APR across non-excluded debts
- exclude student loans from ordinary consumer-debt logic
- do not use mortgage APR here as the intended spirit is expensive debt

### 16.4 “Are your short-term goals on track?”
Use:
- sum of required monthly savings for all goals <= available monthly surplus allocated to those goals

### 16.5 “Do you have any debt other than a mortgage or student loan?”
Use:
- derived from debt type list

### 16.6 “Do you have any debt?”
Use:
- any debt balance > 0 of any type

### 16.7 “Savings required before pension access age”
Use:
- goal target date and user age
- retirement age assumptions configurable
- should allow manual override

### 16.8 “Savings required after pension access age”
Use:
- retirement goals or default retirement need
- should allow manual override if user only has pre-access goals

---

## 17. Recommendations engine outputs

Every recommendation card should have this structure:

- `title`
- `priority`
- `why_you_are_seeing_this`
- `recommended_action`
- `how_to_do_this`
- `watch_out_for`
- `source_links`
- `can_mark_complete`
- `depends_on`

Example:
- Title: Build an initial emergency fund
- Priority: High
- Why: You currently have 0.4 months of essential spending in accessible cash
- Action: Build toward 1–3 months of essential spending
- Watch out for: Don’t lock this money away or invest it in volatile assets
- Sources: Emergency Fund, Savings Accounts

---

## 18. Scoring and prioritisation

Do not reduce the whole site to a single score.  
Instead use ordered priorities:
- `urgent`
- `high`
- `medium`
- `later`

Example:
- urgent: contact debt charity / address arrears
- high: build 1 month emergency fund, get employer match
- medium: finish full emergency fund, define goals
- later: optimise pre- vs post-pension investing mix

This is more faithful to the flowchart than a gamified score.

---

## 19. Handling uncertainty and unknown answers

The engine must support:
- `yes`
- `no`
- `unknown`

If a key field is unknown:
- surface it explicitly,
- explain why it matters,
- route conservatively.

Examples:
- unknown employer match -> recommend checking pension portal/HR
- unknown APR -> recommend checking statements before final debt prioritisation
- unknown target dates -> classify goals as provisional until clarified

---

## 20. Edge-case handling

### 20.1 Self-employed or variable income users
Use more conservative emergency fund recommendations and avoid overconfident monthly projections.

### 20.2 Joint finances
Allow either:
- user-only mode
- household mode

Do not silently mix both.

### 20.3 High earners with tax complexity
Keep guidance educational. The tool can flag:
- pension tax efficiency may be especially relevant
- higher-rate tax relief may change account preference
without trying to fully replace tax planning.

### 20.4 Users with little/no goals defined
Allow a placeholder “general resilience / flexibility” goal set rather than blocking progression.

### 20.5 Renters vs homeowners
Only surface mortgage overpayment logic if a mortgage exists.

### 20.6 Student loans
Present bespoke educational guidance. Do not place them in ordinary debt-avalanche recommendations.

### 20.7 Users already advanced
If user already has:
- strong emergency fund
- no bad debt
- pension contributions sorted
- clear goals
then quickly route them to long-term account selection and investment education.

---

## 21. Content requirements for each step

Every major step page/card should include:
- plain-English explanation
- why this step comes before the next one
- what data was used to decide
- examples
- common mistakes
- link to source wiki page

This is what makes the tool genuinely useful rather than just mechanically branched.

---

## 22. UX recommendations

### 22.1 Interface structure
Use a two-pane or stepper design:
- left/top: current stage and progress through flowchart
- main area: current questions/actions
- expandable: “why this matters” and “show underlying logic”

### 22.2 Visual fidelity
Include:
- a simplified visual map of the original flowchart
- highlight the user’s current position
- allow “view whole flowchart”

### 22.3 Keep forms short
Do not present a huge one-page form.
Use progressive disclosure:
- basics
- strain/debt
- pension
- goals
- outputs

### 22.4 Allow save-and-return
Users may need time to find:
- APRs
- employer match details
- target dates for goals

### 22.5 Explain assumptions
Whenever the engine estimates something, show:
- “Assumed because…”
- “Change this if inaccurate”

---

## 23. Suggested URL / route model

Example routes:

- `/`
- `/start`
- `/basics`
- `/financial-strain`
- `/debts`
- `/pension`
- `/goals`
- `/results`
- `/results/step-1`
- `/results/step-2`
- `/learn/emergency-fund`
- `/learn/pensions`
- `/learn/debt`
- `/about`
- `/methodology`

---

## 24. Suggested rules-engine schema

Example conceptual schema:

```json
{
  "node_id": "debt_over_10_check",
  "type": "question",
  "label": "Do you have any debt over 10% APR?",
  "inputs": ["debt_items[].apr", "debt_items[].type"],
  "derived": true,
  "logic": "exists(debt where type not in ['student_loan'] and apr > 10)",
  "branches": {
    "yes": "overpay_expensive_debt",
    "no": "full_emergency_fund_stage",
    "unknown": "resolve_unknown_debt_apr"
  }
}
```

---

## 25. Suggested data contracts for summary output

The final result object should include:

```json
{
  "flowchart_version_basis": "3.0.10",
  "current_stage": "building_full_emergency_fund",
  "urgent_flags": ["priority_bill_arrears"],
  "derived_metrics": {
    "monthly_surplus": 420,
    "emergency_months": 1.4,
    "highest_debt_apr": 24.9
  },
  "recommended_actions": [
    {
      "id": "overpay_expensive_debt",
      "priority": "high"
    },
    {
      "id": "build_full_emergency_fund",
      "priority": "high"
    }
  ],
  "unknowns": ["employer_max_match_pct"],
  "source_links": [
    "https://ukpersonal.finance/flowchart/",
    "https://ukpersonal.finance/debt/",
    "https://ukpersonal.finance/emergency-fund/"
  ]
}
```

---

## 26. Validation checklist against source flowchart

Before release, test that the implementation preserves all of these:

- Step 1 includes budget, support check, important bills, insurance, minimum debt payments, and debt-charity route.
- Step 2 is an initial emergency fund before later optimisation.
- Step 3 includes workplace pension enrolment and employer match.
- Step 4 contains debt assessment, especially high-interest debt logic.
- Step 5 expands emergency fund to full level.
- Step 6 defines goals, amounts, and dates.
- Step 7 routes near-term goals into cash-oriented saving.
- Step 8 splits long-term planning into before vs after pension access age.
- Consumer debt, mortgage debt, and student loans are not collapsed into one simplistic rule.
- Distress states interrupt later-stage optimisation.

---

## 27. Source mapping table

| Flowchart concept | Interactive implementation |
|---|---|
| Create a budget | Basics intake + budget summary + editable categories |
| Check eligibility for state support | External support prompt + resource links |
| Rely on credit for essentials? | Distress question |
| Prioritise important bills | Urgent action card + arrears capture |
| Insure essentials | Guidance card with contextual prompts |
| Make minimum payments | Mandatory debt action card |
| I can’t afford to | Crisis route to debt support |
| Build initial emergency fund | Calculated target and savings plan |
| Pension enrolment | Employer match check and action |
| Debt over 10% APR? | Derived debt branch |
| Overpay expensive debt | Avalanche-style payoff plan |
| Full emergency fund | Risk-adjusted target recommendation |
| Define goals | Goal creation workflow |
| Short-term goals on track? | Calculated affordability/on-track check |
| Save for goals within 5 years | Cash savings recommendations |
| Debt other than mortgage/student? | Derived branch from debt types |
| Review budget / discretionary spending | Progress/celebration + budget rebalance |
| Any debt? | Derived branch |
| Assess mortgage/student overpayment | Separate comparative guidance |
| Savings before pension access age | Long-term wrappers for accessible future use |
| Savings after pension access age | Pension-centric retirement branch |

---

## 28. MVP deliverables

The MVP should include:

1. Rules file
   - machine-readable node and branch definitions

2. Content file
   - educational copy and source links per node

3. Web app
   - progressive questionnaire
   - results dashboard
   - save/return support

4. Summary export
   - Markdown or PDF-style action plan

5. Methodology page
   - what this tool is
   - what it is not
   - attribution
   - version basis
   - source links

---

## 29. Nice-to-have future enhancements

- household scenario comparison
- debt payoff timeline visualisations
- emergency fund planner sliders
- pension contribution what-if modelling
- account-wrapper comparison assistant
- yearly review reminders
- accessibility-first screen-reader mode
- “show me the original flowchart path behind this answer”

---

## 30. Final implementation guidance

To keep the tool authentic:
- treat the UKPF flowchart as the source hierarchy of priorities,
- derive branch answers whenever practical,
- expose assumptions clearly,
- keep user outputs concrete and non-salesy,
- preserve the flowchart’s educational spirit and caution.

The best implementation is one where a UKPF user would say:
“yes, this feels like the flowchart, just easier to apply to my own life.”
