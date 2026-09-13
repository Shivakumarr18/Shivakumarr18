<div align="center">

![Aviation](https://images.unsplash.com/photo-1567446188601-95f43044f6dc?w=1200&q=80)

</div>

---

<div align="center">

# ✈️ Aviation

### Aviation Data Engineering | Python · SQL · PySpark · Azure

Building reliable data systems for aviation analytics — with a long-term focus on AI-ready data platforms.

[![GitHub](https://img.shields.io/badge/GitHub-Shivakumarr18-181717?style=flat&logo=github)](https://github.com/Shivakumarr18)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin)](https://www.linkedin.com/)

📍 Hyderabad, India

</div>

---

## 👋 About

I'm an Associate Engineer at **CAMP Systems**, working in aviation software and building toward Data Engineering.

My current focus is on developing strong foundations in:

- Data Engineering
- Aviation analytics
- Distributed data processing
- Cloud data platforms
- Data quality and validation
- AI-ready analytical systems

I care less about simply moving data and more about building **trusted data foundations that can support reliable business analysis and AI applications.**

---

# ✈️ Featured Project

## BTS Aviation Delay Intelligence System

**20.9M flight records · 3 years · 36 monthly partitions · Azure**

An end-to-end aviation data engineering platform built using US Bureau of Transportation Statistics flight data.

The system transforms raw flight records into a validated analytical model designed for downstream BI, APIs and eventually an AI interface.

### Architecture

| Stage | Status |
|---|---|
| Source validation | ✅ Complete |
| Bronze layer | ✅ Complete |
| Silver layer | ✅ Complete |
| Gold dimensional model | ✅ Complete |
| Azure validation | ✅ Complete |
| Semantic / business layer | 🔲 Next |
| Power BI analytics | 🔲 Planned |
| REST API | 🔲 Planned |
| AI Analyst interface | 🔲 Planned |

### Scale

| Metric | Value |
|---|---:|
| Source period | Jan 2023 – Dec 2025 |
| Silver records | **20,928,599** |
| Monthly partitions | **36** |
| Raw data | ~4 GB |
| Carriers | 15 |
| Airports | 294 |

---

## 🏆 Gold Layer — Azure Validation

The Gold layer has been completed on Azure Databricks with explicit completion gates.

| Validation | Result |
|---|---:|
| Gold artifacts | **9 / 9 PASS** |
| Completion gates | **10 / 10 PASS** |
| Grain duplicates | **0** |
| NULL foreign keys | **0** |
| Unknown dimension members | **Validated** |
| Surrogate-key uniqueness | **Validated** |
| Partitions | **36 / 36** |
| Arrival-delay minutes | **152,637,336** |
| Cancellations | **287,134** |
| Bridge records | **7,072,280** |

**Azure evidence captured:** September 13, 2026

---

## 🧱 Gold Model

The analytical model currently contains:

| Artifact | Purpose |
|---|---|
| `dim_date` | Date analysis |
| `dim_carrier` | Carrier analysis |
| `dim_airport` | Airport analysis |
| `dim_aircraft` | Aircraft / tail-number analysis |
| `dim_delay_reason` | Delay-cause analysis |
| `fact_delays` | Core flight-delay facts |
| `bridge_flight_delay_reason` | Multi-cause delay relationships |
| `model_cost_scenario` | Cost sensitivity assumptions |
| `model_delay_cost` | Modeled delay-cost outputs |

---

## 🧠 Engineering Principles

### Evidence boundaries

The system explicitly separates:

**OBSERVED → DERIVED → MODELED → INFERRED → UNKNOWN**

This prevents analytical assumptions from being presented as source facts.

### Key architecture decisions

| Decision | Reason |
|---|---|
| Snapshot dimensions | BTS does not provide sufficient history for justified SCD2 |
| Bridge table | A flight can have multiple reported delay causes |
| `operational_influence_class` | Avoids unsupported claims about controllability |
| Separate cost models | Observed metrics and modeled assumptions remain distinct |
| Tail-number aircraft key | Avoids unnecessary fan-out across carriers |

---

# 🛠️ Technical Stack

| Area | Technologies |
|---|---|
| Languages | Python · SQL |
| Processing | PySpark |
| Cloud | Microsoft Azure |
| Compute | Azure Databricks |
| Storage | ADLS Gen2 · Parquet |
| Architecture | Medallion Architecture |
| Data Modeling | Kimball Star Schema |
| Orchestration | Azure Data Factory |
| Visualization | Power BI |
| Future Interface | REST API · AI Interface |

---

# ✈️ Aviation Domain Focus

The project is intentionally grounded in airline operational concepts including:

- IOC / OCC operations
- Irregular Operations (IROPS)
- Delay propagation
- Schedule robustness
- Airline network operations
- Delay-cause analysis
- Operational cost sensitivity

BTS delay categories are treated as **reported source information**. Aviation domain knowledge is used to contextualize the data without claiming unsupported causation.

---

# 🎯 Platform Boundary

### Currently supported

- Historical delay analysis
- Carrier performance analysis
- Airport and route exposure analysis
- Tail-number cascade analysis
- Delay-cause distribution
- Cost sensitivity modeling

### Not currently supported

- Real-time IOC control
- Live crew legality
- Live weather / ATC feeds
- Passenger-level impact
- Real-time disruption prediction
- Prescriptive operational recommendations

These boundaries are intentional.

The goal is to clearly distinguish what the available data can demonstrate from what would require additional operational datasets and real-time integrations.

---

# 🚀 Roadmap

| Stage | Status |
|---|---|
| Source validation | ✅ Complete |
| Bronze layer | ✅ Complete |
| Silver layer | ✅ Complete |
| Gold dimensional model | ✅ Complete |
| Azure validation | ✅ Complete |
| Semantic / business layer | 🔲 Next |
| Power BI analytics | 🔲 Planned |
| REST API | 🔲 Planned |
| AI Analyst interface | 🔲 Planned |

### Long-term direction

**Trusted Data → Semantic Understanding → AI Analysis → Business Decision Support**

The objective is not simply to add AI to a data pipeline.

The objective is to build the **trusted data foundation that makes AI analysis defensible.**

---

# 📂 Projects

### ✈️ BTS Aviation Delay Intelligence — Core Project
20M+ US flight records · PySpark · Azure Databricks · ADLS Gen2 · Kimball Star Schema

End-to-end medallion pipeline on 3 years of US domestic flight data.
Bronze → Silver → Gold. 9/9 artifacts. 10/10 completion gates. Azure validated.

👉 [View Repository](https://github.com/Shivakumarr18/BTS-Aviation-Delay-Intelligence)

---

### 🛫 NASA ASRS Pipelines — Practice Project
Aviation safety data engineering pipeline built before the core project.
Python · SQL · MySQL · Medallion architecture · 4,500 NASA safety reports.

Built to develop foundational pipeline skills before working at production scale.

👉 [View Repository](https://github.com/Shivakumarr18/NASA-ASRS-Pipelines)

---

<div align="center">

### Building in public.

**Domain first. Code second. Evidence always.**

✈️ Aviation · Data Engineering · Cloud · AI Platforms

</div>
