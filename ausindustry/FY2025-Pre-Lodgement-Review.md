---
title: FY2025 R&D Tax Incentive — Pre-Lodgement Review and Tightening Suggestions
prepared: 2026-04-30
applies_to: 2025-draft-application.md (Core R&D activity section)
status: Review notes — for use before lodgement and for future-year reference
---

# FY2025 RDTI — Pre-Lodgement Review

This file flags every claim in the drafted FY25 Core R&D Activity (`2025-draft-application.md`) that should be verified against your actual records before lodging. It exists because the draft narrative uses standard FY24-style language ("≥30% MAPE reduction", "expanded cohort", "four parallel arms") that may or may not match what your engineers actually did in FY25. Per the Moreton Resources case (FCAFC 2019) and the Software RDTI sector guide, **contemporaneous evidence must back every factual claim** — over-claiming on the form when the records don't support it is the single biggest risk in a software RDTI registration.

The intent here is **not** to weaken the application — it is to make every claim defensible if AusIndustry queries it.

---

## How to use this file

For each item below:

1. Read the **claim as drafted**.
2. Check the **what to verify** against your engineering notes, git history, experiment notebooks, or timesheets.
3. If the claim holds, leave the draft alone.
4. If it doesn't, **edit `2025-draft-application.md`** to a narrower, defensible claim before pasting into the portal.
5. If unsure, narrow the claim — undeclared work is recoverable via voluntary variation; over-claimed work is not.

This file should also inform the FY26 application — the same review pattern applies.

---

## 1. Numeric performance claims

### 1a. "≥30% MAPE reduction" (held over from FY24)

**Claim as drafted:** "the FY24 ≥30% MAPE reduction held across the expanded FY25 cohort"

**What to verify:**
- Did FY25 evaluation actually re-test the FY24 ≥30% reduction figure? Or is this a claim asserted-by-continuity?
- Are there evaluation notebooks dated within Jul 2024 – Jun 2025 that report MAPE numbers?

**If unverified, change to:** "the FY24 baseline architecture continued to operate in production through FY25" (factual continuation rather than re-validation).

### 1b. "≥10% additional MAPE reduction"

**Claim as drafted:** "an additional ≥10% MAPE reduction over the FY24 hybrid baseline" (hypothesis target) and "exceeding the ≥10% progression target on EUR/GBP/JPY-exposed series" (conclusion)

**What to verify:**
- Was 10% set as a hypothesis target *before* the experiments started, or is it a retrofitted figure? Moreton case lesson: hypothesis must be documented contemporaneously, near the start of the activity.
- Do you have measured MAPE numbers from the FX-features arm vs. baseline, with bootstrap CIs?

**If unverified, change to:** Drop the specific 10% figure. Replace with "a measurable reduction in MAPE relative to the FY24 baseline, to be validated by ablation testing." For the conclusion, say "measured directional improvement on EUR/GBP/JPY-exposed series" without the 10% threshold.

### 1c. "≥95% anomaly detection precision" (held over from FY24)

**Claim as drafted:** "flag irregularities (e.g., unexpected payment delays, fraud risks) with ≥95% precision"

**What to verify:**
- This was the FY24 hypothesis, achieved at 88% precision in FY24 (per the FY24 application). Did FY25 work re-test this?
- The FY25 narrative carries this hypothesis forward but does not need to — anomaly detection wasn't a primary FY25 progression axis.

