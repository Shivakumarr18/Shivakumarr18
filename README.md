```
                                                    __|__
                                             --o--o--(_)--o--o--
                                               /            \
  ________________________________________________/____________\________________________________________________
 /                                                                                                              \
|   ██████╗ ████████╗███████╗    ██████╗ ██╗██████╗ ██╗      ██████╗ ██████╗ ███████╗    ██████╗              |
|   ██╔══██╗╚══██╔══╝██╔════╝    ██╔══██╗██║██╔══██╗██║     ██╔═══██╗██╔══██╗██╔════╝    ╚════██╗             |
|   ██████╔╝   ██║   ███████╗    ██████╔╝██║██████╔╝██║     ██║   ██║██████╔╝███████╗     █████╔╝             |
|   ██╔══██╗   ██║   ╚════██║    ██╔═══╝ ██║██╔═══╝ ██║     ██║   ██║██╔═══╝ ╚════██║    ██╔═══╝             |
|   ██████╔╝   ██║   ███████║    ██║     ██║██║     ███████╗╚██████╔╝██║     ███████║    ███████╗             |
|   ╚═════╝    ╚═╝   ╚══════╝    ╚═╝     ╚═╝╚═╝     ╚══════╝ ╚═════╝ ╚═╝     ╚══════╝    ╚══════╝             |
 \______________________________________________________________________________________________________________/
```

<div align="center">

```
                    *      .                    .         *
           .                      *                               .
                  .          ___       *              .
      *                    -=|||=-                          *
              .           __/ | \__          .
                         /  \_|_/  \                  .
                        /_____|_____\           *
                       /  __|   |__  \
          .           /__/  |   |  \__\              .
                     /______\   /______\
                    (_________)(_________)
                              |_|
                       _______|_|_______
                      /___________________\
             *       /                     \        *
                    /   BTS AVIATION DELAY   \
                   /   INTELLIGENCE SYSTEM    \
          .       /___________________________\        .
                 (_____________________________) 
```

</div>

---

```
shivakumar@aviation-de:~$ neofetch
```

```
                    ✈                          shivakumar .................. Narsing Shiva Kumar
              ____/|____                       Role ........................ Associate Engineer → Data Engineer
           __/          \__                    Company ..................... CAMP Systems (Aviation MRO)
          /    BTS 2023-25  \                  Experience .................. 3.5 years
         /   18M+ rows       \                 Target ...................... Data Engineering | Oct 2026
        /   Medallion Pipeline \               
       /    PySpark · Databricks \             Languages.Programming ....... Python, SQL, PySpark
      /      Azure · Power BI    \             Languages.Data .............. SQL, HiveQL, DAX
_____/____________________________\_____       Cloud ....................... Azure (Databricks, ADLS Gen2)
~  ~  ~  ~  ~  ~  ~  ~  ~  ~  ~  ~  ~        Pipeline .................... Bronze → Silver → Gold
                                               Schema ...................... Kimball Star Schema
                                               Domain ...................... Aviation Operations (IOC/OCC)
                                               
                                               GitHub.Repos ............... BTS-Aviation-Delay-Intelligence
                                               GitHub.Stars ............... (building in public)
                                               GitHub.Commits ............. Every session. No breaks.
                                               
                                               Email ....................... [your email]
                                               LinkedIn .................... linkedin.com/in/[your handle]
                                               Standard .................... Sachin Standard 🏏
```

---

## ✈️ BTS Aviation Delay Intelligence System

> *"Every row in aviation operational data is a record of a human decision made under pressure."*

```
PIPELINE ARCHITECTURE
─────────────────────────────────────────────────────────────────────

  BTS TranStats API          
  (2023 · 2024 · 2025)       
  ~570K rows/month           
       │                     
       ▼                     
  ┌─────────────┐            
  │   BRONZE    │  ← Raw ingestion. Immutable. Append-only.
  │  Parquet    │    43 columns. ~20.9M rows. 
  │  ADLS Gen2  │    Nulls preserved. Never fabricated.
  └──────┬──────┘            
         │                   
         ▼                   
  ┌─────────────┐            
  │   SILVER    │  ← Cleaned. Validated. Conformed.
  │  PySpark    │    Null validation rules applied.
  │  Databricks │    ARR_DELAY nulls for cancellations NEVER filled.
  └──────┬──────┘            
         │                   
         ▼                   
  ┌─────────────┐            
  │    GOLD     │  ← Kimball Star Schema. Business ready.
  │  Star Schema│    fact_delays + 5 dimension tables
  │  Power BI   │    IOC-domain-aware metrics. 
  └─────────────┘    

─────────────────────────────────────────────────────────────────────
```

