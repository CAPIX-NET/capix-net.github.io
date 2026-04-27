---
title: CAPIX FY2025 R&D Tax Incentive Application — Analysis & Strategy
prepared: 2026-04-26
income_year: 2024-2025
income_period: 1 Jul 2024 – 30 Jun 2025
registration_deadline: 30 April 2026
project_ref: P160E5J1M (CAPIX AI Corporate Cash Management)
prior_registration: IR2411898 (FY2023-24, ref 2324-AP00-052-445)
status: Strategy notes — not yet lodged
---

# CAPIX FY2025 R&D Tax Incentive Application — Analysis & Strategy

## Deadline urgency

As at the date these notes were prepared (2026-04-26), the FY2025 registration deadline is **30 April 2026 — 4 days away**. Late applications **cannot be accepted** under any circumstance (Software RDTI guide, p.16). If the application has not been started, prioritise lodging a complete-but-conservative application now and refining via voluntary variation later if needed (variations are still possible within the 10-month window).

---

## 1. What's already on the record (FY24 baseline)

Under registration **IR2411898** (ref 2324-AP00-052-445):

- **Project P160E5J1M — CAPIX AI Corporate Cash Management** — registered as a multi-year project May 2023 → Dec 2026, total expected spend AUD 1.5M.
- **Core R&D Activity P5D5WJ0S0 — AI CashFlow Forecasting and Management** — Jul 2023–Jun 2024, AUD 735,310 claimed.
- Hypothesis used: hybrid LSTM + Transformer + autoencoder/GNN reduces MAPE ≥30% and detects anomalies with ≥95% precision vs. rule-based control.
- 2 R&D FTE out of 5 total employees; aggregated turnover AUD 710,500; loss AUD -521,900.

This gives a **registered umbrella project** that already covers FY25. Do **not** create a new project — continue P160E5J1M and register **the FY25 core activity (and any supporting activities) under it**.

---

## 2. What was actually done in FY25 (Jul 2024 – Jun 2025)

From the website news log (`/news/index.md`) and AI page (`/ai/index.md`), the FY25 R&D evidence is concrete and dateable:

| Date | Activity | Likely R&D character |
|---|---|---|
| 28 Sep 2024 | Cloud resources migrated to Azure South-East datacentre | **Supporting** — infrastructure for AI model serving |
| 11 Feb 2025 | **FX volatility metrics and currency correlations added to AI cashflow model** | **Core** — new feature engineering, hypothesis-testable |
| 22 Mar 2025 | **NeuralProphet integration & testing for time-series** | **Core** — new model component, hypothesis-testable |
| Throughout FY25 | Hybrid model architecture continues to evolve (LSTM + Transformer + XGBoost per `/ai/`) | **Core** — continuation of registered activity |

**Note:** Agentic AI work (NeuralProphet ground-truthing notes Dec 2025; agentic AI articles Jan–Mar 2026) falls in **FY2026**, not FY2025. Don't claim it here — keep it for the FY26 application (deadline 30 Apr 2027).

---

## 3. Recommended FY25 application structure

Reuse Project P160E5J1M and register **one new core activity** plus **two supporting activities**. The framing must show *progression from FY24*, not duplication. The Software RDTI guide explicitly requires multi-year registrations to "show a progression of work over that period, outlining how the R&D activities have changed and progressed over time" (p.9).

### Core R&D Activity (FY25): "Hybrid forecasting model evolution — FX-aware features and seasonality decomposition"

**Suggested name:** `CAPIX Hybrid AI Forecasting Model — FX Volatility Features and Seasonality Decomposition`

**Start–end:** Jul 2024 – Jun 2025 (within income year; do not bleed into FY26)

**FY25 hypothesis (distinct from FY24):**

> Building on FY24's LSTM+Transformer baseline, we hypothesise that (a) augmenting the input feature space with FX volatility metrics (realised volatility, GARCH(1,1) conditional volatility, currency-pair correlation matrices) and (b) decomposing the target series with NeuralProphet's additive seasonality components prior to LSTM/Transformer prediction will reduce 30/60/90-day MAPE by a further ≥10% on multi-currency cashflow series characterised by mixed weekly/monthly/quarterly cycles, where the FY24 hybrid plateaued. The outcome is unknown because the interaction between NeuralProphet's seasonality decomposition and downstream deep learning predictors has no published benchmark for treasury cashflow data, and because the marginal contribution of FX-derived features over raw FX rates is untested in this domain.