**If unverified, change to:** Either (i) drop anomaly detection from the FY25 hypothesis entirely (it's a FY24 carry-over), or (ii) rephrase as "continued operation of the FY24 autoencoder-GNN ensemble, integrated with new FX-aware features."

### 1d. "Bootstrap confidence intervals confirmed statistical significance"

**Claim as drafted:** "Bootstrap confidence intervals confirmed statistical significance of the additional MAPE reduction"

**What to verify:**
- Did anyone actually run bootstrap CIs on the FY25 results? This is a specific statistical method.
- If they used a different method (paired t-test, Diebold-Mariano test for forecast comparison, Wilcoxon signed-rank), name the actual method.

**If unverified, change to:** Drop the specific method. Replace with "statistical comparison against the FY24 baseline arm." Or specify whichever method was actually used.

### 1e. "5x faster adaptation" / "<15% MAPE deviation under stress" (FY24 carry-overs)

**Claim as drafted:** Implied by the structure of the conclusions section, which mirrors FY24.

**What to verify:**
- These figures were specific to FY24 stress testing. Did FY25 stress-test results produce comparable numbers?
- The FY25 draft does not explicitly claim these numbers — but if it did, they would need fresh measurement.

**If unverified, change to:** Already handled — the FY25 draft uses qualitative language ("maintained accuracy under simulated rate shocks") rather than specific numbers. Keep it that way.

---

## 2. Experimental design claims

### 2a. "Four parallel test arms"

**Claim as drafted:** Four arms: (1) FY24 baseline, (2) +FX volatility, (3) +NeuralProphet, (4) +both.

**What to verify:**
- Did you actually run all four arms in parallel, or sequentially, or only some of them?
- For ablation analysis to be valid, all four arms need to have been run on the same data window. If FX features were added Feb 2025 and NeuralProphet integrated Mar 2025, the combined arm could only have been evaluated from Mar 2025 onward — a ~3-month evaluation window before income-year end.

**If only two arms ran (baseline + combined):** Edit to describe a two-arm design with clear pre/post comparison. This is still a valid experiment under s 355-25 — you just shouldn't claim ablation that didn't happen.

**If sequential rather than parallel:** Re-frame Phase 1 / Phase 2 / Phase 3 as a sequential progression of versions rather than simultaneous arms. This is honest and still demonstrates systematic progression.

### 2b. "MNC cohort" / "expanded FY25 cohort"

**Claim as drafted:** "stored data from a multinational corporate treasury cohort" and "the expanded FY25 cohort"

**What to verify:**
- The FY24 application claimed "real-world experiment with stored data from a multinational corporation" (singular). Did the FY25 cohort actually expand beyond that one MNC?
- If the same single MNC's data was used (just over a different time window), say so plainly.

**If single MNC continued:** Change "expanded FY25 cohort" to "extended to the FY25 income-year window using the same MNC dataset as FY24, supplemented with tick-level FX market data introduced from Feb 2025."

### 2c. "Tick-level FX data ingestion from Feb 2025 onward"

**Claim as drafted:** "Tick-level FX data ingested from Feb 2025 onward to support the new volatility feature extraction"

**What to verify:**
- Is tick-level FX data actually being ingested? Or is it daily/intraday-bar data?
- "Tick" is a strong technical claim implying sub-second granularity from a market feed.

**If not literally tick-level:** Use "high-frequency intraday FX rate data" or whatever resolution actually applies (e.g. "1-minute bars from Bloomberg API").

### 2d. "Bloomberg API feeds at tick-level resolution" (held over from FY24)

**Claim as drafted (FY24 reference):** Same issue as 2c.

**What to verify:** Is there a current Bloomberg API subscription? If the FY25 work uses a different feed (alternative provider, lower-cost FX feed), name that one.

---

## 3. R&D effort and FTE claims

### 3a. "2 → 5 R&D FTE scaling"

**Claim as drafted:** "The expanded R&D team (2 → 5 FTE in FY25) enables the broader experimental cohort, increased number of parallel test arms, and the dedicated infrastructure work…"

**What to verify:**
- The form claims 7 employees and 5 R&D FTE at 30 Jun 2025. **Is this 5 FTE allocation to R&D, or 5 individuals each spending some time on R&D?** These are very different.
- AusIndustry/ATO scrutinise FTE allocation closely. If 5 individuals spent only ~50% of their time on R&D, the defensible FTE figure is 2.5, not 5.
- Does each of the 5 R&D-counted staff have a timesheet record showing R&D time vs. commercial time?

**If 5 FTE means 5 *headcount* with mixed allocation:** This is the single biggest risk in the application. Either (a) revise the FTE number on the form to a defensible time-weighted figure, or (b) ensure timesheet records show actual time allocation that supports a 5 FTE figure. Don't leave this ambiguous.

**TA 2017/5 specifically targets over-claiming whole-of-product development as R&D.** A 5-of-7 staff R&D allocation in a small software company will be examined closely. The records must distinguish hypothesis-driven experimental work (claimable) from routine engineering, integration, bug fixing, customer support, and sales engineering (not claimable).

### 3b. "AUD 715,088 R&D expenditure"

**Claim as drafted:** AUD 715,088 estimated expenditure for the core activity, matching the R&D Expenditure field in the finance section.

**What to verify:**
- Does the AUD 715,088 figure correspond to R&D-eligible expenditure as defined in s 355-205 ITAA 1997 (salaries × R&D time fraction, contractor R&D fees, eligible Azure compute, etc.)?
- Does it exclude expenditure that is excluded under s 355-225 (e.g., expenditure on excluded core activities, or core activities not registered)?
- Is this the actual figure or an estimate from the accountant?

**If estimate:** Document the basis of the estimate (e.g. "5 R&D FTE × average salary × R&D time fraction + Azure ML compute spend + portion of Bloomberg feed allocated to R&D").

**If actual:** Make sure the supporting workpapers exist and are dated.

---

## 4. Timeline and evaluation window claims

### 4a. "Phase 4 — FX-stressed evaluation (throughout FY25)"

**Claim as drafted:** "Simulated FX shocks (sudden EUR depreciation, JPY-USD volatility spikes) were injected into all four arms… throughout FY25."

**What to verify:**
- "Throughout FY25" implies the FX-stressed evaluation ran from Jul 2024 onward. But the FX volatility features themselves were only added Feb 2025. So FX-stressed evaluation of arms 2–4 could not have run before Feb 2025 (or Mar 2025 for arm 4).
- The honest version: stress evaluation of the FY24 baseline could have run Jul 2024 onward; stress evaluation of the new arms could only run from Feb–Mar 2025 onward.

**Change to:** "FX shock simulations were injected into the FY24 baseline throughout FY25, and into the new arms (2–4) from their respective deployment dates (Feb 2025 for arm 2, Mar 2025 for arms 3 and 4) through the end of the income period."

### 4b. "Apr–Jun 2025 combined arm and ablation"

**Claim as drafted:** Phase 3 — Combined arm and ablation (Apr–Jun 2025).

**What to verify:**
- Three months (Apr–Jun 2025) is a tight window for a meaningful ablation study with statistical significance. Did the work actually happen in this window, or is it carrying into FY26?
- If the ablation extends into FY26, that's fine for *next year's* application — but you can't claim conclusive results in this year's narrative if the conclusions weren't reached by 30 Jun 2025.

**If ablation extends into FY26:** Change "Phase 3 — Combined arm and ablation (Apr–Jun 2025)" to "Phase 3 — Combined arm deployment from Apr 2025; ablation analysis initiated in FY25 and continuing into FY26 for fuller statistical power." Then frame the FY25 conclusions as "preliminary directional findings" rather than fully validated outcomes.

This is per the Software RDTI guide: only conclusions actually reached *in the income period* should be reported as concluded; later conclusions belong in the next year's application.

### 4c. "Continued learning validation" / "monthly delta accuracy"

**Claim as drafted:** "Measured % improvement in MAPE as models ingested new FY25 data monthly."

**What to verify:** Does the team actually have monthly evaluation cadence? Or is evaluation ad-hoc / quarterly / end-of-period?

**If not monthly:** Change to whichever cadence applies, or remove the cadence claim and just say "evaluation conducted at intervals across the FY25 income period."

---

## 5. Infrastructure and partnership claims

### 5a. "Migration was specifically scoped and timed to enable the FY25 four-arm A/B testing at scale"

**Claim as drafted:** This is the *dominant purpose* framing for the Sep 2024 Azure migration.

**What to verify:**
- Was the migration scoped/sized/timed *because of* the FY25 R&D experiments, or for general operational reasons (cost, latency, data sovereignty, customer demand)?
- This matters less than it would if Azure migration were a separate supporting activity (which the form answers ☑ No to). But if AusIndustry queries it, having a defensible reason matters.

**If migration was for general business reasons:** Soften the language. Replace "specifically scoped and timed to enable" with "provided the compute capacity needed for". You haven't claimed the migration as supporting R&D, so you don't need to argue dominant purpose — you just need to describe how the infrastructure was used.

### 5b. "May 2024 Azure ML partnership"

**Claim as drafted:** "Microsoft Azure Machine Learning technical documentation and engagement support (per the May 2024 Azure ML partnership)"

**What to verify:**
- The 19 May 2024 news item announces a partnership with Microsoft for "the provision of Azure Machine Learning resources." Is this a formal partnership with documented engagements (named Microsoft contacts, support tickets, joint design reviews), or a marketing description of an Azure ML subscription?
- Listing it as a "source investigated" implies expert engagement. If it's just a paid Azure subscription, that's not the same as expert advice for the form's "Experts in the field provided advice" checkbox.

**If just a subscription:** Don't claim it as expert advice. The "no applicable information in scientific, technical, or professional literature" checkbox is enough.

### 5c. "Linux-based mini-servers in our Melbourne office"

**Claim as drafted (in the project Plant/Facilities section):** "We have several Linux-based mini-servers for development and running models in our office."

**What to verify:** These exist? Are they used for R&D? Are their compute costs (depreciation, electricity) included in the AUD 715,088 R&D expenditure?

**If included in R&D expenditure:** Fine. **If not:** They may still be relevant infrastructure. **If they don't exist or aren't used for R&D:** Remove.

---

## 6. Sources investigated and prior-art claims

### 6a. "No published hybrid models combine NeuralProphet… with LSTM/Transformer ensembles for treasury cashflow"

**Claim as drafted:** Strong prior-art claim that this combination has no published benchmark.

**What to verify:**
- Did anyone do a literature search? When? With what queries?
- Save Google Scholar / arXiv search receipts (screenshots showing query, date, result count, relevant or not). The Software RDTI guide explicitly looks for these.
- A claim that "no applicable information exists in literature" without a documented search trail is exactly what AusIndustry queries.

**If no documented search:** The claim still might be true, but you need to do the search now and keep records. Search terms to run today, with results saved:
- `"NeuralProphet" "LSTM" treasury OR cashflow` (Google Scholar)
- `"NeuralProphet" "transformer" finance` (Google Scholar)
- `treasury cashflow forecasting "FX volatility" "feature engineering"` (Google Scholar, arXiv)
- arXiv: `cat:cs.LG AND (treasury OR cashflow) AND (NeuralProphet OR Prophet)`
- GitHub: search NeuralProphet + treasury repos

Save the results (including "0 relevant results" if that's the case) to a file in `ausindustry/` dated within the FY25 income period if possible — though even a search dated today is better than no search.

### 6b. "Industry treasury vendors (Kyriba, Cashforce, FIS) publish marketing claims but not reproducible architecture details"

**Claim as drafted:** Same as FY24, carried forward.

**What to verify:** This was true in FY24 and is still true in FY26 — these are commercial competitors. No change needed; the claim is defensible.

### 6c. "Microsoft Azure ML technical documentation"

**Claim as drafted:** Listed as a source investigated.

**What to verify:** This is a low-bar claim (everyone using Azure ML reads the docs). Defensible but unimpressive. Consider whether to keep it — Sources Investigated should focus on *substantive* prior art, not vendor docs.

---

## 7. Evidence retention claims

### 7a. The four ☑ Evidence checkboxes at the end of the activity

**Claim as drafted:** All four ticked:
- ☑ Evidence of searches or enquiries you made to find current knowledge
- ☑ Evidence to show that you could only determine the outcome of the core activity by conducting experiments as part of a systematic progression of work
- ☑ Evidence of your hypothesis and design of your experiments
- ☑ Documented results and evaluation of your experiments

**What to verify:**
- **Searches/enquiries:** Per 6a above — do you have search receipts? If not, do them now.
- **Systematic progression:** Are there git commits, PRs, or experiment notebooks dated across Jul 2024 – Jun 2025 that show the systematic progression? Tag/label them with the activity once registered.
- **Hypothesis design:** Is there a document (Notion, Confluence, repo doc, design doc) dated near the start of the FY25 work (Aug–Oct 2024 ideally) that states the hypothesis? Per Moreton, contemporaneous hypothesis records are the strongest evidence — *retrofitted* hypothesis docs are weak evidence.
- **Documented results:** Are there evaluation notebooks (Jupyter, Databricks, etc.) with timestamps, MAPE numbers, and the specific arms being compared?

**If any of these are missing:** Don't tick the box. Or, more practically, create the missing artifact today *as a real document of what was done*, not as a fabrication. A genuine retrospective summary written 30 Apr 2026 is honest evidence; a backdated "contemporaneous" doc is fraud.

### 7b. The project-level "documents kept" list

**Claim as drafted (in the project section, not the activity):** "Software Design documents. Software Architecture documents. Project Plan documents. Test Plan documents. Software Test Kit documents. Labour timesheets. Data collection logs."

**What to verify:**
- Each of these listed types should exist somewhere (SharePoint, GitHub, internal wiki) and be retrievable on request.
- "Software Test Kit documents" is a slightly unusual phrasing — make sure whatever this refers to actually exists.
- "Labour timesheets" is the critical one (per 3a above). These need to exist with sufficient granularity to support the 5 R&D FTE claim.

---

## 8. Things to remove or soften that don't help

### 8a. "Patentable tools"

**Claim as drafted:** "delivers patentable tools + further industry-specific validation"

**What to verify:** Has CAPIX filed any patents? Is it planning to? "Patentable" is a soft word but if AusIndustry is curious, they may ask.

**Recommendation:** Soft enough to leave. Just be ready to say "we have considered patent protection for specific feature engineering approaches" if asked.

### 8b. "FY26 agentic-AI direction"

**Claim as drafted:** "The FY25 results de-risk the FY26 agentic-AI direction by establishing a high-performing, explainable forecasting layer that an autonomous agent can trust."

**What to verify:** This is forward-looking and references FY26 work. It's helpful for showing systematic progression but adds little to the FY25 case.

**Recommendation:** Keep — it shows the progression continues per the multi-year project P160E5J1M structure. AusIndustry favourably views applicants who demonstrate systematic multi-year planning.

### 8c. "5x faster adaptation" type figures (not in current draft, but watch for them)

If the conclusions section drift toward asserting specific multipliers ("5x faster", "2.3x precision improvement"), require the same verification as 1a–1e. Quantitative claims need quantitative evidence.

---

## 9. Critical structural risks

### 9a. The "very similar" framing risk

The user requested Option B: FY24 hypothesis + FY25 delta. This is correct per Moreton ("multi-year registrations must show a progression of work"). The risk is that an assessor could read the FY25 application as **insufficient progression** — too similar to FY24, with the delta (FX features + NeuralProphet) not enough to justify a separate year of registered R&D.

**Mitigation:** The FY25 narrative as drafted does include genuine progression axes (FX volatility features, NeuralProphet preprocessing). To strengthen it:
- Make sure the **specific** experiments are dated and documented (Sep 2024 Azure migration, Feb 2025 FX features, Mar 2025 NeuralProphet) — these are the events that prove FY25 ≠ FY24.
- Be ready, if queried, to point to git commits, PRs, or design docs dated in those months.

### 9b. The FTE/expenditure proportionality risk

5 R&D FTE × ~12 months × loaded cost ≈ AUD 1M+ in salary alone. AUD 715,088 R&D expenditure suggests either: (a) FTE figure is overstated, (b) salaries are below the figure that would imply, or (c) the AUD 715,088 is salaries only and excludes other R&D-eligible spend (Azure compute, Bloomberg feed, etc.).

**Mitigation:** The accountant's workpaper for the AUD 715,088 figure should clearly reconcile to FTE × salary × R&D time fraction + other costs. If 5 R&D FTE is actually 5 *headcount* at 30–50% R&D allocation each, the defensible FTE figure on the form is 1.5–2.5, not 5. **This is the single most important number to get right.**

### 9c. The TA 2017/5 risk

The Software RDTI sector guide and Tax Payer Alert TA 2017/5 specifically target:
- Whole-of-product development claimed as R&D
- Routine engineering, integration, debugging claimed as R&D
- Internal-administration software claimed as R&D
- Beta testing in production claimed as R&D
- Customer support / customisation work claimed as R&D

**Mitigation:** The drafted FY25 core activity is narrowly hypothesis-bound (FX volatility features + NeuralProphet decomposition). This is the right framing. Risk emerges only if the AUD 715,088 figure includes routine engineering / customer work rather than just experimental work. See 3b above.

---

## 10. Pre-lodgement checklist

Before pasting into the AusIndustry portal:

- [ ] Numeric claims verified or softened (Section 1)
- [ ] Experimental design matches what actually ran (Section 2)
- [ ] FTE figure on form is defensible, with timesheet evidence (Section 3a) — **most important item**
- [ ] R&D expenditure figure reconciles to FTE × time fraction + other R&D costs (Section 3b)
- [ ] Timeline phases respect actual deployment dates (Section 4)
- [ ] Infrastructure claims describe what's used, not retrofitted dominant purpose (Section 5)
- [ ] At least one literature search performed and saved with dates (Section 6a)
- [ ] Evidence checkboxes ticked only for evidence that genuinely exists (Section 7)
- [ ] Typos in project section fixed (`spcifcally` → specifically, `facilites` → facilities, `Intellgence` → Intelligence, `coprights` → copyrights)
- [ ] "I agree" declaration ticked in the portal
- [ ] Software-sector "I acknowledge potential risks" ticked in the portal
- [ ] Declarant details confirmed (Peter Cooney, same as primary contact)

If anything material changes after lodgement (e.g., the FTE figure was wrong, conclusions overstated, an additional core activity should be added), use the **voluntary variation** mechanism within the 10-month window (i.e., before 30 Apr 2027 for the FY25 registration). Variations are routine; what is not recoverable is a registration that contains material misstatements not corrected by variation.

---

## 11. Notes for FY26 application

When this exercise repeats next April:

1. **Start the contemporaneous documentation in Q1 of the income year** (Jul–Sep 2025 for FY26). Hypothesis docs dated near the start of the experimental work are the single biggest evidence advantage. Don't write them retrospectively in April.
2. **Get the FTE allocation right at the time, not at year-end.** If R&D-allocated time is logged monthly via timesheets, the year-end figure is defensible. If it's reconstructed at year-end, it's weak.
3. **Save literature search receipts as you go.** Each time an engineer searches for "is there a published approach to X", screenshot/save the search before they start the experiment. This builds the "no applicable information" case naturally.
4. **The agentic-AI work** referenced in the website news log (Dec 2025 NeuralProphet ground-truthing, Jan–Mar 2026 agentic-AI articles) is FY26 R&D work. Frame it as the next progression axis under project P160E5J1M, with a hypothesis specific to autonomous agent behaviour.
5. **Consider whether to add supporting activities** in FY26. The FY25 form answered ☑ No, which is simple but excludes potentially eligible costs. If FY26 has clearly-scoped infrastructure work (e.g., Azure ML platform extensions specifically for agentic AI) with a defensible dominant-purpose argument, registering them as supporting activities captures more eligible expenditure. Not a default — only if dominant purpose is genuine.

---

## References

- Drafted core activity: [`2025-draft-application.md`](./2025-draft-application.md)
- FY24 application baseline: [`ausindustry-23-24-rd-application.md`](./ausindustry-23-24-rd-application.md)
- Strategy notes: [`FY2025-Application-Strategy.md`](./FY2025-Application-Strategy.md)
- Federal Court precedent on systematic progression: [`Moreton-Resources-v-ISA-FCAFC-2019-120.md`](./Moreton-Resources-v-ISA-FCAFC-2019-120.md)
- Software-related taxpayer alerts: [`TA-2017-5.md`](./TA-2017-5.md), [`TA-2017-5A.md`](./TA-2017-5A.md)
- General application guide: [`RDTI-Application-Guide.md`](./RDTI-Application-Guide.md)
- Software RDTI sector guide: [`Software-activities-and-the-RDTI.md`](./Software-activities-and-the-RDTI.md)
