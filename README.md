# Cardiovascular Clinical Decision Support Agent

## Overview

The **Cardiovascular Clinical Decision Support (CDS) Agent** is an AI-powered assistant designed for healthcare providers to support cardiovascular disease (CVD) risk assessment and evidence-based decision support.

This system integrates:

* Machine Learning–based CVD risk prediction
* Clinical practice guidelines (e.g., ACC/AHA)
* Peer‑reviewed biomedical research (PubMed abstracts)

The agent does **not diagnose or prescribe treatment**. It provides structured, citation-backed risk assessments and actionable recommendations to support clinical decision-making.

---

# System Architecture

The agent operates using a structured, tool-driven workflow:

1. **ML Risk Prediction Layer**

   * Calls `cvd_risk_predictor`
   * Outputs:

     * Risk percentage
     * Risk category (LOW / MODERATE / HIGH)
     * Top contributing features

2. **Clinical Guidelines Retrieval Layer**

   * Calls `search_clinical_guidelines`
   * Retrieves relevant guideline recommendations
   * Prioritizes Class I recommendations

3. **Research Evidence Layer**

   * Calls `search_pubmed_abstracts`
   * Retrieves supporting biomedical literature
   * Extracts key evidence statements with PMID citations

4. **Synthesis Engine**

   * Combines ML output + guidelines + research
   * Generates structured, citation-backed assessment

---

# Input Schema

The agent expects structured patient data including:

* Gender
* Height
* Weight
* Blood pressure (systolic/diastolic)
* Cholesterol
* Glucose
* Smoking status
* Alcohol consumption
* Physical activity

### Derived Calculations

* BMI is automatically calculated from height and weight
* Blood pressure staging uses standard thresholds:

  * Stage 1 Hypertension: 130–139 / 80–89
  * Stage 2 Hypertension: ≥140 / ≥90
  * Hypertensive Crisis: ≥180 / ≥120 (flag urgent)

---

# Workflow

When given patient data, the agent performs the following steps:

### Step 1 – Risk Prediction

Calls `cvd_risk_predictor` to:

* Compute cardiovascular risk score
* Identify top contributing risk factors

### Step 2 – Guideline Retrieval

Calls `search_clinical_guidelines` to:

* Retrieve recommendations specific to identified risk factors
* Extract recommendation class and level of evidence

### Step 3 – Research Evidence Retrieval

Calls `search_pubmed_abstracts` to:

* Identify supporting peer‑reviewed studies
* Extract summary findings
* Attach PMID citations

### Step 4 – Structured Synthesis

Generates a comprehensive, structured clinical summary including:

* Risk categorization
* Primary contributing factors
* Evidence-based recommendations
* Immediate clinical actions
* Evidence quality assessment

---

# Output Format

All responses follow a standardized structure:

## RISK SUMMARY

* Overall risk percentage
* Risk category (LOW / MODERATE / HIGH)

## PRIMARY RISK FACTORS

Top 3–5 contributors with:

* Clinical interpretation
* Relative importance

## EVIDENCE-BASED RECOMMENDATIONS

For each risk factor:

* Specific intervention
* Target/goal value
* Guideline citation (Class & Level)
* Supporting research citation (PMID)

## IMMEDIATE ACTIONS

Checklist including:

* Required labs
* Medication considerations
* Lifestyle interventions
* Referral recommendations
* Follow-up timeline

## EVIDENCE QUALITY

* Strength of evidence
* Conflicting data (if any)
* Acknowledgment of uncertainty
* Data limitations

---

# Safety & Clinical Guardrails

The agent enforces the following rules:

* Always includes citations (PMID or guideline class/level)
* Never provides a diagnosis
* Never prescribes treatment
* Flags urgent conditions:

  * BP ≥180/120
  * Risk >90%
* Acknowledges incomplete data
* Prioritizes Class I guideline recommendations
* Keeps responses concise (400–600 words)

---

# Design Principles

### 1. Evidence Transparency

Every recommendation must include a citation.

### 2. Interpretability

Top ML contributing factors are explicitly reported.

### 3. Clinical Alignment

Recommendations align with established cardiovascular guidelines.

### 4. Modularity

Each tool (risk model, guideline search, research retrieval) operates independently and can be upgraded without affecting the overall system.

### 5. Extensibility

Future enhancements may include:

* EHR integration
* Longitudinal patient tracking
* Explainable AI visualizations
* Medication optimization modules
* Multi-modal ECG integration

---

# Limitations

* Risk models depend on training dataset quality
* Guideline interpretation may evolve over time
* Literature retrieval may not capture all recent studies
* Does not replace physician judgment

---

# Intended Use

This system is designed for:

* Clinical decision support
* Educational purposes
* Research demonstrations
* Hackathon and innovation projects

It is **not intended for autonomous medical decision-making**.

---

# Value Proposition

This agent delivers:

* Fast cardiovascular risk stratification
* Evidence-backed recommendations
* Transparent reasoning with citations
* Structured clinical output

The combination of ML prediction + guideline alignment + literature support ensures both computational rigor and clinical relevance.

---

# License

For research and educational use only.