**Why a competent professional cannot determine the outcome:**

- No published literature benchmarks NeuralProphet-decomposed series fed into LSTM/Transformer ensembles for multi-currency *treasury* cashflow (search Computer Science journals, GitHub, arXiv — keep search receipts).
- FX volatility-as-feature vs FX rate-as-feature interaction effects on cashflow MAPE are not in the FY24 result set or in publicly available work.
- Industry treasury vendors (Kyriba, Cashforce, FIS) publish marketing claims, not reproducible architecture details.

**Experiment design (must be documented contemporaneously — get this from your engineers now):**

- **Test arms:** (1) FY24 baseline hybrid; (2) baseline + FX volatility features; (3) baseline + NeuralProphet seasonality preprocessor; (4) baseline + both.
- **Data:** Same MNC cohort as FY24 (continuity matters for valid comparison) over Jul 2024 – Jun 2025.
- **Metrics:** MAPE@30/60/90 days; directional accuracy; FX-stressed MAPE under simulated rate shocks.
- **Statistical:** Bootstrap CIs; matched-pair tests against FY24 hybrid as paired control.

**New knowledge produced:**

- Empirical mapping of NeuralProphet decomposition's value-add on top of attention-based predictors for sparse, multi-currency series.
- A treasury-specific FX feature library (volatility surfaces, correlation embeddings) with measured ablation contribution to forecast accuracy.

### Supporting R&D Activity 1: Azure cloud platform migration & ML serving infrastructure

