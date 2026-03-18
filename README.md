# 💷 UK Personal Finance Flowchart — Interactive Tool

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Version](https://img.shields.io/badge/version-3.0.10-4a90d9)](https://github.com/)
[![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)](https://github.com/)
[![Single File](https://img.shields.io/badge/size-single%20HTML%20file-orange)](./index.html)
[![Vanilla JS](https://img.shields.io/badge/built%20with-vanilla%20JS-f7df1e)](./index.html)

**An interactive, browser-based implementation of the UK Personal Finance Flowchart — eight evidence-based steps from your first budget to your personalised long-term investment strategy.**

Built for the UK. Based on the community-maintained [UKPF Flowchart](https://ukpersonal.finance/flowchart/) (v3.0.10). Runs entirely in your browser — no server, no account, no data sent anywhere.

---

> **⚠️ IMPORTANT DISCLAIMER**
>
> This tool is for **educational and informational purposes only**. It is **not** financial advice and must **not** be treated as such.
>
> - The information presented is generic guidance — your personal circumstances will vary significantly.
> - Always **do your own research** and verify all figures independently before making any financial decision.
> - For decisions involving significant sums, debt restructuring, pension choices, or investment strategy, **consider seeking regulated financial advice** from a qualified financial adviser (FCA-authorised).
> - Tax rules, pension rules, benefit thresholds, and ISA limits can change. Always check current HMRC and government guidance.
> - Past investment performance does not guarantee future results. The value of investments can go down as well as up.
>
> **The authors and contributors accept no liability for financial decisions made using this tool.**

---

## 🌐 Live Demo / Landing Page

Open [`landing.html`](./landing.html) in your browser for the full landing page, or go straight to the tool by opening [`index.html`](./index.html).

No build step. No installation. Just open the file.

---

## ✨ What This Tool Does

This is an interactive guide through the **UKPF Flowchart** — a structured, decision-based financial journey designed for UK residents. It tracks your personal numbers throughout, asks the key questions at each stage, and ends with a personalised investment strategy.

### The Five Stages

| Stage | Colour | Focus |
|-------|--------|-------|
| **A — Foundations** | 🌸 Rose | Budget, essential bills, costly debt |
| **B — Safety Net** | 🟡 Amber | Starter emergency fund, workplace pension enrolment |
| **C — Debt & Buffer** | 🟢 Green | Debt repayment schedule, full emergency fund |
| **D — Goal Planning** | 🔵 Blue | Budget review, defining and classifying financial goals |
| **E — Long-Term Investing** | 🟣 Lavender | Short-term goal saving, long-term investment strategy |

### The Eight Steps

1. **Budget & Pay Essential Bills** — Create a budget, check benefit entitlement, insure essentials, make minimum debt payments
2. **Build Your Initial Emergency Fund** — Save 1–3 months of essential outgoings in an easy-access account
3. **Enrol in Your Workplace Pension** — Capture the full employer match — it's free money
4. **Create a Debt Repayment Schedule** — List every debt; overpay highest-APR first (avalanche method)
5. **Build Your Full Emergency Fund** — Expand to 3–6 months (or 6–12 months if self-employed)
6. **Define Your Financial Goals** — Write down each goal with a target amount and timeline; classify as short-term (<5 yrs) or long-term
7. **Save for Short-Term Goals** — Cash ISAs, easy-access savings, Premium Bonds, fixed-rate accounts
8. **Long-Term Investing** — Stocks & Shares ISA, SIPP, Workplace Pension, LISA — tailored to your timeline

### Two Personalised Outcomes

The journey ends with one of two investment strategies, based on whether you need access to your money before pension access age (~58):

- **Outcome A** — Stocks & Shares ISA–first (flexible, for pre-pension goals)
- **Outcome B** — Pension–first (for retirement-only saving, maximum tax efficiency)

---

## 🛠 Features

| Feature | Description |
|---------|-------------|
| 📊 **Live Budget Analysis** | Enter income, essential spend, savings, and discretionary spend — surplus is calculated in real time |
| 🏦 **Emergency Fund Tracker** | See your fund in months of essential spending, with clear targets |
| 💳 **Debt Scheduler** | Add each debt with balance, APR, and minimum payment; highest APR flagged immediately |
| 💼 **Pension Match Optimiser** | See exactly what employer match you're leaving on the table |
| 🎯 **Goal Planner** | Add unlimited goals with target amounts and years; monthly saving required computed live |
| 📈 **Goals Allocation Chart** | Visual stacked bar: Essential · Savings · Goals · Discretionary · Surplus |
| 🧠 **Smart Insight Cards** | Contextual alerts, progress indicators, and personalised notes at every step |
| 🗺 **Living Sidebar** | Nine key metrics (income, surplus, emergency fund, APR, pension match, goals) updated live |
| 📄 **Downloadable PDF** | Professional print report: key numbers, goals table, allocation chart, priority actions, investment strategy |
| 💾 **Auto-Save** | Progress saved automatically to `localStorage` — pick up where you left off |
| 🔒 **Fully Private** | Nothing is sent anywhere. All data stays in your browser. Zero analytics, zero tracking |

---

## 🚀 Getting Started

### Option 1 — Download and open (simplest)

1. Click **`Code → Download ZIP`** on this repository page
2. Unzip the folder
3. Open **`index.html`** in any modern browser (Chrome, Firefox, Edge, Safari)
4. That's it — no installation required

### Option 2 — Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/UKPF.git
cd UKPF
# Open index.html in your browser
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

### Option 3 — Fork and host on GitHub Pages

1. **Fork** this repository (top-right button on GitHub)
2. Go to **Settings → Pages**
3. Under **Source**, select `main` branch, root folder (`/`)
4. Click **Save** — your site will be live at `https://YOUR-USERNAME.github.io/UKPF/`

The landing page will be served at `/landing.html` and the tool at `/index.html`.

---

## 📁 File Structure

```
UKPF/
├── index.html          ← The interactive flowchart tool (single file, ~2,800 lines)
├── landing.html        ← Marketing landing page
├── README.md           ← This file
├── .gitignore
│
├── ukpf_flow_spec.md           ← Node/decision tree specification
├── ukpf_checkpoint_calculation_spec.md  ← Metrics calculation spec
├── ukpf_design_language_spec.md         ← Design system specification
└── rules.md                    ← Development guidelines
```

**The entire interactive tool is a single, self-contained HTML file.** It has:
- Zero external dependencies (no npm, no frameworks, no CDN calls at runtime)
- No backend or server required
- `localStorage` for persistence (clears when you clear browser data)
- Works fully offline after first load (the only external call is Google Fonts for Inter)

---

## 🔧 Customisation & Development

The tool is intentionally a single HTML file — CSS, JavaScript, and HTML all in one place — to make it trivially easy to fork, inspect, and adapt.

### Key sections inside `index.html`

| Section | What it does |
|---------|-------------|
| CSS custom properties (`--s1` … `--s5`) | Stage colour palette — edit these to retheme |
| `const NODES = { … }` | The full decision tree — all steps, questions, and outcomes |
| `calculateMetrics()` | Derives all financial metrics from user inputs |
| `getInsightCards(nodeId)` | Returns personalised insight cards per step |
| `renderTrail()` | Builds the live sidebar numbers |
| `buildPrintReport()` | Generates the PDF print report HTML |
| `renderGoalsChart()` | Draws the income allocation bar chart |

### Running a local dev server

If you prefer a server (needed for some browser security policies):

```bash
# Python 3
python -m http.server 3737

# Node.js (npx)
npx serve .

# Then open: http://localhost:3737/index.html
```

---

## 📖 Based On / Attribution

This tool is an interactive implementation of the **UK Personal Finance Flowchart**, maintained and published by the UK Personal Finance community.

| Resource | Link |
|----------|------|
| UKPF Flowchart | [ukpersonal.finance/flowchart](https://ukpersonal.finance/flowchart/) |
| Budgeting | [ukpersonal.finance/budgeting](https://ukpersonal.finance/budgeting/) |
| Emergency Fund | [ukpersonal.finance/emergency-fund](https://ukpersonal.finance/emergency-fund/) |
| Pensions | [ukpersonal.finance/pensions](https://ukpersonal.finance/pensions/) |
| ISA Guide | [ukpersonal.finance/isa](https://ukpersonal.finance/isa/) |
| Lifetime ISA | [ukpersonal.finance/lifetime-isa](https://ukpersonal.finance/lifetime-isa/) |
| Debt | [ukpersonal.finance/debt](https://ukpersonal.finance/debt/) |
| Investing | [ukpersonal.finance/investing](https://ukpersonal.finance/investing/) |
| Index Funds | [ukpersonal.finance/index-funds](https://ukpersonal.finance/index-funds/) |
| Student Loans | [ukpersonal.finance/student-loans](https://ukpersonal.finance/student-loans/) |

The original flowchart content is the work of the UKPF community and is reproduced here under its Creative Commons licence. Please visit [ukpersonal.finance](https://ukpersonal.finance/) for the authoritative, up-to-date version of all guidance.

---

## ⚖️ Licence

This project is licensed under the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International** licence, inheriting the licence of the original UKPF Flowchart.

[![CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**You are free to:**
- ✅ **Share** — copy and redistribute the material in any medium or format
- ✅ **Adapt** — remix, transform, and build upon the material

**Under the following terms:**
- 📛 **Attribution** — You must give appropriate credit to the UKPF community and link to [ukpersonal.finance](https://ukpersonal.finance/)
- 🚫 **NonCommercial** — You may not use the material for commercial purposes
- 🔄 **ShareAlike** — If you remix or transform this, you must distribute under the same CC BY-NC-SA 4.0 licence

[Full licence text →](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode)

---

## 🙏 Contributing

Contributions are welcome, subject to the licence terms above.

**Good contributions include:**
- Fixes to calculation errors or logic bugs
- Updated figures (ISA limits, pension thresholds, LISA rules, etc.) when HMRC/government guidance changes
- Accessibility improvements
- Additional insight cards for edge cases
- UI/UX improvements that keep the tool focused and uncluttered

**Please do not:**
- Add tracking, analytics, or any external data collection
- Introduce framework dependencies (the zero-dependency philosophy is intentional)
- Make changes that alter the fundamental UKPF flowchart logic without community rationale

Open an issue first for significant changes so the direction can be discussed before you invest time writing code.

---

## 🔍 Keywords

*For discoverability: UK personal finance, UKPF flowchart, UK budgeting tool, UK emergency fund calculator, ISA guide UK, S&S ISA, Stocks and Shares ISA, SIPP calculator, workplace pension UK, debt avalanche UK, UK financial planning, personal finance UK free tool, r/UKPersonalFinance, interactive finance flowchart, UK investing guide, index funds UK, financial independence UK, FIRE UK, how to save money UK, UK money management.*

---

*Not financial advice. Always do your own research. Consider regulated financial advice for significant decisions.*
