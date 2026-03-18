# UK Personal Finance Flowchart — `rules.md`

Source basis: UKPersonalFinance flowchart page and the linked image version, current version 3.0.10, last updated 2025-12-22. This file is a structured interpretation of the flowchart logic for product/design use. It is intended to stay faithful to the original flowchart and linked wiki pages, while expressing the journey as explicit rules and decision nodes rather than as a visual diagram.

## Purpose

This file converts the UK Personal Finance Flowchart into a machine-friendly decision model for building an interactive experience that remains aligned with the original UKPF logic. The priority is to:

1. preserve the order of decisions,
2. preserve the gating questions,
3. preserve the recommended action at each branch,
4. preserve the linked topic pages for deeper guidance,
5. avoid adding new financial advice beyond the flowchart.

## Canonical source

- Interactive flowchart page: `https://ukpersonal.finance/flowchart/`
- Image version: `https://flowchart.ukpersonal.finance`
- Version observed: `3.0.10`
- Last updated observed: `2025-12-22`

## Design principles for an interactive rebuild

- Treat the flowchart as a decision engine, not just a content page.
- Each question should be a discrete node with a yes/no or categorical answer.
- Each action node should show:
  - the recommended action,
  - why it appears at that stage,
  - the original UKPF wiki link,
  - the next question or destination.
- Preserve the original ordering of steps 1 through 8.
- Keep the UKPF disclaimer visible.
- Credit UKPersonalFinance and retain the original CC BY-NC-SA 4.0 licence terms for any non-commercial derivative based on their work.

## Global assumptions

These assumptions are implicit in the flowchart and should be made explicit in an interactive product:

- The user is dealing with personal finance in a UK context.
- The flow starts from basic financial stability before optimising investments.
- Expensive debt is generally prioritised before medium- and long-term investing.
- Emergency resilience is built in two stages: an initial emergency fund, then a fuller one.
- Pension matching is treated as a high-priority step once immediate crisis issues are controlled.
- Short-term and long-term goals are separated, with under-5-year needs generally pushed toward cash-like/savings options and over-5-year needs toward long-term investing.
- Mortgage and student-loan decisions are treated differently from other debts.

## Required disclaimer

Show this or equivalent text prominently in any interactive version:

> This is for information only and should not be taken as financial advice. Always do your own research and make fully informed decisions.

---

## Rule model

## Step 0 — Start here

### Node `start`
**Intent:** entry point and orientation.

**Display guidance:**
- A starting point for your financial planning journey.
- Overwhelmed? Take your time, one step at a time.
- Read the wiki and ask questions in the UKPF community.

**Next:** `step_1_budget`

---

## Step 1 — Budget, essential bills, support, and crisis triage

### Node `step_1_budget`
**Title:** Budget. Pay bills, necessary expenses, and expensive debts.

**Primary actions:**
- Create a budget.
- Check eligibility for state financial support.
- Insure essentials such as car and home; consider life and income protection as relevant.
- Make minimum payments on all debts.
- Prioritise important bills, including examples named on the flowchart:
  - Council tax
  - Food
  - Mortgage / rent
  - Transport for work

**Linked topics:**
- Budgeting
- Benefit entitlement
- Insurance
- Debt repayment

**Next question:** `q_rely_on_credit_for_essentials`

### Node `q_rely_on_credit_for_essentials`
**Question:** Do you rely on credit cards or loans for essentials?

**If yes →** `step_1_crisis_support`

**If no →** `q_any_debt_over_10_apr`

### Node `step_1_crisis_support`
**Title:** Immediate affordability / problem debt support.

**Actions:**
- Prioritise important bills.
- Seek debt counselling from a reputable charity.
- Continue minimum payments where possible.
- Cut back where feasible.

**Intent:** this branch handles financial distress before optimisation.

**Linked topics:**
- Problem debt
- Debt repayment
- Budgeting / living costs

**Loop:** after stabilisation, return to `q_any_debt_over_10_apr`

### Node `q_any_debt_over_10_apr`
**Question:** Do you have any debt over 10% APR?

**If yes →** `step_1_overpay_expensive_debt`

**If no →** `step_2_initial_emergency_fund`

