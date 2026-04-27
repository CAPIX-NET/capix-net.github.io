# CAPIX Treasury Software - R&D Tax Incentive Application Guide

## Current Registration Status

| Field | Detail |
|-------|--------|
| **Entity** | CAPIX TREASURY SOFTWARE PTY LTD |
| **ABN** | 81 072 587 976 |
| **Director** | Peter Cooney |
| **Address** | L 2, 696 Bourke St, Melbourne VIC 3000 |
| **Email** | peter@capix.net |
| **Registration Number** | IR2411898 |
| **Income Year Registered** | 2023-2024 (1 Jul 2023 - 30 Jun 2024) |
| **Registration Date** | 22 May 2025 |
| **Reference** | 2324-AP00-052-445 |

**Status**: First-time registrant. Registration confirmed under section 27A of the *Industry Research and Development Act 1986*.

---

## Program Overview

The R&D Tax Incentive (RDTI) offsets eligible R&D costs via a tax offset on your income tax return.

### Tax Offset Rates

| Turnover | Offset | Type |
|----------|--------|------|
| **Under $20M** | Corporate tax rate + **18.5% premium** | **Refundable** (paid as cash even if in tax loss) |
| **$20M+** (R&D spend up to 2% of total expenses) | Corporate tax rate + 8.5% | Non-refundable |
| **$20M+** (R&D spend above 2% of total expenses) | Corporate tax rate + 16.5% | Non-refundable |

**CAPIX likely qualifies for the refundable offset** (corporate tax rate + 18.5% premium) as a small-to-medium software company with turnover under $20M. This means CAPIX can receive a **cash refund** even if in a tax loss position.

### Key Thresholds

- **Minimum claim**: $20,000 in notional R&D deductions (or use a registered Research Service Provider if under $20K)
- **Maximum claim**: $150M in R&D expenditure per year (amounts above this cap receive offset at the base corporate tax rate only)
- **Registration deadline**: Within **10 months** of the end of the income year (i.e., by 30 April for a standard 1 Jul - 30 Jun income year)

---

## Eligibility Criteria

### Entity Requirements (CAPIX meets all)

- [x] Incorporated under Australian law
- [x] Registered for income tax
- [x] Conducts at least one core R&D activity
- [x] R&D notional deductions of at least $20,000

### What Qualifies as Core R&D Activities

Core R&D activities must satisfy **all** of the following:

1. **Outcome cannot be known in advance** - A competent professional cannot determine the outcome based on current publicly available worldwide knowledge without conducting an experiment
2. **Systematic progression of work** - Based on principles of established science, progressing from hypothesis to experiment, observation, evaluation, and logical conclusions
3. **Substantial purpose of generating new knowledge** - The activity's primary aim is to create knowledge in materials, products, devices, processes, or services

### What Qualifies as Supporting R&D Activities

Supporting activities must:
- **Directly relate** to a core R&D activity
- Be conducted for the **dominant purpose** of supporting the core R&D activity
- Be documented at the time the activities occur

### Software-Specific Exclusion (Important)

Software developed for **internal administration** by the developer (or connected entities) is **excluded from core R&D**. However, it **may qualify as a supporting R&D activity** if its dominant purpose is supporting a core R&D activity.

**Key precedent**: Following the *Moreton Resources* court decision, "activities involving the application of existing technology in a different context or location are capable of meeting the definition of core R&D activities" if all legislative requirements are met.

---

## CAPIX R&D Activities - Mapping to RDTI Criteria

Based on a comprehensive review of the CAPIX website and product documentation, here are the R&D activities that are strong candidates for the RDTI claim, organised by core and supporting activities.

### CORE R&D ACTIVITY 1: AI/ML Hybrid Architecture for Cash Flow Forecasting

**Description**: Development of a novel hybrid AI architecture combining three complementary machine learning approaches (LSTM, Transformer models, and XGBoost) for treasury cash flow forecasting.

**Why it qualifies**:
- **New knowledge**: No existing publicly available solution combines LSTM temporal forecasting, Transformer multivariate sequence prediction, and XGBoost gradient boosting specifically for multi-currency treasury cash flow forecasting. The interaction effects between these three model types in a financial treasury context required experimentation.
- **Technical uncertainty**: How to optimally weight and ensemble three fundamentally different ML architectures for treasury-specific time series data; how to handle multi-currency correlations, FX volatility, and seasonality detection across weekly/monthly/quarterly/yearly cycles within a unified prediction framework.
- **Systematic progression**: Hypothesis-driven development from initial single-model experiments (June 2023) through evaluation of Prophet AI and NeuralProphet, to the current hybrid architecture with confidence bands and uncertainty quantification.

**Timeline**: June 2023 - ongoing

**Key technical challenges investigated**:
- Optimal ensemble weighting across LSTM, Transformer, and XGBoost for different forecast horizons
- Multi-currency handling with FX volatility metrics and currency correlations
- Seasonality detection algorithms for complex financial patterns
- Confidence band calibration and uncertainty quantification for CFO/auditor requirements
- Explainability integration (SHAP/attention mechanisms) for regulated financial environments

