# Open-Source Projects for CAPIX AI / Large Quantitative Model Development

A curated set of open-source projects worth evaluating for CAPIX's AI and large
quantitative model work, organized by role in the stack and focused on treasury /
capital-markets quantitative modeling.

> Internal planning document. Not published to the website.

## 1. Core ML / model-training frameworks
The foundation layer for training or fine-tuning large models.

- **PyTorch** — de facto standard for research and production model development.
  Mature ecosystem, best hiring pool.
- **JAX + Flax** — Google's high-performance autodiff/XLA stack. Strong for
  large-scale numerical and quantitative work where you want compiled, vectorized
  math (closer to "quant" code than typical deep learning).
- **Hugging Face Transformers / PEFT / Accelerate** — the practical toolkit for
  fine-tuning and deploying transformer models (including LoRA/QLoRA
  parameter-efficient tuning, which keeps GPU costs sane).
- **Ray** — distributed compute for scaling training, hyperparameter tuning
  (Ray Tune), and serving across a cluster.

## 2. Time-series & financial quantitative modeling
The most directly relevant category for treasury/markets.

- **Qlib** (Microsoft) — purpose-built AI quant investment platform: data handling,
  factor models, backtesting, and ML model pipelines for financial forecasting.
  Probably the single most relevant project to the CAPIX domain.
- **GluonTS** (Amazon) and **NeuralForecast / StatsForecast** (Nixtla) —
  probabilistic and neural time-series forecasting (cash-flow, FX, rate, liquidity
  forecasting).
- **Darts** — unified API spanning classical (ARIMA) to deep-learning forecasters;
  good for prototyping treasury forecasting models.
- **QuantLib** — the established library for derivative pricing, yield curves, fixed
  income, and risk — useful as the "ground truth" quantitative engine that ML models
  augment rather than replace.
- **Prophet** — quick, interpretable baseline forecasting.

## 3. LLM / foundation-model serving & orchestration
If "large quantitative model" includes LLM-augmented analytics or agentic workflows.

- **vLLM** — high-throughput LLM inference/serving (the standard for self-hosting
  open-weight models efficiently).
- **Open-weight model families** — **Llama**, **Mistral / Mixtral**, **Qwen**,
  **DeepSeek** — for self-hosted models where data residency/confidentiality of
  treasury data matters.
- **LangChain / LlamaIndex** — orchestration and RAG over internal documents/data.
- **Ollama** — easy local model hosting for dev/experimentation.

## 4. Experiment tracking, data & pipeline infrastructure
- **MLflow** — experiment tracking, model registry, lifecycle management.
- **DVC** — data and model versioning (critical for reproducibility and audit —
  important in a regulated financial context).
- **Feast** — feature store for serving consistent features to training and inference.
- **Apache Arrow / Polars / DuckDB** — fast columnar data processing for large
  market/time-series datasets (Polars and DuckDB in particular are excellent for
  quant data wrangling).
- **Optuna** — hyperparameter optimization.

## 5. Validation, explainability & risk
Matters for finance and regulatory governance.

- **SHAP / Captum** — model explainability, important for governance and
  regulator/auditor scrutiny.
- **Evidently** — data and model drift monitoring in production.
- **Great Expectations** — data quality/validation gates in pipelines.

## A pragmatic starting stack for CAPIX
A minimal, coherent combination to begin with:

**PyTorch + Qlib + Polars/DuckDB + MLflow + DVC**, adding **vLLM + an open-weight
model** if self-hosted LLM capability over confidential treasury data is needed.

## Decisions to make before committing
These change the recommendation materially:

1. **What is the "large quantitative model"** — a forecasting/risk model (favors
   Qlib, GluonTS, QuantLib), or an LLM-based analytics/agent system (favors vLLM,
   open-weight LLMs, LangChain)?
2. **Self-hosted vs. API** — does treasury-data confidentiality require everything
   on-prem/VPC, or can hosted model APIs be used for some parts?
3. **License constraints** — most above are permissive (Apache/MIT/BSD); a few model
   weights have usage restrictions worth checking against commercial use.