### Node `step_1_overpay_expensive_debt`
**Title:** Overpay expensive debt.

**Actions:**
- Overpay debts, focusing on the highest interest rates.
- Refinance to cheaper rates when available.

**Linked topic:**
- Debt repayment

**Loop:** remain here until answer to `q_any_debt_over_10_apr` becomes `no`

---

## Step 2 — Initial emergency fund

### Node `step_2_initial_emergency_fund`
**Title:** Emergency fund.

**Action:** Build an initial emergency fund of 1–3 months of outgoings.

**Why this is here:** after immediate affordability and very expensive debt are addressed, the user should gain some cash resilience before moving on.

**Linked topic:**
- Emergency fund

**Next:** `step_3_pension_enrolment`

---

## Step 3 — Pension enrolment / employer match

### Node `step_3_pension_enrolment`
**Title:** Pension enrolment.

**Action:** Ensure you are auto-enrolled in your workplace pension and contribute enough to receive the maximum employer match, if affordable.

**Linked topic:**
- Pensions

**Next:** `step_4_assess_debts`

---

## Step 4 — Assess debts other than mortgage or student loan

### Node `step_4_assess_debts`
**Title:** Assess debts.

**Question:** Do you have any debt other than a mortgage or student loan?

**If yes →** `step_4_debt_schedule`

**If no →** `step_5_full_emergency_fund`

### Node `step_4_debt_schedule`
**Title:** Make a debt repayment schedule.

**Actions:**
- Make a debt repayment schedule.
- Take into account interest rates available for savings and debt.

**Linked topic:**
- Debt repayment

**Next:** `step_5_full_emergency_fund`

---

## Step 5 — Full emergency fund

### Node `step_5_full_emergency_fund`
**Title:** Full emergency fund.

**Action:** Build emergency fund to 3–12 months of outgoings, depending on personal circumstances.

**Linked topic:**
- Emergency fund

**Next:** `step_6_define_goals`

---

## Step 6 — Define goals and rebalance budget

### Node `step_6_define_goals`
**Title:** Define goals.

**Actions:**
- Review your budget.
- You may now be in a better position to increase discretionary spending if you wish.
- Define your financial goals, including the amounts needed and target dates.

**Linked topics:**
- Budgeting
- Defining your goals

**Next:** `step_7_short_term_goals`

---

## Step 7 — Short-term goals under 5 years

### Node `step_7_short_term_goals`
**Title:** Short-term goals (<5 years).

**Question:** Are your short-term goals on track?

**If no →** `step_7_save_for_short_term_goals`

**If yes →** `step_8_long_term_goals`

### Node `step_7_save_for_short_term_goals`
**Title:** Save for goals within 5 years.

**Suggested focus areas:**
- Cash LISA for a first-home deposit for a property under £450k.
- Savings accounts.
- Premium Bonds.

**Linked topics:**
- Savings accounts
- Lifetime ISA

**Loop:** once short-term goals are on track, proceed to `step_8_long_term_goals`

---

## Step 8 — Long-term goals over 5 years

### Node `step_8_long_term_goals`
**Title:** Long-term goals (>5 years).

**Question split:**
- Is savings required before pension access age (about 58)?
- Or is savings required after pension access age?

This is the core branching decision in the long-term section.

### Node `q_savings_before_pension_access_age`
**Question:** Is the money needed before pension access age (~58)?

**If yes →** `step_8_pre_pension_long_term_savings`

**If no →** `q_any_remaining_debt`

### Node `step_8_pre_pension_long_term_savings`
**Title:** Long-term saving/investing before pension access age.

**Suggested focus areas:**
- Stocks and Shares ISA.
- Stocks and Shares LISA for first-home deposit use under the property cap, where appropriate.
- General Investment Account if ISA allowance is already used.

**Linked topics:**
- Investing 101
- ISA
- LISA

**Terminal state:** user is focusing on tax-efficient long-term investing outside pension lock-up constraints.

### Node `q_any_remaining_debt`
**Question:** Do you have any debt?

**If yes →** `step_8_assess_overpayment_benefit`

**If no →** `step_8_post_pension_long_term_investing`

