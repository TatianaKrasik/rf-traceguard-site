# RF-TraceGuard

**Measurement integrity monitoring for RF production test stations**

RF-TraceGuard reads the test results and reference measurements that an automated RF test station already records, and follows the condition of the measurement path between calibrations. Each result receives an integrity class, reference measurements are tracked for drift, and the components most likely behind a change are ranked for inspection.

Patent pending · U.S. Provisional Application No. 64/184,842

---

## Background

Calibration confirms the instruments on the calibration date. Cables, connectors, switches and fixtures keep ageing after that date, and a slow drift inside the tolerance still produces results that look normal. In daily practice engineers find such a change late, often through a rise in failures, and then search for its source by replacing parts one at a time.

RF-TraceGuard treats the measurement chain itself as the object of monitoring. Every test is described as the chain of components the signal passes through, each component keeps its reference baseline and uncertainty contribution, and the routine stream of results becomes a source of information about the station.

## Main modules

| Module | Role |
|---|---|
| Measurement Model | Stations, test paths and components, with reference values and uncertainty contributions |
| Integrity Engine | Compares the margin to the specification limit with the combined (RSS) uncertainty of the path and the drift status, and assigns VALID, WARNING or REVIEW |
| Drift Monitor | Baseline from the first reference points, EWMA, linear trend over recent points and a forecast of the time to the warning and critical levels |
| Root-Cause Engine | Ranks candidate components by the affected paths that contain them, their presence in paths that stayed normal and the shift of their own reference measurements |
| Incident record | Keeps the timeline, the evidence and the list of affected results for later review |

An optional language model can phrase the explanation and order the recommended checks. It can be switched off, and every figure behind the result stays in the report.

## Operating principles

- **Read-only.** The software works on files the station already writes. The approved test sequence and station control stay with the existing test software.
- **Advisory.** Engineers check the suggested cause on the hardware and keep the final production decision.
- **Deterministic core.** Integrity classes, drift assessment and candidate ranking come from deterministic algorithms.
- **Local.** The application runs on site, offline.

## Input data

The following describes the input formats used by the software; these files are **not distributed with the website**.

**Production measurements** (`results.csv`): time, station, DUT, product and test identifiers, frequency, measured value, specification limits, PASS/FAIL status, software version and calibration identifier.

**Reference measurements** (`references.csv`): time, station, reference name, frequency, expected and measured values, and the component path being checked.

Touchstone files (`.s2p`) are supported for network analyzer data.

## Website and navigation

This repository contains the **RF-TraceGuard information website**, not the RF-TraceGuard executable, Python source code or a downloadable demonstration dataset.

Start with [`index.html`](index.html). The pages link to one another using relative paths:

| Page | File | Contents |
|---|---|---|
| Home | [`index.html`](index.html) | Overview and selected field observations |
| Technology | [`technology.html`](technology.html) | Measurement model, workflow and prototype interface |
| Applications | [`applications.html`](applications.html) | Documented applications and measurement results |
| Comparison | [`comparison.html`](comparison.html) | Comparison with other technical approaches |
| Recognition | [`recognition.html`](recognition.html) | Award and professional assessments |
| Research & IP | [`research.html`](research.html) | Research background and patent application |
| About | [`about.html`](about.html) | Developer, professional background and contact |

To preview the site before publishing, download **all HTML files together** into one folder and open `index.html` in a browser. Keep `tatiana-krasik.jpg` in the same folder; the portrait is also embedded in `about.html` so that page can display it when opened on its own.

Google Drive is used to store and review the files; its individual HTML preview links are **not** a deployed website, and navigation among them may not work in the Drive viewer. For the public site, publish these files at the repository root via GitHub Pages.

GitHub repository: [TatianaKrasik/rf-traceguard-site](https://github.com/TatianaKrasik/rf-traceguard-site).

## Demonstration dataset

The Technology page describes a synthetic demonstration for station ATE-02; the underlying dataset is **not included in this website repository**. Cable C2 develops increasing loss at 6 GHz: its reference deviation reaches +0.26 dB against a warning level of +0.20 dB, with a trend of about +0.024 dB per day.

A product reading of −19.70 dBm against a −20.00 dBm limit still reports PASS. Its margin equals about 1.03 times the combined uncertainty of the path, and the path carries an active drift warning, so RF-TraceGuard classes the result as WARNING, retest required. Cable C2 ranks first (score 100.0), ahead of Cable C1 (63.3) and the analyzer (51.0).

All values in this example are synthetic.

## Field applications

The software has been applied at three sites, each documented by the host organization:

- **Electronics manufacturing.** A shared cable path at 666 MHz drifted while every product still passed. The probable source was found 6 minutes after diagnostics began and recovery was confirmed after 18 minutes. Similar searches at the site used to take 1.5 to 3 hours.
- **Microwave measurement laboratory.** A network analyzer setup drifted between 12 and 18 GHz while the comparable setups stayed stable. The onset was traced to series 5, and after a cable replacement the peak S21 deviation fell from 0.38 dB to 0.07 dB.
- **University research laboratory.** On an electromechanical bench the EWMA flagged a sustained offset in shunt current at the fourth cycle of a series. Staff found a loose signal connector, and the repeat series stayed within +0.78% of the baseline.

## Status and roadmap

The current version implements the read-only part of the method. Next steps:

- Calibration of thresholds and score weights on industrial data. Until then the score serves to order candidates for inspection.
- Station topology in YAML or JSON configuration files.
- Test lines with active components such as RF power amplifiers.
- Network analyzer stations with temperature taken into account.
- Route-based localization and analysis across several stations, as described in the provisional patent application.

## Recognition

Winner of the “Best Innovative Solution for Industry” category at the 2025 All-Russian hackathon “Best Innovations: Practice”, with the highest final score among 18 finalists.

## Author

**Dr. Tatiana Krasik**, RF and microwave measurement engineer

Email: tatyanakrasik12@gmail.com
LinkedIn: [linkedin.com/in/tatiana-krasik-phd-08704421b](https://www.linkedin.com/in/tatiana-krasik-phd-08704421b)

## License

© 2026 Tatiana Krasik. All rights reserved.
Patent pending, U.S. Provisional Application No. 64/184,842.
