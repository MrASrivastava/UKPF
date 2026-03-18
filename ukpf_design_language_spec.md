# UKPF Flowchart Tool — Colour Theme & Design Language Spec

## Purpose

This document analyses the visual character of the current UK Personal Finance flowchart properties and translates that into a practical design language for a new tool that should feel authentically aligned with the original experience.

This spec is intentionally **stylistic rather than brand-official**. It is based on a visual audit of the current image flowchart and the interactive wiki page, and is designed to preserve their character while making the new tool more usable, more interactive, and more insight-driven.

---

## 1. Source Character Summary

The original properties have two related but slightly different visual modes:

### A. The flowchart image version
This is the strongest visual reference. It has:
- a light neutral page background
- a vertically structured decision map
- pastel-coloured step zones
- thin dark borders
- black arrows and connectors
- small, dense, practical text
- very little decoration
- a clear “information map” feel rather than an “app dashboard” feel

### B. The wiki / interactive page
This feels more like a practical knowledge base:
- content-first
- simple WordPress-style typography and links
- low visual drama
- plain spacing
- high clarity
- stronger emphasis on reading than on product polish

Your tool should borrow more heavily from the **flowchart image version** for colour and structural identity, while borrowing from the **wiki page** for clarity, accessibility, and calm information delivery.

---

## 2. Design Intent for Your Tool

The tool should feel like:

- a **guided financial map**
- a **calm public-interest utility**
- a **decision journey**
- a **serious but friendly educational product**

It should **not** feel like:

- a flashy fintech app
- a neon budgeting dashboard
- a luxury wealth-management product
- a gamified consumer app
- a generic SaaS admin panel

The emotional tone should be:

- calm
- reassuring
- non-judgmental
- practical
- trustworthy
- slightly academic / reference-like
- quietly structured

---

## 3. Core Visual Principles to Preserve

## 3.1 Low-gloss, high-clarity design
The current UKPF properties are visually modest. They do not rely on:
- gradients
- glassmorphism
- glossy cards
- rich illustration
- oversized hero sections
- trendy product marketing tropes

Preserve that restraint.

## 3.2 Colour is used structurally, not decoratively
The most important visual behaviour in the original flowchart is that colour signals **stage and category**, not mood or marketing emphasis.

That means colour in your tool should primarily answer:
- where am I in the sequence?
- what type of checkpoint is this?
- what phase of the journey does this belong to?

## 3.3 Information density is acceptable
The original does not look sparse or luxurious. It accepts that users are here to think, compare, and decide.

Your tool can be cleaner and more spacious, but it should still feel information-rich.

## 3.4 Utility over ornament
Every visual element should earn its place:
- progress markers
- insight cards
- calculation summaries
- next-action prompts
- status labels
- branch indicators

---

## 4. Colour Theme Analysis

## 4.1 Observed palette character

The flowchart uses a sequence of soft pastel blocks with darker related borders. The colours are muted and practical rather than saturated. The main families are:

- muted rose / pink
- soft amber / yellow
- pale green
- pale blue
- soft lavender / violet

These colours correspond to logical stages in the journey and create a strong sense of progression.

The palette is effective because it is:
- visually differentiated
- gentle on the eye
- non-threatening
- easy to scan
- emotionally neutral but not sterile

---

## 4.2 Proposed theme palette for your tool

These values are **implementation-ready approximations** designed to match the visual character of the source flowchart.

### Base neutrals
```css
--bg-page: #efefef;
--bg-surface: #ffffff;
--bg-subtle: #f6f6f6;
--border-default: #c8c8c8;
--text-primary: #1f1f1f;
--text-secondary: #555555;
--text-muted: #767676;
--link: #2b6cb0;
--focus: #1d4ed8;
```

### Step 1 — Budget / crisis / immediate stability
```css
--step1-fill: #efd0d0;
--step1-fill-strong: #e6bcbc;
--step1-border: #c99696;
--step1-band: #e1b5b5;
```

### Step 2 / 3 — emergency buffer / pension bridge
```css
--step2-fill: #f3e3ad;
--step2-fill-strong: #ecd58d;
--step2-border: #c9af63;
--step2-band: #e7d08a;
```