### Node `step_8_assess_overpayment_benefit`
**Title:** Assess overpayment benefit.

**Actions:**
- Assess overpayment benefit based on your goals and preferences.
- For student loans, refer to the student loan guidance.
- For mortgages, refer to mortgage overpayments guidance.

**Linked topics:**
- Student loans
- Mortgage overpayments vs investments

**Next:** `step_8_post_pension_long_term_investing`

### Node `step_8_post_pension_long_term_investing`
**Title:** Long-term investing for money needed after pension access age.

**Suggested focus areas:**
- Workplace pension.
- SIPP, especially if in 40%+ tax brackets and additional relief can be claimed.
- Stocks and Shares LISA, while noting the drawbacks discussed in the wiki.

**Follow-on action:** make long-term investments in low-cost index funds and choose the most tax-efficient accounts for the goal and circumstances.

**Linked topics:**
- Pensions
- ISA vs LISA vs Pension
- Investing 101
- Index funds

**Terminal state:** user is optimising tax-efficient retirement-oriented investing.

---

## Condensed decision tree

```text
START
  -> Step 1: budget, priority bills, support, insurance, minimum debt payments
    -> Q: rely on credit for essentials?
       yes -> crisis support / debt counselling / prioritise bills / cut costs
       no  -> Q: any debt >10% APR?
                 yes -> overpay highest-interest debt, refinance where possible
                 no  -> Step 2: build 1-3 month emergency fund
  -> Step 3: pension enrolment and employer match
  -> Step 4: any debt other than mortgage or student loan?
       yes -> make debt repayment schedule
       no  -> continue
  -> Step 5: build 3-12 month emergency fund
  -> Step 6: define goals and target dates
  -> Step 7: are short-term goals (<5 years) on track?
       no  -> cash LISA / savings / premium bonds
       yes -> continue
  -> Step 8: long-term goals (>5 years)
       -> Q: money needed before pension access age?
          yes -> S&S ISA / S&S LISA / GIA
          no  -> Q: any debt?
                    yes -> assess mortgage or student-loan overpayment benefit
                    no  -> workplace pension / SIPP / S&S LISA
       -> invest long term in low-cost index funds using the most tax-efficient wrapper
```

---

## Suggested data model for an interactive product

```yaml
flowchart:
  id: ukpf_flowchart_v3_0_10
  source_page: https://ukpersonal.finance/flowchart/
  source_image: https://flowchart.ukpersonal.finance
  version: 3.0.10
  last_updated: 2025-12-22
  disclaimer_required: true
  licence: CC-BY-NC-SA-4.0

nodes:
  - id: start
    type: info
    next: step_1_budget

  - id: step_1_budget
    type: action
    links: [budgeting, benefit-entitlement, insurance, debt]
    next: q_rely_on_credit_for_essentials

  - id: q_rely_on_credit_for_essentials
    type: question
    answers:
      yes: step_1_crisis_support
      no: q_any_debt_over_10_apr

  - id: step_1_crisis_support
    type: action
    links: [problem-debt, debt, budgeting]
    next: q_any_debt_over_10_apr

  - id: q_any_debt_over_10_apr
    type: question
    answers:
      yes: step_1_overpay_expensive_debt
      no: step_2_initial_emergency_fund

  - id: step_1_overpay_expensive_debt
    type: action
    links: [debt]
    loop_until: q_any_debt_over_10_apr=no

  - id: step_2_initial_emergency_fund
    type: action
    links: [emergency-fund]
    next: step_3_pension_enrolment

  - id: step_3_pension_enrolment
    type: action
    links: [pensions]
    next: step_4_assess_debts

  - id: step_4_assess_debts
    type: question
    answers:
      yes: step_4_debt_schedule
      no: step_5_full_emergency_fund

  - id: step_4_debt_schedule
    type: action
    links: [debt]
    next: step_5_full_emergency_fund

  - id: step_5_full_emergency_fund
    type: action
    links: [emergency-fund]
    next: step_6_define_goals

  - id: step_6_define_goals
    type: action
    links: [budgeting, goals]
    next: step_7_short_term_goals

  - id: step_7_short_term_goals
    type: question
    answers:
      yes: step_8_long_term_goals
      no: step_7_save_for_short_term_goals

  - id: step_7_save_for_short_term_goals
    type: action
    links: [savings, lisa]
    next: step_8_long_term_goals

  - id: step_8_long_term_goals
    type: question_group
    next: q_savings_before_pension_access_age

  - id: q_savings_before_pension_access_age
    type: question
    answers:
      yes: step_8_pre_pension_long_term_savings
      no: q_any_remaining_debt

  - id: step_8_pre_pension_long_term_savings
    type: action
    links: [investing-101, isa, lisa]
    terminal: true

  - id: q_any_remaining_debt
    type: question
    answers:
      yes: step_8_assess_overpayment_benefit
      no: step_8_post_pension_long_term_investing

  - id: step_8_assess_overpayment_benefit
    type: action
    links: [student-loans, mortgage-overpayments]
    next: step_8_post_pension_long_term_investing

  - id: step_8_post_pension_long_term_investing
    type: action
    links: [pensions, isa-vs-lisa-vs-pension, investing-101, index-funds]
    terminal: true
```

