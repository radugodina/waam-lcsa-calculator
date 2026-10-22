# WAAM Life Cycle Sustainability Calculator — Version 4

This version adds the official **NOVA FCT/DEMI** and **UNIDEMI** logos supplied by the project owner. The NOVA logo is at the top of the page. The UNIDEMI logo is in the institutional header and in a research identity strip visible on **all four views**; its original cog appears in all navigation tab labels and as the browser favicon.

The existing Version 3 calculations, charts, social assessment and uncertainty simulation are retained. Original view and chart service source files supplied in the conversation were used to verify that mapping. No changes are made to the connected Google Sheets project.

**Deploying:** upload `index.html` to the root of the GitHub repository, activate GitHub Pages for your main branch/root, and navigate to the Pages URL. The HTML embeds the supplied logos so `index.html` works alone; the `assets/` copies are included for later replacement.

---

# WAAM Life Cycle Sustainability Assessment (LCSA) Calculator — v3

A single-file, offline-capable HTML/JavaScript application suitable for **GitHub Pages**. It reconstructs the WAAM sustainability calculator developed by Samruddha Kokare and Radu Godina, using the shared original Apps Script code, live Google Sheets formulas, screenshot, and associated publication.

## Quick start

Open `index.html` in a modern browser. No Google account, Apps Script runtime, external JavaScript libraries, server, or internet connection is needed. For publication, commit `index.html` to the root of a GitHub repository and enable **Settings → Pages → Deploy from a branch → main / (root)**.

## Included features

- **LCA:** WAAM material/energy/gas inventories, ReCiPe 2016 (H) single score, the workbook's GWP parameters, 18 midpoint indicator comparisons, contribution chart and horizontal WAAM/CNC comparison.
- **LCC:** machine investment, depreciation, facility availability, maintenance, tooling, operator time, steel wire/bar prices, electricity, shielding gas and post-processing, plus a pure CNC cost comparison.
- **CNC stock:** cylindrical or cuboidal stock selection with context-sensitive dimension fields; changing stock type recalculates the CNC impact and cost comparison. Corresponds to `Sheet1!D69` and `Sheet1!D107:E110` from the original script.
- **S-LCA screening:** social country and company selection, gross value added, employees, collective bargaining, salary, gender ratio and pay gap, injury frequency, annual report, sustainability and consumer policies, customer feedback and privacy. Uses the 18 equally weighted social criteria in `Sheet2!D5:D22` and historical country benchmarks in `Sheet3!A3:L28`.
- **Results:** summary cards; orange and blue original-style horizontal bars (WAAM/CNC); environmental and cost doughnut charts; S-LCA score versus its cutoff; three-column detailed analysis with environmental/cost/social tables and drivers.
- **Detailed original charts (new in v3):** selected-stock production-cost and environmental comparison; WAAM/CNC cost and environmental contribution breakdowns; upstream steel consumption, carbon footprint, cumulative energy demand; 18 two-process normalized ReCiPe midpoint charts; 10 country/company social indicator comparisons.
- **Monte Carlo uncertainty (new in v3):** 10,000 independent, seeded normal-variation samples of environmental LCI contributions and production cost components, 50-bin histograms, means, standard deviations and estimated 95% outcome ranges. The uncertainty simulation is deliberately run on request, instead of on each slider move.
- **State:** reset to published example; restore opening values; save and load a complete local JSON scenario; export all LCA/LCC/S-LCA values to CSV; print to PDF.

## Model provenance and precise differences

The environmental and financial calculations follow the reconstructed workbook conventions from version 1; the additional S-LCA screening reimplements the accessible **actual Sheet2 rules**, not just a generic sustainability index.

The original spreadsheet includes 18 binary social indicators. Most are compared to a country reference, EU mean, global average, or a Yes/No benchmark. **All indicators have equal weights.** A score **≥0.50** is labelled positive, and a score below 0.50 negative. The available country reference values date chiefly to 2021–2024 and must be updated for contemporary use. For example, the original country is Latvia and the sample organisation has a screening score of **0.50 (9/18)**.

