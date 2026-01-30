# FAERS Pharmacovigilance System
**Large-Scale Drug Safety Analysis using Unsupervised Learning**

## Overview
This project builds an end-to-end pharmacovigilance system using the **FDA Adverse Event Reporting System (FAERS)** to identify drug–adverse event associations and patient risk patterns at scale.  
It applies unsupervised machine learning techniques to millions of real-world safety reports to surface early drug safety signals and vulnerable patient populations.

---

## Key Highlights
- **Data Scale:** 2.85M+ adverse event reports across 7 quarters (2024 Q1 – 2025 Q3)
- **Pattern Mining:** 1,900 clinically meaningful drug–reaction association rules
- **Risk Stratification:** 8 patient clusters (Silhouette score: **0.47**)
- **Efficiency:** 70% dimensionality reduction while preserving **99.4%** signal fidelity
- **Early Detection:** Safety signals identified **2–3 quarters before** FDA alerts

---

## Dataset
- **Source:** FDA Adverse Event Reporting System (FAERS)
- **Raw Size:** ~15 GB (quarterly ASCII releases)
- **Processed Size:** ~619 MB (model-ready dataset)
- **Tables Used:** DEMO, DRUG, REAC, OUTC, INDI

> Due to size constraints, raw FAERS datasets are not stored in this repository.

---

## Repository Contents
- `notebooks_01_quarter_preprocessing.ipynb`  
  FAERS quarterly ingestion, cleaning, and dataset merging
- `notebooks_02_final_dataset_preprocessing.ipynb`  
  Feature engineering and transformation into a model-ready dataset
- `notebooks_03_models_output.ipynb`  
  Association rule mining, clustering, and dimensionality reduction
- `results_association_rules_output.csv`  
  Output of discovered drug–reaction association rules
- `Report.pdf`  
  Detailed technical report (adapted from an academic project and shared for portfolio purposes)
- `requirements.txt`  
  Python dependencies

---

## Methodology

### 1. Data Engineering
- Integrated 7 FAERS quarterly releases into a unified dataset
- Removed duplicate records and extreme outliers (age > 120)
- Engineered clinical features such as:
  - polypharmacy category
  - reaction severity
  - serious outcome indicators

**Final Dataset:**  
`2,847,862 cases × 19 features`

---

### 2. Association Rule Mining
- Algorithm: **FP-Growth**
- Metrics: Support, Confidence, Lift
- Filters applied to retain clinically relevant patterns

**Example Rule**
- *Methotrexate → Pneumonia*  
  Confidence: 0.72 | Lift: 8.4

---

### 3. Patient Risk Clustering
- Algorithm: **K-Means**
- Optimal clusters: **8**
- Silhouette score: **0.4698**

**Notable Clusters**
- Elderly high-mortality group (18.4% death rate)
- Pediatric vaccine-related reactions
- Oncology patients with severe outcomes

---

### 4. Dimensionality Reduction
- Reduced 10,000+ sparse features to 48 core signals
- Preserved statistical structure:
  - Drug frequency correlation: **0.9994**
  - Reaction frequency correlation: **0.9969**

---

## Validation
- **Stability Testing:** Independent 100K samples with consistent rule discovery
- **External Evidence:**
  - 62% of top rules aligned with FDA MedWatch
  - 31/50 top rules supported by published literature
- **Robustness:** Patterns remained stable despite minimal sample overlap

---

## Impact
- Identified **226K+** serious adverse reaction cases
- Flagged **670K+** elderly patients at elevated risk
- Highlighted dangerous drug combinations for proactive safety monitoring

---

## Tools & Technologies
- Python, Pandas, NumPy
- Scikit-learn, mlxtend
- Matplotlib, Seaborn
- Jupyter Notebook
  
---

## Future Work
- Real-time FAERS monitoring using streaming pipelines
- Temporal modeling with LSTM-based architectures
- Causal inference to distinguish correlation from causation

---

## Disclaimer
This project is for research and educational purposes only.  
Findings do not constitute medical advice and should be validated by healthcare professionals.
