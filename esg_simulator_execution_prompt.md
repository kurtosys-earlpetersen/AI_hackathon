# Execution Prompt: Interactive ESG & Carbon Impact Simulator

## Source Brief

Use the supplied brief screenshot as the product brief for the build:

- Brief: **Brief B**
- Title: **Interactive ESG & Carbon Impact Simulator**
- Team selection: **Team 1**
- Concept: Make ESG transparency tangible rather than abstract numbers on a product page.
- Engineering goal: Build an interactive client slider component where typing an investment value dynamically reads a portfolio asset weight array, computes proportional real-world offsets such as carbon and water, and transforms the results into visual custom CSS or SVG progress graphics.
- Data schema rule: Any mock data must conform to existing Kurtosys API schema definitions.

Reference screenshot path:

```text
/Users/earl.petersen/.cursor/projects/Users-earl-petersen-Library-CloudStorage-OneDrive-Kurtosys-Kurtosys-Clients-Miscellaneous-AI-hackathon/assets/image-5ab8151c-5bdf-4042-a1f0-b44c88bcb7d7.png
```

## Task

Update or rebuild `esg_simulator.html` into a polished, self-contained prototype for an **SSGA / State Street Investment Management ESG & Carbon Impact Simulator**.

The final page must feel like it belongs on `ssga.com`: institutional, precise, spacious, data-led, restrained, and credible. It should not look like a generic hackathon dashboard. Prioritize clarity, trust, and fund-product storytelling over decorative effects.

## Brand And Visual Direction

Use `ssga.com` and State Street Investment Management as the look-and-feel reference.

Design cues to apply:

- Use a light institutional UI by default: white, off-white, pale grey, deep navy, State Street-style blue accents, muted slate text, and restrained chart colors.
- Use strong editorial hierarchy: small uppercase eyebrow labels, large confident headings, compact explanatory copy, and generous whitespace.
- Include an SSGA-style hero section with a line inspired by the site messaging, for example: **"Getting there starts here"**.
- Use clean cards, subtle borders, thin dividers, and sharp data panels instead of dark glassmorphism.
- Use accessible color contrast and avoid excessive gradients, glow effects, or gamified visuals.
- Keep the tone institutional and compliance-aware.

Suggested palette:

- Deep navy: `#001E42`
- SSGA blue: `#005EB8`
- Bright link/action blue: `#0072CE`
- Light blue tint: `#EAF4FF`
- Background: `#F7F9FB`
- Surface: `#FFFFFF`
- Border: `#D8E0E8`
- Text: `#1F2933`
- Secondary text: `#5D6B7A`
- Positive / lower impact: `#2E7D5B`
- Warning / estimated data: `#B7791F`
- Risk / high impact: `#B42318`

## Font Assets

Use the supplied font archives:

- `Inter.zip`
- `Sharp Grotesk Font Family.zip`

If the archives are available in the working directory, extract them into a local `fonts/` directory and load them with `@font-face`.

Font usage:

- Use **Sharp Grotesk** for hero headings, major section headings, and large metric numerals where licensing/files allow.
- Use **Inter** for body text, form controls, tables, labels, and chart annotations.
- Fallbacks:
  - Heading fallback: `Arial`, `Helvetica Neue`, sans-serif.
  - Body fallback: `Inter`, `Arial`, sans-serif.

Do not rely on Google Fonts or external font CDNs. The prototype should work offline once the local font files are present.

## Existing File Context

The current `esg_simulator.html` is a self-contained static HTML/CSS/JS prototype with:

- Sector allocation sliders.
- Preset scenarios.
- ESG and carbon KPIs.
- A benchmark comparison.
- Donut and quadrant visuals.
- Mock sector-level carbon values.

You may preserve the single-file approach, but redesign the page to align with SSGA and correct the data assumptions below.

## Required Jira / Confluence Context

Incorporate the following findings directly into the implementation and/or explanatory UI copy.

### SSGA Sustainability Schema

The SSGA `nexus_sustainability` dataset is sourced from `VWS_ESG_PORTFOLIO_CHARACTERISTICS`.