- **Gender pay gap:** `Sheet2!D11` actually tests `C11 <= 11`, although `E11` displays `10` in the workbook. To preserve formula behaviour, this HTML uses **11%** as the pass threshold and documents this inconsistency.
- **Country comparison:** selecting a country in the social area adjusts the sheet-specific electricity single-score factor and WAAM hourly labour rate to the corresponding `Sheet3` values, as well as its social benchmark data. Selecting a country through the electricity control also synchronizes these values. Manual factor edits remain possible.
- **Missing social benchmarks:** the workbook lacks some national wage, social security and gross-value-added values. Rather than score unavailable data arbitrarily, the HTML shows `N/A` and reports a screening percentage using the number of *evaluable* indicators. This is a deliberate conservative usability deviation from the original fixed 18-indicator averaging, and the number evaluated is explicitly shown.
- **Environment chart:** the supplied original Apps Script fetched `Sheet1!D107:E108` or `D109:E110` depending on stock type and displayed the two scores using Google BarChart. The standalone implementation reproduces that behaviour with dependency-free HTML bars; precise visual rendering is not pixel-identical to Google Charts.
- **Google Apps Script:** `onOpen()`, the Calculator custom menu, `google.script.run`, `CacheService`, and spreadsheet mutation do not run on a GitHub Pages site. The standalone page computes locally; restore resets to the opening state of the session. It does **not** write to the original Google Sheet.
- **Electricity convention:** the workbook uses WAAM deposition power × deposition time (without cooling standby load) for its single-score equation, whereas the published paper's Eq. (10) includes standby power. The web version follows the worksheet convention and discloses it.
- **Post-processing power:** the workbook's `Sheet1!F36` approximation (finishing kW × finishing time plus short setup/standby energy) drives the single score.
- **Material category factors:** country changes update the spreadsheet's aggregate single-score electricity factor, but the 18 midpoint electricity factors and GWP electricity factor remain independently stored, because the source spreadsheet does not contain a per-country set of all these midpoint factors.
- **Travel speed** remains an input to preserve the original tool's interface, although the simplified workbook build-rate formula does not use it.

## Outstanding limitations

The newly supplied `getChartProductionCostData`, `getChartSocialImpactData`, `getGraphicsLeftColumnData`, `getGraphicsCenterColumnData`, `getGraphicsRightColumnData`, `getLeftColumnData`, and `getRightColumnData` now ground the original chart definitions and indicators. The original `view_graphics_*` and detailed client rendering scripts are still unavailable, so spacing, formatting and some chart behaviour remain independent reconstructions rather than a byte-identical port. No social score is an empirically verified company social audit; sample values are illustrative.

### Monte Carlo parity and limitations

The historical Sheets' `Sheet6` uncertainty samples use `NORMINV(RAND(),mean,0.1·mean)` for individual environmental quantities and `Sheet9` uses the same for individual manufacturing cost components. The HTML produces **10,000 new draws** using a seeded Box–Muller normal generator, applying the selected relative standard deviation separately to each environmental inventory contribution and each cost component. Environmental factors are held fixed. Hence the expected mean and variance match the simplified independent-component normal approach; **individual samples and histogram bins will not match live Sheets RAND() results**. Confidence-style bounds `mean ± 1.96 SD` are approximately 95% **outcome ranges**, not uncertainty on the estimated mean. A paired-draw probability of lower impact/cost is an additional analytical output. The model assumes independence and normality; it does not estimate epistemic or model-structure uncertainty.

### Original service mapping added in v3

| Apps Script service | Workbook source | Recreated output |
| --- | --- | --- |
| `getChartProductionCostData()` | `Sheet1!D112:E115` | WAAM/CNC comparative production cost chart |
| `getChartSocialImpactData()` | `Sheet2!D24:E25` | Company screening score vs 0.50 cut-off |
| `getGraphicsLeftColumnData()` | `Sheet1!E44:E47`, `L110:L117`, `G107:G110`, `G121:G124`, `G127:G130`, `Sheet6` | LCA contributions, carbon footprint, CED, steel demand, environmental distributions |
| `getGraphicsCenterColumnData()` | `Sheet1!E61:E66`, `J110:J119`, `L89:U106`, `Sheet9` | LCC contributions, per-category relative midpoint bars, cost uncertainty |
| `getGraphicsRightColumnData()` | `Sheet3!N5:P31` | Country and company social benchmark charts |
| `getLeftColumnData()` / `getRightColumnData()` | `Sheet1` and `Sheet2` | Geometric/WAAM inputs, economic parameters and binary policies |


This site is a **research demonstrator**, not a certified environmental declaration, audited costing system or validated company social audit.

## Scientific reference

Kokare, S., Oliveira, J. P., & Godina, R. (2026). *Advancing sustainable manufacturing decision-making through an online life cycle assessment tool for wire-based directed energy deposition*. **The International Journal of Advanced Manufacturing Technology**, 143, 391–419. https://doi.org/10.1007/s00170-025-17351-4

## Developer API / testing

All calculation logic is in `index.html`. The browser exposes:

```js
window.WAAMCalculator.calculate(window.WAAMCalculator.getInputs());
window.WAAMCalculator.socialAssessment(window.WAAMCalculator.getInputs());
```

Run `node tests/verify.js` if Node.js is installed to test the scientific calculation values, original Latvian S-LCA snapshot, steel/CED indicators and Monte Carlo model.
