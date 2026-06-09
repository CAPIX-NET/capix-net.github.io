---
layout: page
title: Local AI Hardware for Treasury
subtitle: Bringing Large Quantitative Models In-House
description: CAPIX is moving large quantitative AI models from the cloud to local hardware for greater control, data sovereignty and efficiency — with the NVIDIA DGX Spark at the centre of our strategy.
permalink: /ai/local-hardware/
---
## Running Large Quantitative Models on Local Hardware

### A Shift from Cloud to On-Premise AI

For several years CAPIX has run its AI cashflow forecasting and risk models on cloud infrastructure, taking advantage of the scalability and managed services that platforms such as Microsoft Azure provide. That approach served us well as we developed and validated our [hybrid forecasting models](/ai/) and [autonomous treasury agents](/ai/agents/).

As our models have grown larger and more central to the way our customers manage liquidity, we have been re-evaluating where that compute should live. Increasingly, the answer is **on local hardware, in-house**. We are excited about what this means for control, data sovereignty, cost predictability and raw efficiency — and the **NVIDIA DGX Spark** is at the centre of this strategy.

---

### Why Move Away from the Cloud?

The cloud is not going away at CAPIX, but for the heavy, sustained workloads of training and running large quantitative models, local hardware is increasingly the better fit. Several factors are driving the shift:

#### Data Sovereignty and Control

Treasury data is among the most sensitive information a business holds — bank balances, payment instructions, counterparty exposures and forecasts. Running models on hardware we own and operate means that this data never has to leave our controlled environment to be processed by a third-party AI service. For customers with strict data-residency and confidentiality requirements, in-house inference removes an entire category of risk.

#### Cost Predictability

Cloud GPU instances are powerful, but for continuous, round-the-clock model training and inference the metered costs add up quickly and can be hard to forecast. Owning the hardware converts an unpredictable operating expense into a known, fixed capital cost. For workloads that run constantly — exactly the profile of our autonomous treasury agents — the economics increasingly favour local compute.

#### Efficiency and Latency

Keeping the model, the data and the application close together removes network round-trips and the overhead of moving large datasets in and out of the cloud. Lower latency means faster reforecasting when new transactions arrive, and tighter feedback loops when we are iterating on model design.

#### Independence

Running our own AI infrastructure reduces our dependence on the availability, pricing and policy decisions of external providers. We control the full stack — from the silicon to the model weights to the treasury application that consumes them.

---

### Why the NVIDIA DGX Spark?

The **NVIDIA DGX Spark** is a compact AI supercomputer built on the NVIDIA GB10 Grace Blackwell platform, designed to bring data-centre-class AI capability to the desk. It is exactly the kind of hardware that makes in-house AI practical for a focused team like ours.

What excites us about the DGX Spark for treasury workloads:

- **Serious compute in a small footprint** — petaFLOP-class AI performance in a unit that sits on a desk, with no data-centre buildout required
- **Large unified memory** — enough coherent CPU + GPU memory to hold and run large quantitative models locally, including the larger language and time-series models we use for reasoning and forecasting
- **The full NVIDIA AI stack** — CUDA, cuDNN and the broader ecosystem our existing PyTorch and TensorFlow models already target, so our work moves across with minimal friction
- **Local fine-tuning and inference** — the ability to fine-tune models on our own treasury datasets and serve them entirely on-premise
- **Scalability** — units can be paired and clustered as our model and workload sizes grow

In short, the DGX Spark lets us train, fine-tune and serve large models in-house with capability that until recently required a cloud GPU cluster.

---

### What This Means for Our Models

CAPIX's forecasting and risk platform is built on a hybrid of model types — **LSTM** and **Transformer** networks for temporal forecasting, **XGBoost** for structured tabular data, and **large language models** for the reasoning layer behind our [autonomous agents](/ai/agents/). These are increasingly large quantitative models, and they benefit directly from dedicated local acceleration.

Bringing them in-house allows us to:

- **Train and retrain faster**, iterating on model architecture and features without waiting on cloud capacity or watching the meter
- **Fine-tune on sensitive data safely**, adapting models to customer-specific patterns without that data leaving a controlled environment
- **Run inference continuously** for our always-on monitoring and forecasting agents, at predictable cost
- **Experiment more freely**, because the marginal cost of an additional training run is our own electricity rather than a cloud invoice

---

### A Hybrid Future

This is not an all-or-nothing move. We see a **hybrid model** as the future: local hardware such as the DGX Spark for the heavy, sustained and data-sensitive workloads, complemented by cloud resources where elastic scale or geographic reach genuinely adds value. The goal is to put each workload where it runs best — in terms of control, cost and performance — rather than defaulting everything to the cloud.

For our customers, the benefit is straightforward: AI-driven treasury tools that are faster, more cost-efficient, and built on infrastructure where data sovereignty and control are designed in from the start.

---

### Learn More

CAPIX continues to invest in the infrastructure behind our AI treasury solutions. To discuss how our AI-enhanced forecasting and autonomous agents could work for your organisation, [contact us](/contact/) for a consultation.

_CAPIX – empowering better decisions through intelligent treasury solutions._
