<div align="center">

![Aviation](https://images.unsplash.com/photo-1567446188601-95f43044f6dc?w=1200&q=80)

# ✈️ Aviation

</div>

---

<div align="center">

```
shivakumar@aviation-de:~$ neofetch
```

</div>

```
                                        Name ............. Narsing Shiva Kumar
✈  climbing to cruise
        /                                Company .......... CAMP Systems (Aviation MRO Software)
       /   BTS Aviation Delay            
      /    Intelligence System           
     /     20.9M rows · 2023–2025
    /                                    Languages ........ Python · SQL · PySpark
                                         Cloud ............ Azure Databricks · ADLS Gen2
                                         Pipeline ......... Bronze → Silver → Gold (Medallion)
                                         Schema ........... Kimball Star Schema
                                         Domain ........... Aviation Operations (IOC/OCC)
                                         Visualisation .... Power BI

                                         GitHub ........... Shivakumarr18
                                         Streak ........... Never breaks. Laptop travels everywhere.
```

---

## ✈️ BTS Aviation Delay Intelligence System

> *"20.9M rows. 3 years. 15 carriers. 294 airports. One star schema. Built from scratch."*

```
  BTS TranStats — US Bureau of Transportation Statistics
  January 2023 → December 2025  |  36 CSV files  |  ~4GB raw
           │
           ▼
    ┌──────────────────────────────────────────────────────┐
    │   BRONZE                                             │
    │   36/36 partitions  ·  20,928,599 rows               │
    │   Immutable · Append-only · Parquet · YEAR/MONTH     │
    └──────────────────────┬───────────────────────────────┘
                           │
                           ▼
    ┌──────────────────────────────────────────────────────┐
    │   SILVER  v4.0  ·  FROZEN  ·   │
    │   12 validation gates per partition                  │
    │   20,928,599 rows  ·  NULLs preserved. Never filled. │
    └──────────────────────┬───────────────────────────────┘
                           │
                           ▼
    ┌──────────────────────────────────────────────────────┐
    │   GOLD  ·  Kimball Star Schema                       │
    │   fact_delays + 5 dimensions + bridge table          │
    │   Cost model separated  ·  IOC pillars mapped        │
    │   Local TEST_MODE: 8/8 TCG passed                    │
    │   Azure Full Run: IN PROGRESS ← TODAY                │
    └──────────────────────────────────────────────────────┘
                           │
                           ▼
              Power BI  ·  REST API  ·  AI Interface
```

---

## 📊 The 5 Delay Columns — Domain Context

> *Before writing a single line of code, I studied the IOC — the nerve centre of every airline.*
> *BTS records delay categories as reported. This project uses domain knowledge to contextualise them — not to overclaim causation.*

| Column | BTS Definition | Domain Context (DERIVED — not BTS truth) |
|--------|---------------|------------------------------------------|
| `CARRIER_DELAY` | Delay within airline control as reported | May include MEL faults · crew issues · aircraft swaps · GPU failures · fuelling — BTS does not specify which |
| `WEATHER_DELAY` | Weather conditions as reported by carrier | Consistent with fog · crosswinds · thunderstorms · snow · heat scenarios |
| `NAS_DELAY` | National Airspace System delay as reported | Consistent with ATC ground stops · GDPs · runway closures · congestion |
| `SECURITY_DELAY` | Security delay as reported | Consistent with screening events · terminal issues |
| `LATE_AIRCRAFT_DELAY` | Late arriving aircraft as reported | Interpreted as cascade propagation signal — schedule robustness indicator |
| **`NULL in cause fields`** | Delay-cause fields not populated | Preserved as-is. Expected for flights where reportable delay-cause values are absent. Not treated as failure or success. |

---

## 🏗️ Architecture Decision Records

| ADR | Decision | Why |
|-----|----------|-----|
| ADR-GOLD-001 | Snapshot dimensions for v1 | No attribute change events in BTS. Fake SCD2 is dishonest. |
| ADR-GOLD-002 | Bridge table for delay reasons | One flight can have multiple causes. Single FK discards information. |
| ADR-GOLD-003 | `operational_influence_class` not `is_controllable` | BTS cannot prove controllability. Binary True/False overclaims. |
| ADR-GOLD-004 | `monotonically_increasing_id` for v1 | SHA-256 deferred to Azure v2. |
| ADR-GOLD-005 | Cost model in separate tables | Observed ≠ Modeled. Evidence boundary must be explicit. |
| ADR-GOLD-006 | Aircraft keyed by `tail_number` only | Including carrier_code causes fan-out across operators. |

---

## 🧠 Domain Foundation

```
📖 Peter J. Bruce — Airline Operations Control

   Ch 1  →  What the IOC is. Three pillars: Safety > Legality > Efficiency.
             Every delay column maps to one of these three.

   Ch 3  →  How the schedule is built months before the day.
             Hub vs point-to-point. Slots. Curfews. Schedule robustness.

   Ch 4  →  What happens when the plan breaks.
             IROPS spectrum. Every disruption type decoded to its BTS column.

   Ch 5  →  How information flows during disruption.
             Cascade intelligence. Information propagation patterns.

📄 Ferguson et al. (FAA/NEXTOR 2010)
   → US airline cost-of-delay: $45/min reference.
   → Airborne delay costs ~20x ground delay per minute.
   → Applied to Gold layer cost sensitivity calculator.
```

---

## 📈 Current Status — September 2026

| Layer | Local | Azure | Evidence |
|-------|-------|-------|----------|
| Health Check | ✅ 14/14 | — | Pre-ingestion. All 36 CSVs validated. |
| Bronze | ✅ 36/36 | ✅ 36/36 | 20,928,599 rows. Parquet. Immutable. |
| Silver v4.0 | ✅ 36/36 | ✅ Uploaded | 20,928,599 rows. 12 gates. Frozen. |
| Gold TEST_MODE | ✅ 8/8 TCG | — | 99,972 rows. 36/36 partitions covered. |
| Gold Full Run | ⏳ Fix needed | ⏳ PENDING | `os.path.exists` → ADLS fix. Today. |
| GCG 10 checks | ⏳ | ⏳ | After Gold Azure run passes. |
| Power BI | 🔲 | 🔲 | After Gold Azure evidence. |
| REST API | 🔲 | 🔲 | After Power BI. |

---

## 🛠️ Tech Stack

```
Language        Python 3.11 · SQL
Processing      PySpark 3.x · Azure Databricks
Storage         Azure Data Lake Storage Gen2 · Parquet
Orchestration   Azure Data Factory (planned)
Visualisation   Power BI
Format          Medallion Architecture (Bronze → Silver → Gold)
Schema          Kimball Star Schema
Evidence states OBSERVED · DERIVED · MODELED · INFERRED · UNKNOWN
Standard        type hints · docstrings · errors as UI
```

---

## 🎯 Platform Boundary — What This System Is and Is Not

```
✅  CAN DO
    Historical delay pattern analysis
    Carrier performance comparison
    Route exposure quantification
    Tail number cascade propagation
    Cost sensitivity modelling (cited assumptions)

❌  CANNOT DO
    Real-time IOC operational control
    Live crew legality assessment
    Live weather or ATC feed
    Passenger-level impact tracking
```

---

<div align="center">

```
  Altitude    : Climbing through Gold layer
  Fuel        : Domain Knowledge + Technical Depth + 20.9M rows
  ETA         : On Schedule
```

*Building in public. Domain first. Code second. Insights always.*

**Industry Advisors:** · Luis R. Meza (Aviation Director) · Jack Yang (Airlines CEO)

</div>