---

### CORE R&D ACTIVITY 2: Agentic AI for Autonomous Treasury Operations

**Description**: Development of AI agents that operate independently within governance boundaries to manage treasury cash flows autonomously - moving beyond prediction to autonomous decision-making.

**Why it qualifies**:
- **New knowledge**: Autonomous AI agents for treasury operations is a novel application. No existing publicly available system combines Large Language Model reasoning with real-time treasury data pipelines for autonomous cash management decisions within governance frameworks.
- **Technical uncertainty**: How to safely delegate treasury decisions to AI agents while maintaining audit compliance; how to design governance boundaries that allow useful autonomy without unacceptable risk; how to integrate LLM reasoning with real-time bank feeds, ERP data, and market data for reliable autonomous action.
- **Systematic progression**: Built upon the forecasting R&D (Activity 1), progressing from monitoring-only agents to intelligent reforecasting, then risk detection, and finally cash flow optimisation agents.

**Timeline**: March 2026 - ongoing

**Key technical challenges investigated**:
- Agent architecture for continuous real-time monitoring across accounts and currencies
- Automatic reforecasting triggers when new data invalidates current predictions
- Risk detection algorithms (liquidity shortfall prediction, FX exposure, counterparty concentration, anomaly identification)
- Policy-driven operational boundaries with kill-switch capability
- Complete audit trail generation for regulatory compliance
- Integration of LLM reasoning with structured treasury engine operations

---

### CORE R&D ACTIVITY 3: Financial Instrument Pricing Library Development

**Description**: Development and enhancement of proprietary pricing algorithms for bonds, options, swaps, and complex derivative instruments.

**Why it qualifies**:
- **New knowledge**: Advanced pricing models adapted for specific market conditions and instrument types not adequately served by existing libraries. Version v23.12.01 released December 2023 with new computational approaches.
- **Technical uncertainty**: Numerical methods for pricing exotic instruments; volatility surface construction; yield curve interpolation techniques for specific market microstructures.
- **Systematic progression**: Iterative development with mathematical hypothesis, implementation, backtesting against market data, and refinement.

**Timeline**: Ongoing (library upgraded to v23.12.01 in December 2023)

---

### SUPPORTING R&D ACTIVITY 1: Application Modernisation (Desktop to Cloud/Web)

**Description**: Migration of CTM from Windows desktop (Access/VBA) to Blazor Server web application on Azure, including VBA-to-VB.NET/C# code transformation and database migration.

**Why it qualifies as supporting**:
- Directly supports Core Activities 1 and 2 by providing the cloud-native platform required for AI/ML model integration and real-time data pipelines
- Dominant purpose: enabling the AI-enhanced treasury platform that the core R&D activities produce
- The modernisation creates the architectural foundation (Azure SQL, Azure Functions, Service Bus, real-time data pipelines) without which the AI/ML R&D cannot be deployed

**Key elements**:
- ~200 Access forms to Blazor Server conversion
- ~200 VBA modules to VB.NET/C# transformation
- 4 C++ DLLs (pricing, encryption, math) wrapper generation
- Azure SQL Database migration with Entity Framework Core
- Real-time data pipeline architecture for AI agent integration

---

### SUPPORTING R&D ACTIVITY 2: Cloud Infrastructure & Data Pipeline Development

**Description**: Design and implementation of Azure cloud infrastructure supporting real-time data ingestion, ML model serving, and autonomous agent operations.

**Why it qualifies as supporting**:
- Directly supports Core Activities 1 and 2
- Infrastructure required for: ERP data ingestion, bank feed processing, market data integration, ML model training/serving, and agent orchestration
- Technologies: Azure ML, Apache Kafka/Spark for streaming, FastAPI for model serving, Docker containerisation

---

### SUPPORTING R&D ACTIVITY 3: ERP Integration Layer

**Description**: Development of integration interfaces with SAP, Oracle, FinanceOne, and Microsoft Dynamics 365 for automated data ingestion into the AI forecasting and agent systems.

**Why it qualifies as supporting**:
- Directly supports Core Activity 1 (AI forecasting requires AP/AR/budget data from ERP systems)
- Dominant purpose is feeding the AI models with the structured financial data they need
- Includes feature engineering pipeline for transforming raw ERP data into ML-ready features

---

## Expenditure Categories to Claim

The following R&D expenditure types are typically claimable:

### Staff Costs (Largest Component)
- **Developer salaries** (proportioned to time spent on R&D activities)
- **Data scientist / ML engineer time** on AI/ML development
- **Domain expert time** (treasury/finance expertise applied to defining hypotheses and evaluating experimental outcomes)
- **Supervisor/management time** directly related to R&D activities

### Contractor Costs
- External AI/ML consultants
- Cloud architecture consultants
- Any Research Service Providers engaged