Directly related to the core activity (model can't be experimentally A/B-tested at scale without it). Dominant purpose: enabling the FY25 core experiments. Document the Sep 2024 South-East datacentre migration plus any Azure ML compute / MLflow / serving infrastructure work.

### Supporting R&D Activity 2: ERP feature pipeline extensions for FX & multi-currency data

Pipeline work to ingest tick-level FX data (Bloomberg/market feed) and produce the new feature set. Directly related to the core hypothesis; would not have been built in this form without the core experiment.

---

## 4. Critical risks and how Moreton Resources informs them

The Moreton case (`Moreton-Resources-v-ISA-FCAFC-2019-120.md`) is the leading authority on what counts as "experimental activities" under s 355‑25(1). Three lessons directly apply:

**(a) "Experimental" doesn't disqualify applied/site-specific work.** The Full Court overturned the Tribunal's narrow view that applying existing technology to a new context isn't experimental ([148]–[154]). For CAPIX, this means **applying known ML architectures (LSTM, Transformer, NeuralProphet) to multi-currency treasury cashflow** is *capable* of being a core R&D activity — but only if the experimental framing is genuine (hypothesis → experiment → observation → evaluation), not just observation-by-application.

**(b) Don't conflate the project with the activities.** The Tribunal in Moreton lost because it treated "the pilot project as a whole" as the unit of analysis ([262]). Conversely, the Board successfully argued that activities must be assessed individually against s 355‑25 ([143](c)). For the form: keep the **core activity narrowly hypothesis-bound** to the FY25 model evolution work — don't write "we built the AI treasury platform" as the activity.

**(c) Records must show experiments actually happened in the year.** The Tribunal found in Moreton that some claimed activities in 2012-2014 were "no different in their character" from earlier registered work ([130]). Risk for CAPIX: the FY25 core activity must show *new* hypotheses tested in FY25 — not re-runs of FY24 experiments.

### Software-specific risks (Taxpayer Alerts TA 2017/5 and TA 2017/5A)

These were acknowledged in the FY24 application and remain critical:

- **Don't claim whole-of-product development.** Distinguish hypothesis-driven experimentation (the core activity) from routine engineering, integration work, and bug fixing (not claimable). The ATO/Industry alert expressly targets this.
- **Internal-administration exclusion (s 355‑25(2)(h)):** CAPIX products are sold to external corporate treasuries — not internal admin — so the AI forecasting product is not excluded. But anything built solely for CAPIX's *own* internal use (own bookkeeping, internal CI/CD, own website) is excluded from core R&D and may only qualify as supporting if its dominant purpose is supporting a registered core activity.
- **Beta testing / debugging:** Software RDTI guide allows these as part of a core activity *only if* they form part of a systematic progression of work. Don't claim production beta testing as core R&D.

---

## 5. Form section guidance (what to put where)

| Form section | What changed from FY24 | Required action |
|---|---|---|
| Registration type | No change | Same |
| Company details | No change | Same |
| Contact details | Verify Peter's details still correct | Verify |
| Application inclusions | Same (None of the above; no advance/overseas finding) | Same |
| Employees | **Update**: how many at 30 Jun 2025? FTE on R&D? | Get current numbers |
| Finance | **Update for FY25**: taxable income/loss, aggregated turnover, export sales | Need from accountant |
| Project | **Reuse P160E5J1M** — do not create a new project | Same |
| Core activity | **NEW** — add a FY25 core activity (per §3 above) | Draft per §3 |
| Supporting activities | **NEW** — two supporting activities (per §3 above) | Draft per §3 |
| Risks acknowledgement | Same software TA acknowledgement as FY24 | Acknowledge |

---

## 6. Records to gather before lodging

Per the Software RDTI guide Table 1 (p.19) and Moreton's emphasis on contemporaneous evidence, before lodging make sure you have:

1. **Literature search trail** for the FY25 hypothesis — saved Google Scholar / arXiv searches, dates, queries, results showing the gap. Screenshot if needed.
2. **Hypothesis document** dated near the start of the experiments (Aug–Oct 2024 for the FX features; Jan–Feb 2025 for NeuralProphet).
3. **Git commits / PR history** showing the experimental code branches, model variants, A/B test harness. Tag commits with the activity ID once registered.
4. **Experiment results** — MAPE numbers, training logs, evaluation notebooks, ablation tables, with timestamps in the FY25 window.
5. **Timesheets or time-allocation records** — the 2 R&D FTE need a defensible split between R&D time and commercial/support time. The FY24 application claimed AUD 735,310 against 2 FTE on R&D; if FY25 spend differs materially, be ready to justify.
6. **Azure invoices** with R&D environments separated from production (the alert expressly looks for this).
7. **Any external advice / expert consultations** — e.g. Microsoft Azure ML support engagements, academic contacts.

---

## 7. What to avoid claiming in this FY25 application

- **The full website rebuild** (visible in this repo's git log Apr 2025) — that's marketing/admin, not R&D.
- **Routine pricing library updates** — no FY25 news entries indicate hypothesis-driven pricing R&D in the year. The Dec 2023 v23.12.01 work was already FY24.
- **Generic "Python migration"** — the 6 Jul 2025 news item ("moving from Microsoft technology to Python") is FY26 work.
- **Agentic AI work** — all dated FY26. Save this for next year's application.

---

## 8. After lodging

If anything is materially different from the picture above (e.g. substantial pricing-library R&D actually occurred, or agentic AI prototype work began before 30 Jun 2025), the registration can be **varied** within the same 10-month window (i.e. before 30 Apr 2026). Variations after that window are limited.

---

## 9. Outstanding items requiring user input before form draft

To convert these notes into a form-ready core activity narrative (the same level of detail as the FY24 application at `ausindustry-23-24-rd-application.md` lines 205–442):

- [ ] Confirm the **actual FY25 hypothesis pursued** (the FX features + NeuralProphet framing above is inferred from the news log; confirm vs. what the engineers actually tested)
- [ ] Confirm **FY25 R&D expenditure estimate** (FY24 was AUD 735,310)
- [ ] Confirm **FY25 employees at 30 Jun 2025** and **R&D FTE**
- [ ] Confirm **FY25 finance** — taxable income/loss, aggregated turnover, export sales
- [ ] Confirm whether any **supporting activities** beyond the two listed in §3 should be added (e.g. ERP integration extensions, security/compliance work directly serving the core hypothesis)

---

## References

- FY24 application: [`ausindustry-23-24-rd-application.md`](./ausindustry-23-24-rd-application.md)
- FY24 registration letter: [`Registration-Letter.md`](./Registration-Letter.md)
- General application guide: [`RDTI-Application-Guide.md`](./RDTI-Application-Guide.md)
- AusIndustry first-time registrant pack: [`First-Time-Registrant-Pack.md`](./First-Time-Registrant-Pack.md)
- Software-specific eligibility guide: [`Software-activities-and-the-RDTI.md`](./Software-activities-and-the-RDTI.md)
- Federal Court precedent on "core R&D activities": [`Moreton-Resources-v-ISA-FCAFC-2019-120.md`](./Moreton-Resources-v-ISA-FCAFC-2019-120.md)
- Software-related taxpayer alerts: [`TA-2017-5.md`](./TA-2017-5.md), [`TA-2017-5A.md`](./TA-2017-5A.md)
