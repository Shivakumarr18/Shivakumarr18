<div align="center">

![Aviation](https://images.unsplash.com/photo-1567446188601-95f43044f6dc?w=1200&q=80)


</div>

---

✈️ Aviation Data Engineering

shivakumar@aviation-de:~$ neofetch

Name ............. Narsing Shiva Kumar
Role ............. Associate Engineer → Data Engineer
Company .......... CAMP Systems (Aviation MRO Software)
Languages ........ Python · SQL · PySpark
Cloud ............ Azure Databricks · ADLS Gen2
Pipeline ......... Bronze → Silver → Gold
Architecture ..... Medallion + Kimball Star Schema
Domain ........... Aviation Operations (IOC/OCC)
Visualisation .... Power BI
GitHub ........... Shivakumarr18
Streak ........... Never breaks. Laptop travels everywhere.

✈️ BTS Aviation Delay Intelligence System

20.9M rows. 3 years. 15 carriers. 294 airports. One analytical model. Built from scratch.

BTS TranStats — US Bureau of Transportation Statistics
January 2023 → December 2025 | 36 monthly partitions | ~4GB raw
        │
        ▼
BRONZE  ✅ COMPLETE
36/36 partitions · 20,928,599 rows
Immutable · Append-only · Parquet · YEAR/MONTH
        │
        ▼
SILVER v4.0  ✅ COMPLETE
12 validation gates per partition
20,928,599 rows · NULLs preserved
        │
        ▼
GOLD · Kimball Star Schema  ✅ COMPLETE
9/9 artifacts · 10/10 GCG passed
fact_delays + 5 dims + bridge + 2 cost models
Azure Databricks · Standard_F4 · East US
Evidence captured: 2026-09-13
        │
        ▼
Power BI · REST API · AI Interface
⏳ NEXT

🏆 Gold Layer — Azure Evidence

Cluster  : Standard_F4 · East US · Azure Databricks
Storage  : ADLS Gen2 · btsaviation
Input    : 20,928,599 rows (Silver · Jan 2023 – Dec 2025)

GOLD ARTIFACTS (9/9):
  dim_date                   ✅
  dim_carrier                ✅
  dim_airport                ✅
  dim_aircraft               ✅
  dim_delay_reason           ✅
  fact_delays                ✅
  bridge_flight_delay_reason ✅
  model_cost_scenario        ✅
  model_delay_cost           ✅

GOLD COMPLETION GATE (10/10):
  GCG 01 — Artifacts exist      ✅ (9/9)
  GCG 02 — Row count            ✅ (20,928,599)
  GCG 03 — Grain uniqueness     ✅ (0 duplicates)
  GCG 04 — NULL foreign keys    ✅ (all zeros)
  GCG 05 — UNKNOWN members      ✅ (all 5 dims)
  GCG 06 — Surrogate key unique ✅ (all dims)
  GCG 07 — Partition count      ✅ (36/36)
  GCG 08 — arr_delay_mins       ✅ (152,637,336)
  GCG 09 — Cancellation count   ✅ (287,134)
  GCG 10 — Bridge integrity     ✅ (7,072,280 rows)

STATUS: GOLD LAYER COMPLETE ON AZURE ✅

📊 Delay-Cause Columns — Domain Context

Before writing the analytical model, I studied airline operations and the role of the IOC — the operational nerve centre of an airline.

BTS records delay categories as reported. This project uses aviation domain knowledge to contextualise those categories — not to overclaim causation.

Column

BTS Definition

Domain Context — DERIVED, not BTS truth

CARRIER_DELAY

Delay within airline control as reported

May be consistent with airline-controlled operational issues such as crew, aircraft, maintenance or ground-service factors. BTS does not specify the underlying event.

WEATHER_DELAY

Weather conditions as reported by carrier

Consistent with operational effects associated with adverse weather scenarios.

NAS_DELAY

National Airspace System delay as reported

Consistent with ATC restrictions, congestion, ground stops and other NAS-related constraints.

SECURITY_DELAY

Security delay as reported

Represents delays attributed to security-related circumstances.

LATE_AIRCRAFT_DELAY

Late arriving aircraft as reported

Used as a potential cascade-propagation signal and schedule-robustness indicator.

NULL in cause fields

Delay-cause fields not populated

Preserved as-is. Not interpreted as either “no cause” or “unknown cause” without supporting evidence.

🏗️ Architecture Decision Records

ADR

Decision

Why

ADR-GOLD-001

Snapshot dimensions for v1

BTS does not provide the attribute-change history required to justify a traditional SCD2 implementation.

ADR-GOLD-002

Bridge table for delay reasons

A flight can contain multiple reported delay causes. A single FK would discard information.

ADR-GOLD-003

operational_influence_class instead of is_controllable

BTS cannot establish whether a delay was operationally controllable. A binary label would overclaim.

ADR-GOLD-004

monotonically_increasing_id for v1

SHA-256-based deterministic keys deferred to a future Azure implementation.

ADR-GOLD-005

Cost model in separate tables

Observed operational metrics and modeled cost assumptions must remain explicitly separated.

ADR-GOLD-006

Aircraft keyed by tail_number

Avoids unnecessary fan-out caused by combining aircraft identity with carrier ownership.

🧠 Domain Foundation

📖 Peter J. Bruce — Airline Operations Control

Ch 1 → IOC fundamentals.
       Safety, legality and efficiency as operational priorities.

Ch 3 → How airline schedules are constructed.
       Hubs, point-to-point networks, slots, curfews and robustness.

Ch 4 → What happens when the operating plan breaks.
       IROPS and disruption propagation.

Ch 5 → How operational information moves during disruption.
       Coordination and information propagation.

📄 Ferguson et al. (FAA/NEXTOR 2010)

→ $45/min reference for US airline delay-cost analysis.
→ Airborne delay costs substantially exceed equivalent ground delay.
→ Used only as a cited assumption in the Gold cost-sensitivity model.

📈 Current Status — September 2026

Layer

Local

Azure

Evidence

Health Check

✅ 14/14

—

36 CSVs validated before ingestion

Bronze

✅ 36/36

✅ 36/36

20,928,599 rows · Parquet

Silver v4.0

✅ 36/36

✅ Complete

12 validation gates · frozen

Gold

✅ Complete

✅ Complete

9/9 artifacts · Kimball star schema

Gold GCG

✅ 10/10

✅ 10/10

0 duplicate grains · 0 NULL FKs

Power BI

🔲

🔲

Next

REST API

🔲

🔲

After Power BI

AI Interface

🔲

🔲

Final application layer

🛠️ Tech Stack

Language        Python 3.11 · SQL
Processing      PySpark 3.x · Azure Databricks
Storage         Azure Data Lake Storage Gen2 · Parquet
Orchestration   Azure Data Factory (planned)
Visualisation   Power BI
Architecture    Medallion Architecture · Kimball Star Schema
Evidence states OBSERVED · DERIVED · MODELED · INFERRED · UNKNOWN

Engineering standard:
    Type hints · docstrings · explicit validation · structured logging
    · failure visibility · reproducible evidence

🎯 Platform Boundary — What This System Is and Is Not

✅ CAN DO
   Historical delay pattern analysis
   Carrier performance comparison
   Route exposure quantification
   Tail-number cascade analysis
   Delay-cause distribution analysis
   Cost sensitivity modelling using cited assumptions

❌ CANNOT DO
   Real-time IOC operational control
   Live crew legality assessment
   Live weather or ATC feed analysis
   Passenger-level impact tracking
   Real-time disruption prediction
   Prescriptive operational recommendations

These boundaries are intentional.

The system distinguishes what the source data can demonstrate from what would require additional operational datasets, validated predictive models and real-time integrations.

Direction   : Data Engineering → AI Data Platform
Status      : Gold complete. Descending into Power BI.
Foundation  : Domain Knowledge + Technical Depth + Trusted Data
Scale       : 20,928,599 Silver records · 3 years · 36 partitions

Building in public. Domain first. Code second. Evidence always.
