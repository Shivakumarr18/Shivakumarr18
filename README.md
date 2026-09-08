<div align="center">

![Aviation](https://images.unsplash.com/photo-1436491865332-7a61a109cc05?w=1200&q=80)

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
          ✈  climbing to cruise          Role ............. Associate Engineer → Data Engineer
        /                                Company .......... CAMP Systems (Aviation MRO Software)
       /   BTS Aviation Delay            Experience ....... 3.5 years
      /    Intelligence System           Target ........... Data Engineering | October 2026
     /     18M+ rows · 2023-2025
    /                                    Languages ........ Python · SQL · PySpark
                                         Cloud ............ Azure Databricks · ADLS Gen2
                                         Pipeline ......... Bronze → Silver → Gold (Medallion)
                                         Schema ........... Kimball Star Schema
                                         Domain ........... Aviation Operations (IOC/OCC)
                                         Visualisation .... Power BI

                                         GitHub ........... Shivakumarr18
                                         Standard ......... Sachin Standard 🏏
                                         Streak ........... Never breaks. Laptop travels everywhere.
```

---

## 🏗️ BTS Aviation Delay Intelligence System

> *"Every row in aviation operational data is a record of a human decision made under pressure."*

```
  BTS TranStats (2023-2025)
  ~570K rows/month · 43 columns
           │
           ▼
    ┌─────────────┐
    │   BRONZE    │  Raw ingestion. Immutable. Append-only. Nulls preserved.
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │   SILVER    │  Cleaned. Validated. Null rules enforced.
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │    GOLD     │  Kimball Star Schema. fact_delays + 5 dimensions. Power BI ready.
    └─────────────┘
```

---

## 📊 The 5 Delay Columns — Domain Decoded

| Column | What Generated It |
|--------|------------------|
| `CARRIER_DELAY` | MEL faults · crew duty breaches · aircraft swaps · GPU failures |
| `WEATHER_DELAY` | Fog · crosswinds · thunderstorms · snow · Safety pillar override |
| `NAS_DELAY` | ATC ground stops · GDPs · runway closures · airspace restrictions |
| `SECURITY_DELAY` | Terminal evacuations · re-screening · overflight clearances |
| `LATE_AIRCRAFT_DELAY` | Propagation signal. Previous rotation was late. Schedule too tight. |
| `NULL (84% of rows)` | ← **SUCCESS.** IOC recovered on time. Not missing data. |

---

## 🧠 Domain Foundation

```
Before writing a single line of code:

  📖 Peter J. Bruce — Airline Operations Control

     Ch 1 → What the IOC is. Three pillars: Safety > Legality > Efficiency.
     Ch 3 → How the schedule is built. Slots. Curfews. Schedule robustness.
     Ch 4 → What happens when the plan breaks. IROPS. Every column decoded.
```

---

## 🏆 Architecture Decision Records

| ADR | Decision | Rationale |
|-----|----------|-----------|
| ADR-GOLD-001 | SCD Type 1 for dimensions | Operational simplicity. Current state is what matters. |
| ADR-GOLD-002 | Delay reason as separate dimension | CARRIER_DELAY is composite. Not atomic. Cannot be treated as one. |
| ADR-GOLD-003 | Surrogate keys over natural keys | Isolation from source system changes. Kimball standard. |
| ADR-GOLD-004 | Cost model separated from fact table | Assumptions must be explicit and auditable. |
| ADR-GOLD-005 | Aircraft dimension included | TAIL_NUM enables cascade chain analysis across rotations. |
| ADR-GOLD-006 | ARR_DELAY nulls for cancellations preserved | Cancelled flights have no arrival. NULL is correct. Never fill with 0. |

---

<div align="center">

```
  Destination : Data Engineer | October 2026
  Altitude    : Climbing
  Fuel        : Domain Knowledge + Technical Depth
  ETA         : On Schedule
```

*Building in public. Domain first. Code second. Insights always.*

</div>