It provides **portfolio-level sustainability metrics**, not per-holding ESG metrics.

Available ESG/climate items include:

- Climate Metrics
- Brown Revenues
- Potential Emissions
- Green Bonds
- Green/Fossil Fuel Revenue Ratio
- SBTi Targets
- Low Carbon Transition Score
- Carbon Risk Rating
- Carbon Footprint
- Total Carbon Emissions
- Weighted Average Carbon Intensity
- Implied Temperature Rise
- Climate Value at Risk
- Product Involvement & Controversy
- R-Factor

### Water Data Constraint

No water intensity or water stress field currently exists in the SSGA `nexus_sustainability` schema.

The brief mentions "carbon, water", but water must be treated as one of the following:

- Hidden entirely from the primary calculator, or
- Shown as a clearly marked **future / illustrative extension**, not as an available SSGA production metric.

If included, water must be visually labelled:

> Illustrative future metric. Water stress is not currently present in the SSGA `nexus_sustainability` schema.

A reasonable future mock shape is:

```js
{
  portfolioWaterStress: 0.0,
  benchmarkWaterStress: 0.0,
  coveragePct: 0.0,
  difference: 0.0
}
```

Do not imply that SSGA currently provides water data through the same API.

### Holdings / Asset Weight Constraint

The SSGA Nexus repo has separate apps:

- Sustainability app:
  - Dataset: `nexus_sustainability`
  - Input: `CRS_FUND_ALIAS`
  - Returns portfolio-level summary metrics.
- Holdings app:
  - Dataset: `nexus_holdings_view` / `nexus_holdings_export`
  - Input: `FUND_ID`
  - Returns individual positions such as instrument name, `portfolio_weight`, sector, and market.

There is no endpoint that returns:

```js
[
  {
    identifier: "...",
    weight: 0.0,
    carbonFootprint: 0.0
  }
]
```

The simulator may show a conceptual allocation or investment input, but the carbon calculation must be presented as using **already-weighted portfolio summary metrics** from `nexus_sustainability`. If sector sliders are retained, label them as an illustrative scenario overlay rather than a true Kurtosys sustainability API calculation.

## Required Mock Data

Use the following actual carbon values as the primary mock dataset.

Fund context:

- Fund: State Street World ESG Index Equity Fund - A
- Period end: 31-Jan-25
- Benchmark: Bloomberg MSCI US Corporate/Government ESG Custom Index

Carbon Footprint, tCO2e / $M EVIC:

| Scope | Portfolio | Portfolio Coverage | Benchmark | Benchmark Coverage |
| --- | ---: | ---: | ---: | ---: |
| Scope 1+2+3 | 216.99 | 84.78% | 215.63 | 86.16% |
| Scope 1+2 | 58.83 | 92.88% | 57.59 | 94.75% |
| Scope 1 | 51.53 | 92.88% | 50.54 | 94.75% |
| Scope 2 | 7.30 | 92.88% | 7.05 | 94.75% |
| Scope 3 | 181.49 | 88.76% | 178.52 | 90.20% |

Total Carbon Emissions:

| Scope | Portfolio | Benchmark |
| --- | ---: | ---: |
| Scope 1 | 136,569.39 | 334,182.89 |
| Scope 2 | 19,344.25 | 46,585.24 |
| Scope 3 | 459,676.79 | 1,123,736.10 |
| Scope 1+2 | 155,914.61 | 380,770.07 |

Other climate metrics:

| Metric | Portfolio | Benchmark |
| --- | ---: | ---: |
| Carbon Risk Rating | 56.34 | 56.45 |
| Low Carbon Transition Score | 6.01 | 6.01 |
| Implied Temperature Rise | 2.33°C | Not available |
| Brown Revenues | 2.48% | 2.38% |

## Interaction Requirements

Build the simulator around a client-entered investment amount.

Required controls:

- Investment amount input, with currency formatting.
- Scope selector:
  - Scope 1
  - Scope 2
  - Scope 3
  - Scope 1+2
  - Scope 1+2+3