### The 5 Delay Cause Columns — Decoded

```
┌──────────────────────┬────────────────────────────────────────────────────────┐
│ BTS Column           │ What Generated It (IOC Domain Knowledge)               │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ CARRIER_DELAY        │ MEL faults · crew duty breaches · aircraft swaps ·     │
│                      │ fuelling decisions · GPU failures · paperwork delays   │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ WEATHER_DELAY        │ Fog · crosswinds · thunderstorms · snow · heat ·       │
│                      │ Safety pillar override. Airline not accountable.        │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ NAS_DELAY            │ ATC ground stops · GDPs · runway closures ·            │
│                      │ airspace restrictions · congestion                     │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ SECURITY_DELAY       │ Terminal evacuations · re-screening events ·           │
│                      │ overflight clearance issues. Rare. High duration.      │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ LATE_AIRCRAFT_DELAY  │ Propagation signal. Previous rotation was late.        │
│                      │ Schedule too tight. No buffer. Cascade, not cause.     │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ NULL (84% of rows)   │ ← SUCCESS. IOC recovered the flight on time.           │
│                      │   Not missing data. Operational intelligence.          │
└──────────────────────┴────────────────────────────────────────────────────────┘
```

---

## 🏗️ Architecture Decision Records

| ADR | Decision | Rationale |
|-----|----------|-----------|
| ADR-GOLD-001 | SCD Type 1 for dimensions | Operational simplicity. Historical tracking not required at this grain. |
| ADR-GOLD-002 | Delay reason as separate dimension | CARRIER_DELAY is composite. Cannot treat it as atomic. |
| ADR-GOLD-003 | Surrogate keys over natural keys | Isolation from source system changes. Standard Kimball practice. |
| ADR-GOLD-004 | Cost model separated from fact table | Assumptions must be explicit and auditable. Not embedded in data. |
| ADR-GOLD-005 | Aircraft dimension included | TAIL_NUM enables cascade chain analysis across rotations. |
| ADR-GOLD-006 | ARR_DELAY nulls for cancellations preserved | Cancelled flights have no arrival. NULL is correct. Never fill with 0. |

---

## 📊 Gold Layer Metrics

```python
# The metrics that matter — domain justified, not just aggregated

metrics = {
    "OTP"              : "% flights where ArrDel15 = 0  |  Primary IOC KPI",
    "cascade_ratio"    : "LATE_AIRCRAFT per initial delay  |  Schedule robustness signal",
    "airborne_recovery": "ARR_DELAY - DEP_DELAY  |  Tailwinds and routing intelligence",
    "nAS_heatmap"      : "NAS_DELAY by airport × hour × season  |  ATC pattern detection",
    "event_detection"  : "3-phase pattern (NAS spike → LATE wave → CANCELLATION)  |  Storm fingerprint",
    "cost_sensitivity" : "User inputs cost/min  →  System outputs exposure  |  Defensible estimate",
}
```

---

## 🧠 Domain Foundation

```
Before writing a single line of code, I studied:

  📖 Peter J. Bruce — "Airline Operations Control"
     
     Chapter 1  →  What the IOC is and why it exists
                    The three pillars: Safety > Legality > Efficiency
                    Every delay column maps to one of these three.
     
     Chapter 3  →  How the schedule is built months before the day
                    Hub vs point-to-point cascade risk
                    Slots, curfews, schedule robustness, buffer time
     
     Chapter 4  →  What happens when the plan breaks
                    IROPS spectrum: minor to 4-5 day network recovery
                    Every disruption type decoded to its BTS column

  Result: 18 million rows read as operational intelligence, not just data.
```

---

## 🛠️ Tech Stack

```
Language        Python 3.11 · SQL
Processing      PySpark 3.x · Azure Databricks
Storage         Azure Data Lake Storage Gen2 · Parquet
Orchestration   Databricks Workflows
Visualisation   Power BI
Format          Medallion Architecture (Bronze → Silver → Gold)
Schema          Kimball Star Schema
Standard        Sachin Standard (type hints · docstrings · error as UI)
```

---

## 📈 GitHub Activity

> *"Laptop travels everywhere. Streak never breaks."*

---

<div align="center">

```
                              ·  ·  ·  ✈  ·  ·  ·
                    
         Destination: Data Engineer | October 2026
         
         Altitude    : Climbing
         Speed       : Consistent  
         Fuel        : Domain Knowledge + Technical Depth
         ETA         : On Schedule
```

*Building in public. Domain first. Code second. Insights always.*

</div>