### Step 4 / 5 — debt assessment / full resilience
```css
--step3-fill: #dbeacb;
--step3-fill-strong: #c8ddb4;
--step3-border: #98b07f;
--step3-band: #bfd7a6;
```

### Step 6 — define goals / review budget
```css
--step4-fill: #dce8f6;
--step4-fill-strong: #c8daef;
--step4-border: #98b2cf;
--step4-band: #bfd2ea;
```

### Step 7 / 8 — future goals / long-term investing
```css
--step5-fill: #ddd4f2;
--step5-fill-strong: #cfc2ea;
--step5-border: #9f95c6;
--step5-band: #c2b4e4;
```

### Status overlays
These are for modern app states while staying in character.
```css
--status-critical-bg: #f7dada;
--status-critical-border: #c97b7b;

--status-warning-bg: #f6edc8;
--status-warning-border: #c7aa53;

--status-progress-bg: #dfead5;
--status-progress-border: #8fad7e;

--status-info-bg: #dfe9f5;
--status-info-border: #90aac8;
```

---

## 4.3 Colour usage rules

### Use the stage colours for:
- section banners
- step pills
- active journey rail markers
- checkpoint headers
- step summary cards
- branch grouping panels

### Use neutrals for:
- main content surfaces
- calculator cards
- text-heavy explanations
- form fields
- global page background

### Use status colours sparingly for:
- blocked states
- warnings
- progress achieved
- readiness summaries

### Do not:
- flood the whole page with pastel colour
- use gradients
- use very saturated fintech greens/blues
- use black backgrounds
- make every card a different colour at once

The tool should look **ordered**, not rainbow-like.

---

## 5. Stage Mapping Recommendation

To stay faithful, the product should visibly move through the same stage families as the flowchart.

### Stage A — Foundations / stability
Use rose and warm blush tones.

Typical checkpoints:
- budget
- priority bills
- debt distress
- minimum payments
- crisis support

### Stage B — Starter resilience
Use warm yellow / amber tones.

Typical checkpoints:
- starter emergency fund
- pension enrolment / employer match

### Stage C — Mid-foundation optimisation
Use pale green tones.

Typical checkpoints:
- bad debt
- emergency fund expansion
- debt review

### Stage D — Goal framing
Use pale blue tones.

Typical checkpoints:
- review budget
- define goals
- classify horizon

### Stage E — Future planning
Use lavender / violet tones.

Typical checkpoints:
- short-term goals
- long-term investing
- pre-pension vs post-pension allocation
- wrapper selection summaries

This staged colouring is one of the strongest ways to keep the original identity alive.

---

## 6. Typography

## 6.1 General direction
The source experience reads like a practical web reference, not a designed editorial magazine. Typography should therefore be:

- simple
- highly legible
- neutral
- compact enough for dense information
- not overly stylised

## 6.2 Recommended font stack
Use a system-first sans serif stack:

