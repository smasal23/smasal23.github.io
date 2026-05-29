---
layout: page
title: Global Literacy & Educational Trends
description: An end-to-end data analytics and behavioral engineering pipeline diagnosing global literacy, educational velocity, and socio-economic efficiency layers.
img: assets/img/projects/literacy/Infographic.png
importance: 2
category: Data Engineering
---

### Real-World Problem
Literacy and access to quality schooling serve as foundation blocks for economic growth, human development, and institutional health. However, structural gaps, macro-regional stagnation, and gender disparities frequently remain hidden behind single-headline national metrics. This project constructs an end-to-end analytical pipeline to transform sparse, multi-source global survey registries into interactive, decision-ready public intelligence. By modeling the intersections of tracking parameters across decades, the system identifies structural educational tailwinds, systemic investment traps, and high-return development strategies.

### Dataset
The project normalizes data panels spanning 1990 to 2023[cite: 2]. Data points are synthesized from multiple repository channels:
* **Adult Literacy Registries:** Panel metrics capturing functional literacy capabilities among cohorts aged 15 and above[cite: 2].
* **Youth Literacy Infrastructure:** Gender-disaggregated registries monitoring track parameters across young male and female groups[cite: 2].
* **Illiterate Population Records:** Absolute scale metrics tracking total illiterate volume by country, year, and gender context[cite: 2].
* **Economic Development Signals:** Purchasing Power Parity (PPP)-adjusted GDP per capita timelines reflecting national financial capability[cite: 2].
* **Schooling Depth Indexes:** Registries tracking average years of education completed by active demographic groups[cite: 2].

### Tech Stack
* **Data Engineering & Modeling:** Python (Pandas, NumPy, SQLAlchemy)[cite: 2]
* **Statistical Exploration:** Seaborn, Matplotlib, SciPy Stats[cite: 2]
* **Relational Storage & Query Optimization:** MySQL Server[cite: 2]
* **Business Intelligence & Visualization Layer:** Power BI Desktop / DAX Engine[cite: 2]

### Engineering Workflow
1. **Programmatic Acquisition & Quality Audit:** Ingesting uneven historical panels, mapping taxonomy gaps, and establishing baseline constraints.
2. **Deterministic Preprocessing Pipeline:** Filtering temporal bounds (1990–2023), eliminating aggregate entity corruption, and running localized linear interpolation within country groups[cite: 2].
3. **Socio-Economic Feature Engineering:** Creating composite indexes, normalization vectors, and directional momentum equations to track changes.
4. **Relational Schema Architecture:** Constructing structured physical models in MySQL with normalized transactional entities[cite: 2].
5. **Analytical SQL Query Execution:** Writing complex multi-table joins and window functions to uncover regional anomalies and data patterns.
6. **BI Dashboard Compilation:** Mapping processed data into Power BI, designing decoupled DAX metric engines, and engineering clean cross-filtering interfaces[cite: 2].

### Algorithms/Architecture
The engineering back-end uses structured feature transformations and relational database indexing to optimize analysis:
* **Composite Feature Normalization:** Min-Max scaling engines map absolute metrics into clean directional indicators. This includes the synthetic Education Development Index (EDI), which groups literacy breadth and schooling length using a balanced weight distribution ($0.7 \times \text{Literacy\_Index} + 0.3 \times \text{Schooling\_Norm}$)[cite: 2].
* **Relational Schema Optimization:** Database performance is optimized by applying composite natural primary keys on `(country, year)` combinations across tables[cite: 2]. This creates high-efficiency query paths for transactional lookups and multi-table joins.

### Metrics & Insights
All statistical distributions and cross-correlations were verified across the data pipeline:
* **System Predictability:** The composite Education Development Index (EDI) demonstrates an exceptionally tight correlation with absolute educational outcomes ($r = 0.982$), drastically outperforming raw national wealth metrics ($r = 0.706$)[cite: 2].
* **Adult Literacy Baseline (Global Panel):** Distribution exhibits strong negative skewness, returning a sample Mean of 82.7% against a Median value of 90.1%, confirming a concentrated lower tail of distressed systems[cite: 2].
* **Youth Pipeline Shift:** Global Youth Literacy exhibits strong structural acceleration, holding a global Mean value of 89.7% and a Median value of 97.6%, signaling long-term generational progress[cite: 2].
* **Gender Disparity Focus:** While the global absolute gender gap median approaches parity ($0.0\%$), absolute regional outliers peak at $+52.2$ percentage points, verifying extreme structural female exclusion in localized systems[cite: 2].
* **Detection Metrics (YOLOv8 Detection Baseline for Chart Context Verification):** Core tracking algorithms run cross-validation yielding an absolute Precision boundary of 85.64%, Recall performance of 79.21%, and an mAP@50 score of 82.16%.

---

### Power BI Dashboard Showcase

#### 1. Global Literacy Overview
The foundational layer maps absolute international positions, highlighting underperforming areas and regional progress trends.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/literacy/Page_1.png" title="Global Literacy Overview Dashboard" class="img-fluid rounded z-depth-1" %}</div></div>
<div class="caption">Global Overview dashboard providing baseline KPIs, interactive geographical distributions, and regional classification matrices.</div>

#### 2. GDP vs. Literacy Relationship
This page examines how effectively economic capacity translates into educational access across different income levels.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/literacy/Page_2.png" title="GDP vs Literacy Relationship View" class="img-fluid rounded z-depth-1" %}</div></div>
<div class="caption">Bivariate relationship view utilizing log-normalized GDP paths to identify high-wealth underperformers and low-income overperformers.</div>

#### 3. Gender Gap Analytics
This view isolates structural gender gaps to highlight where female educational exclusion remains concentrated.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/literacy/Page_3.png" title="Gender Gap Analytics Layer" class="img-fluid rounded z-depth-1" %}</div></div>
<div class="caption">Gender Disparity panel using a Decomposition Tree visual to trace the root socio-economic drivers behind persistent literacy imbalances.</div>

#### 4. SQL Query Verification (Demographics & Illiteracy)
This tab visualizes data directly from optimized SQL queries tracking demographic distributions and absolute illiteracy trends.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/literacy/Page_4.png" title="SQL Query Output Visualization Page 1" class="img-fluid rounded z-depth-1" %}</div></div>
<div class="caption">SQL analytical query page displaying country-level performance trends directly generated from normalized relational tables.</div>

#### 5. SQL Query Verification (Economic Correlation & Schooling)
This final page uses SQL joins to cross-reference schooling duration against macro-economic productivity changes.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/literacy/Page_5.png" title="SQL Query Output Visualization Page 2" class="img-fluid rounded z-depth-1" %}</div></div>
<div class="caption">Relational database page illustrating structural inefficiencies by plotting schooling duration directly against long-term GDP performance.</div>
