# WAAM Life Cycle Sustainability Assessment (LCSA) Calculator

Interactive browser-based calculator for the **Life Cycle Assessment (LCA)**, **Life Cycle Costing (LCC)**, and **Social Life Cycle Assessment (S-LCA)** of products made using **Wire Arc Additive Manufacturing (WAAM)**, including a comparison with conventional CNC milling.

**Use the interactive calculator:** [https://radugodina.github.io/waam-lcsa-calculator/](https://radugodina.github.io/waam-lcsa-calculator/)

> GitHub Pages must be enabled for this repository (Settings → Pages → Deploy from a branch → `main` / `/(root)`) before the above link works.

## What you can do

- Specify part geometry, WAAM process parameters, CNC stock dimensions, machining parameters and manufacturing costs.
- Compare the environmental impacts, carbon footprints, energy consumption, material demand and production costs of WAAM and CNC milling.
- Explore 18 ReCiPe midpoint indicator comparisons and contribution charts.
- Evaluate indicative social sustainability criteria using country and company information.
- Run a 10,000-sample Monte Carlo uncertainty analysis of the modelled environmental impacts and costs.
- Save, restore and export calculation scenarios.

The website is a **standalone HTML/JavaScript application**. It does not require Google Sheets, a Google account or an active Google Apps Script deployment. Calculations execute within your browser.

## Authors and institutional affiliation

**Samruddha Kokare; Radu Godina**  
**UNIDEMI — Research and Development Unit for Mechanical and Industrial Engineering**  
**NOVA School of Science and Technology (NOVA FCT), Universidade NOVA de Lisboa**

The site incorporates the supplied UNIDEMI and NOVA FCT/DEMI institutional logos.

## Scientific publication

Kokare, S., Oliveira, J. P., & Godina, R. (2026). *Advancing sustainable manufacturing decision-making through an online life cycle assessment tool for wire-based directed energy deposition*. **The International Journal of Advanced Manufacturing Technology**, 143, 391–419. https://doi.org/10.1007/s00170-025-17351-4

## Technical documentation

See [Technical Notes](TECHNICAL_NOTES.md) for calculation conventions, differences from the Google Sheets implementation, historical social reference data and limitations. See [Validation](VALIDATION.md) for model checks and reproducibility notes.

## Research-use note

This application is a research demonstrator. Its screening estimates and illustrative parameters should not be interpreted as certified environmental declarations, audited manufacturing costs or verified social audits. The standalone calculator does not write values back to the original spreadsheet.
