# Version 4 changes

- Official uploaded UNIDEMI vertical logo appears in a persistent institutional header and in a research identity strip for all calculator views.
- Original UNIDEMI cog emblem appears in each view-navigation tab and favicon.
- Official uploaded NOVA FCT / DEMI horizontal logo appears at the top of the page.
- Brand images are embedded as data URIs, ensuring that a single `index.html` can be opened offline or deployed without external assets.
- Existing calculation scripts from Version 3 were preserved byte-for-byte inside the `<script>` element.
- Corrected stale methodology note about the Monte Carlo implementation.

---

# WAAM LCSA v3 — verification

## Automated model checks (`node tests/verify.js`)

| Quantity | HTML value | Target / source |
| --- | ---: | --- |
| Environmental single score — WAAM | 9.811865 Pts | Published case (~9.81) |
| Environmental single score — CNC | 15.560246 Pts | Published case (~15.56) |
| Manufacturing cost — WAAM | €1,213.083 | Published case (~€1,213) |
| Manufacturing cost — CNC | €1,495.911 | Published case (~€1,496) |
| Social score — source company, Latvia | 0.50 (9/18) | Google Sheets `Sheet2!D5:D24` |

The sample yields about 36.94% lower single-score environmental impact and 18.91% lower manufacturing cost for WAAM versus CNC, broadly reproducing the case-study findings. The social validation is the Latvia scenario with default company values, **not** the original published-case Belgium preset.

## Implementation traceability

- `getCenterColumnData()` → stock shape/dimensions, CNC cutting feed/depth/width, 11 economic parameters, five social numeric parameters, sustainability report, company name, selected country and annual gross value added.
- `getChartEnvironmentImpactData()` → two horizontal bars reading the WAAM versus selected CNC stock impacts. Numeric values come from the client-side equivalent of Sheet1 computations.
- `style_main` → white panels, three-column structure, browser-friendly controls, bars and charts; improved mobile behaviour.
- `view_right_column` → environment, cost and social score comparisons and binary policy inputs.

## Fidelity boundaries

Independent browser calculations have been verified analytically via Node.js. The HTML has been statically parsed for unique element IDs. Pixel-level/browser interaction and the unshared script modules remain to be tested in a full browser; further validation is required before any deployment used for decisions or publications. The original source dataset has historical social country benchmarks and formula/cell inconsistencies disclosed in README.md.

## Additional service source checks (v3)

The user-provided `getGraphicsLeftColumnData` and `getGraphicsCenterColumnData` bind upstream steel, CED and ReCiPe midpoint comparisons to the named `Sheet1` ranges; the new browser implementations reproduce their structural and numerical calculation sources. `getGraphicsRightColumnData` supplies ten comparison charts built from `Sheet3` and the original social screening cut-offs.

Added automated checks verify upstream steel yield adjustments, cumulative energy demand factors, a reproducible 10,000-sample Monte Carlo simulation, and that simulated means stay within 1.5% of deterministic LCA and LCC baseline totals.

## Browser execution verification

A Chromium/Playwright interaction smoke test was performed using in-memory page content. The dashboard loaded with **9.81 Pts** for WAAM, ten social comparison charts rendered, and the Monte Carlo button created SVG histograms and a summary table for 10,000 samples. There were no uncaught JavaScript errors. The simulation should still be reviewed for research-grade equivalence before publication or stakeholder decisions. Environment limits prevented a direct `file:///` navigation, so the in-memory browser route was used for the smoke test.