### Software & Cloud Costs
- Azure ML compute costs for model training
- Azure infrastructure costs attributable to R&D (dev/test environments)
- Software licences used exclusively or primarily for R&D (ML frameworks, development tools)

### Other Costs
- Training data acquisition/preparation
- Technical literature and research materials
- Depreciation of equipment used for R&D

### Important: Apportionment
Where staff or resources are used for both R&D and non-R&D work, costs must be **apportioned** based on the proportion of time/usage dedicated to R&D activities. Keep timesheets or time-tracking records.

---

## Record-Keeping Requirements

**Critical**: CAPIX must maintain contemporaneous records (created at the time of R&D activity). This is the single most important compliance requirement.

### Records to Maintain

| Record Type | What to Document |
|------------|-----------------|
| **Hypothesis documentation** | What you set out to discover; what outcome was uncertain |
| **Experiment logs** | What experiments/tests were conducted; methodology used |
| **Observation records** | Results of experiments; what was learned |
| **Evaluation notes** | Analysis of results; conclusions drawn |
| **Literature reviews** | Evidence that outcomes weren't known from existing knowledge |
| **Time records** | Staff time allocation between R&D and non-R&D work |
| **Financial records** | Expenditure directly attributable to R&D activities |
| **Meeting minutes** | Technical discussions about R&D direction and decisions |
| **Code commits/PRs** | Git history showing R&D development progression |
| **Architecture documents** | System design decisions and technical rationale |

### Recommended Documentation Structure

For each core R&D activity, maintain a log structured as:

```
1. HYPOTHESIS: What we set out to investigate
   - What was the technical uncertainty?
   - Why couldn't a competent professional determine the outcome?
   - What literature/knowledge review was conducted?

2. EXPERIMENT: What we did
   - Methodology and approach
   - Tools and technologies used
   - Date range of activity

3. OBSERVATION: What we found
   - Results of experiments
   - Unexpected findings
   - Performance metrics

4. EVALUATION: What we concluded
   - Did the hypothesis hold?
   - What new knowledge was generated?
   - How did this inform next steps?
```

---

## Next Steps for CAPIX

### For the 2023-2024 Income Year (Already Registered)

1. **Complete the ATO R&D Tax Incentive Schedule** when lodging the income tax return, referencing Registration Number **IR2411898**
2. **Calculate eligible R&D expenditure** for 1 Jul 2023 - 30 Jun 2024
3. **Ensure contemporaneous records exist** for all claimed activities in that period
4. **Apportion costs** where staff/resources were shared between R&D and commercial work

### For the 2024-2025 Income Year (Next Registration)

1. **Registration deadline**: By **30 April 2026** (10 months after 30 June 2025)
2. Start compiling expenditure records now
3. Maintain ongoing R&D activity logs (hypothesis-experiment-observation-evaluation)
4. Register via the customer portal at https://incentives.business.gov.au/

### For the 2025-2026 Income Year

1. **Registration deadline**: By **30 April 2027**
2. The Agentic AI work (Core Activity 2) falls primarily in this period
3. Continue maintaining contemporaneous records

### Ongoing Best Practices

- Keep a **dedicated R&D log/journal** updated weekly or fortnightly
- Use **git commit history** as supporting evidence of systematic progression
- Document **what didn't work** as well as what did (shows genuine experimentation)
- Record **literature reviews** and searches showing outcomes weren't already known
- Maintain **timesheets** showing staff allocation to R&D vs commercial work
- Separate **R&D Azure costs** from production costs in billing

---

## Key Contacts & Resources

| Resource | Detail |
|----------|--------|
| **AusIndustry Contact Centre** | 13 28 46 |
| **Email** | rdtaxincentive@industry.gov.au |
| **Customer Portal** | https://incentives.business.gov.au/ |
| **Main Guidance** | https://business.gov.au/rdti |
| **Software Sector Guide** | business.gov.au > R&DTI > Sector Guides > Software Development |
| **ATO R&D Schedule** | Completed with income tax return |

---

## Risk Areas to Watch

1. **Software internal administration exclusion**: CAPIX's products are sold to external customers (corporate treasuries, banks), so the core products are NOT internal administration software. However, any tools built solely for CAPIX's own internal use would be excluded from core R&D.

2. **Self-assessment responsibility**: Registration does not guarantee eligibility. CAPIX must self-assess that each claimed activity genuinely meets all the criteria.

3. **Compliance reviews**: AusIndustry and ATO may audit the claim at any time. Strong contemporaneous records are the best defence.

4. **Apportionment accuracy**: Over-claiming staff time on R&D when work was partly commercial is a common compliance issue. Be conservative and well-documented.

5. **Gambling/tobacco exclusion**: Not applicable to CAPIX (effective from income years starting 1 Jul 2025).

---

*Prepared: 31 March 2026*
*Based on: AusIndustry registration documents, business.gov.au RDTI guidance, CAPIX website content*