- Optional scenario selector:
  - Current portfolio
  - Lower-carbon tilt
  - Benchmark comparison
  - Paris-aligned illustrative strategy

Required computed outputs:

- Selected carbon footprint metric in `tCO2e / $M EVIC`.
- Portfolio vs benchmark difference.
- Coverage percentage.
- Estimated financed-emissions-style impact scaled by the entered investment value.
- A plain-English impact explanation, for example:
  - "For a $100,000 investment, this scenario maps to an estimated X tCO2e using the selected portfolio carbon-footprint intensity."

Important calculation guidance:

- Carbon footprint is an intensity metric. Treat investment scaling as an educational approximation, not a production financed-emissions methodology.
- Make the methodology visible in an expandable or side-panel note.
- Clearly state that production values come from portfolio-level SSGA sustainability data.

## Visual Requirements

Include these UI areas:

- Hero section:
  - SSGA-style eyebrow.
  - Main title: **Interactive ESG & Carbon Impact Simulator**.
  - Short explanatory text connecting investment amount to portfolio-level carbon transparency.
- Input panel:
  - Investment amount.
  - Scope selector.
  - Scenario selector.
- Results panel:
  - Main carbon impact number.
  - Portfolio vs benchmark comparison.
  - Coverage.
  - Carbon risk rating.
  - Temperature alignment.
- SVG or CSS progress graphics:
  - Portfolio vs benchmark horizontal comparison bar.
  - Scope breakdown chart.
  - Coverage meter.
  - Optional carbon pathway or thermometer visual for implied temperature rise.
- Data context panel:
  - Show the source schema constraints.
  - Explain water data limitation.
  - Explain that holdings and sustainability are separate apps/datasets.
- Compliance-style footnote:
  - Mark all outputs as illustrative.
  - State that this is not investment advice.

## Content Tone

Use concise institutional copy. Avoid marketing hype.

Preferred language:

- "portfolio-level metric"
- "coverage"
- "benchmark"
- "methodology"
- "illustrative estimate"
- "schema-aligned mock data"
- "not currently available in the SSGA sustainability schema"

Avoid:

- "real-time per-holding ESG calculation"
- "water impact from SSGA data"
- "guaranteed offset"
- "actual avoided emissions"

## Implementation Constraints

- Keep the prototype self-contained unless extracting local fonts.
- Use semantic HTML.
- Use accessible labels for controls.
- Use plain JavaScript; no build step unless absolutely necessary.
- Do not fetch live APIs.
- Do not use external CDNs.
- Keep mock data in a clearly named object, for example `ssgaSustainabilityMock`.
- Use `Intl.NumberFormat` for currency and number formatting.
- Ensure the page is responsive for desktop and tablet widths.

## Acceptance Criteria

The implementation is complete when:

- `esg_simulator.html` presents an SSGA-style ESG and carbon impact simulator.
- Local font usage is wired for Inter and Sharp Grotesk where available.
- The primary calculation uses the provided SSGA carbon footprint values.
- Water is either omitted from primary outputs or marked as a future illustrative metric.
- The UI does not claim per-holding sustainability data exists.
- Portfolio vs benchmark comparisons are visible and understandable.
- Investment amount changes update all relevant output values.
- The page includes schema and methodology context from the Jira/Confluence research.
- The prototype can be opened directly in a browser without a build command.

## Suggested Implementation Plan

1. Extract font archives into `fonts/` if available.
2. Add local `@font-face` declarations for Inter and Sharp Grotesk.
3. Replace the current dark visual language with an SSGA-inspired light institutional design.
4. Replace stylised sector carbon data with the schema-aligned `ssgaSustainabilityMock` object.
5. Add investment amount, scope, and scenario controls.
6. Implement derived calculations from selected scope and investment value.
7. Add SVG/CSS comparison visuals.
8. Add methodology, schema, and water limitation panels.
9. Test manually by changing investment values, scopes, and scenarios.
10. Verify that all claims remain aligned with the Jira/Confluence constraints.