```css
font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

If you want an even more utilitarian feel, you can use:

```css
font-family: Arial, Helvetica, sans-serif;
```

Inter is the safer modern implementation choice because it preserves clarity while still feeling understated.

## 6.3 Typography scale
Suggested scale:

```css
--text-xs: 12px;
--text-sm: 14px;
--text-md: 16px;
--text-lg: 18px;
--text-xl: 22px;
--text-2xl: 28px;
```

### Weight recommendations
- page titles: 700
- section headers: 600
- card titles: 600
- body text: 400
- labels / metadata: 500

## 6.4 Tone rules
Text should feel:
- plain English
- directly useful
- calm
- non-performative

Avoid highly branded microcopy or startup-style hype.

---

## 7. Layout Language

## 7.1 Core layout feel
The original flowchart is strongly vertical and sequential. Your tool should preserve a sense of downward or forward progress.

Recommended layout model:
- left journey rail or top journey path
- central reading / interaction column
- supporting insight panel on desktop
- compact stacked flow on mobile

## 7.2 Preferred page structure
Desktop:
- header
- progress band
- main 2-column body
  - primary checkpoint panel
  - secondary “Your numbers so far” or “Journey trail” panel

Mobile:
- stacked flow
- checkpoint card first
- expandable journey trail below
- sticky next-step footer

## 7.3 Spacing style
The source is compact, but your tool should modernise slightly.

Suggested spacing system:
```css
--space-1: 4px;
--space-2: 8px;
--space-3: 12px;
--space-4: 16px;
--space-5: 24px;
--space-6: 32px;
--space-7: 40px;
```

Use space to create clarity, not luxury.

---

## 8. Component Design Language

## 8.1 Checkpoint cards
Checkpoint cards should be the heart of the experience.

Style:
- white or very light neutral body
- thin border
- coloured top band or header strip mapped to current stage
- minimal shadow or no shadow
- square or gently rounded corners only

Recommended card shape:
```css
border-radius: 8px;
border: 1px solid var(--border-default);
box-shadow: none;
```

Optional:
```css
box-shadow: 0 1px 2px rgba(0,0,0,0.04);
```

Do not use deep, floating SaaS shadows.

## 8.2 Progress rail
The progress rail should feel like a modern translation of the left-hand coloured stage bars in the original flowchart.

Use:
- stacked stage blocks
- current step highlight
- completed step ticks
- current location marker
- subtle numerical snapshot under each stage

## 8.3 Insight cards
These are your main enhancement over the original.

Style:
- neutral or lightly tinted background
- thin border
- short title
- large key number
- one short explanatory sentence

Example card types:
- status
- gap
- opportunity
- urgency
- trade-off
- progress

## 8.4 Decision prompts
Question blocks should visually echo flowchart decision diamonds without literally drawing diamonds everywhere.

Suggested translation:
- centered question heading
- “Yes / No / Unsure” action group
- optional small note below
- branch preview hint

You can use a subtle diamond icon or angular accent, but avoid turning the UI into clip-art.

## 8.5 Buttons
Buttons should be clear and understated.

Primary button:
- filled with current stage colour border pair
- dark text
- medium weight
- no flashy gradient

Secondary button:
- white background
- thin border
- dark text

Example:
```css
border-radius: 8px;
padding: 10px 14px;
border: 1px solid currentColor;
```

## 8.6 Form fields
Fields should feel practical and safe:
- white fill
- medium contrast border
- dark text
- clear focus state
- no floating-label gimmicks required

## 8.7 Tags and status pills
Use small labelled pills for:
- Critical
- Needs attention
- In progress
- Strong
- Estimate
- Confirmed

These are useful for progress visibility without breaking the restrained tone.

---

## 9. Iconography & Graphics

## 9.1 Icon style
Use icons sparingly and keep them simple:
- outlined or lightly filled
- consistent stroke weight
- non-cartoonish
- mostly functional

Good icon uses:
- warning
- info
- progress
- calculator
- goal
- savings
- pension
- debt
- timeline

## 9.2 Graphics
Do not use hero illustrations or mascot-style visuals.

If you use diagrams, prefer:
- simple flow arrows
- compact step maps
- small progress visuals
- minimal charts
- timeline markers

Your strongest “graphic” should be the journey structure itself.

---

## 10. Interaction Design Language

## 10.1 Behaviour style
The interaction should feel:
- sequential
- calm
- explainable
- lightly guided
- reversible

The user should always know:
- where they are
- what this step means
- what changed numerically
- what comes next

## 10.2 Progress feedback
After each checkpoint, show:
- step completed
- updated readiness state
- one key new number learned
- one next action

Example:
- “You now know your monthly surplus.”
- “Your starter emergency fund gap is now quantified.”
- “Next: check whether you are missing employer pension match.”

## 10.3 Reveal strategy
Use progressive disclosure:
- short summary first
- “see the maths” expansion
- “why this matters” explanation
- “advanced details” in Deep Mode

This fits the wiki’s educational nature and prevents visual overload.

---

## 11. Accessibility & Usability Rules

The interactive wiki page explicitly positions itself as the screen-reader-compatible version, so your tool should preserve that spirit.

### Requirements
- keyboard navigable
- strong focus states
- semantic headings
- plain-language labels
- sufficient contrast for text and interactive controls
- mobile-first readability
- no colour-only meaning
- progress states also labelled in text

### Important note
The pastel stage colours are part of the identity, but they should sit behind readable dark text and should not be the only signal.

---

## 12. Recommended Modernisation Moves

These changes keep the spirit while improving usability.

## 12.1 Add a persistent “journey trail”
A summary strip showing:
- monthly surplus / deficit
- emergency fund months
- highest APR debt
- pension match status
- goals defined

This is a modern enhancement that fits the original logic.

## 12.2 Add checkpoint summaries
At the end of each step:
- what you learned
- what changed
- what matters now
- what is next

## 12.3 Add expandable insight cards
This lets you enrich the flowchart with numbers while preserving clarity.

## 12.4 Add “map view” and “step view”
Map view:
- overall flowchart structure
- good for orientation

Step view:
- one checkpoint at a time
- better for completion

This is a strong way to remain faithful to the original while making the experience usable.

---

## 13. Things You Should Explicitly Avoid

Do not turn this into:
- a dark fintech app
- a neon modern trading UI
- a glossy personal wealth dashboard
- a luxury planning tool
- a heavily animated mobile-first startup aesthetic
- a gamified streak-based experience
- a cartoon educational app

Avoid:
- oversized rounded blobs
- strong drop shadows
- intense gradients
- glass blur
- saturated greens and blues
- excessive emoji
- giant empty spaces
- marketing-style hero copy

The product should feel like a **trusted decision map**, not a sales surface.

---

## 14. Suggested CSS Token Layer

```css
:root {
  --bg-page: #efefef;
  --bg-surface: #ffffff;
  --bg-subtle: #f6f6f6;

  --text-primary: #1f1f1f;
  --text-secondary: #555555;
  --text-muted: #767676;

  --border-default: #c8c8c8;
  --link: #2b6cb0;
  --focus: #1d4ed8;

  --step1-fill: #efd0d0;
  --step1-fill-strong: #e6bcbc;
  --step1-border: #c99696;
  --step1-band: #e1b5b5;

  --step2-fill: #f3e3ad;
  --step2-fill-strong: #ecd58d;
  --step2-border: #c9af63;
  --step2-band: #e7d08a;

  --step3-fill: #dbeacb;
  --step3-fill-strong: #c8ddb4;
  --step3-border: #98b07f;
  --step3-band: #bfd7a6;

  --step4-fill: #dce8f6;
  --step4-fill-strong: #c8daef;
  --step4-border: #98b2cf;
  --step4-band: #bfd2ea;

  --step5-fill: #ddd4f2;
  --step5-fill-strong: #cfc2ea;
  --step5-border: #9f95c6;
  --step5-band: #c2b4e4;

  --status-critical-bg: #f7dada;
  --status-critical-border: #c97b7b;
  --status-warning-bg: #f6edc8;
  --status-warning-border: #c7aa53;
  --status-progress-bg: #dfead5;
  --status-progress-border: #8fad7e;
  --status-info-bg: #dfe9f5;
  --status-info-border: #90aac8;

  --radius-sm: 6px;
  --radius-md: 8px;

  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;

  --text-xs: 12px;
  --text-sm: 14px;
  --text-md: 16px;
  --text-lg: 18px;
  --text-xl: 22px;
  --text-2xl: 28px;
}
```

---

## 15. Suggested One-Line Design Direction

If you need a single sentence to guide implementation, use this:

**Build it like a calm, pastel-coded financial decision map: more usable and insightful than the original, but still restrained, practical, sequential, and reference-like.**

---

## 16. Final Recommendation

For authenticity, your tool should be designed as:

- **a modernised flowchart utility**
- not a reinvented brand system

That means:
- keep the pastel stage progression
- keep the neutral reading-first UI
- keep the low-gloss restraint
- add just enough structure, hierarchy, and insight to make the journey genuinely more actionable

The best result will feel as though the original UKPF flowchart has been carefully translated into a living, interactive product rather than visually “rebranded”.