---

## Content fidelity rules

When turning this into an interactive website, enforce these rules:

1. Do not reorder the core stages.
2. Do not jump users to investing before the debt/emergency-fund gates are handled.
3. Keep mortgage and student-loan treatment separate from ordinary consumer debt.
4. Keep short-term goals separate from long-term goals.
5. Keep “before pension access age” and “after pension access age” as separate branches.
6. Surface the relevant UKPF wiki page at each node rather than replacing it with your own unsupported advice.
7. Any explanatory text you add should be labelled as implementation guidance, not as part of the original flowchart.
8. Preserve the UK property cap reference for LISA first-home deposit mentions where the flowchart includes it.
9. Preserve the distinction between initial and full emergency funds.
10. Preserve the special role of workplace pension employer match.
11. Preserve the debt-over-10%-APR gate as a specific early triage question.
12. Preserve the “do you rely on credit for essentials?” branch as an early distress signal.

---

## UX recommendations for your interactive version

These are implementation recommendations, not part of the original flowchart:

### 1. Use a question-first wizard
Ask one question at a time and show:
- where the user is in the flow,
- why the question matters,
- the action they unlock,
- the original UKPF page for details.

### 2. Separate `rule`, `explanation`, and `source`
At every node, structure content like this:
- `rule`: the exact recommendation or gate,
- `explanation`: a brief plain-English explanation,
- `source`: the UKPF page.

### 3. Preserve branch history
Let users see:
- their answers so far,
- the path taken,
- the actions they have already completed,
- what remains next.

### 4. Avoid pretending to personalise financial advice
Phrase output like:
- “Based on the UKPF flowchart, your next priority is…”
- not “You should definitely…”

### 5. Add a “show the original flowchart step” mode
For each node, show:
- original step number,
- original label,
- linked wiki page,
- current path.

---

## Minimal schema for a future app

```ts
export type FlowNodeType = 'info' | 'question' | 'action' | 'question_group';

export interface FlowNode {
  id: string;
  step?: number;
  title: string;
  type: FlowNodeType;
  question?: string;
  actions?: string[];
  links?: string[];
  answers?: Record<string, string>;
  next?: string;
  loopUntil?: string;
  terminal?: boolean;
}
```

---

## Next best deliverables after this file

1. A `flowchart.json` file with every node fully enumerated.
2. A `content_map.md` linking every node to the correct UKPF wiki page.
3. A React decision-tree UI that reads from the JSON rather than hard-coding logic.
4. A “strict fidelity mode” where the app never says more than the source plus short implementation text.
5. A “design notes” file that explicitly lists what is original UKPF logic vs what is your product behaviour.

---

## Source notes

This rules file was derived from the UKPersonalFinance flowchart page, which states:
- the flowchart is clickable and each step links to a detailed page,
- the current version is 3.0.10,
- the last update shown is 2025-12-22,
- the image version lives at `flowchart.ukpersonal.finance`,
- the work is licensed under CC BY-NC-SA 4.0. The page also includes the disclaimer that it is for information only and not financial advice. citeturn172825view0

