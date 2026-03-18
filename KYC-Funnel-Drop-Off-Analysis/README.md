# **KYC ONBOARDING: FUNNEL DROP-OFF ANALYSIS**

*End-to-end data science project · FinTech Product Analytics*

## Project Overview

**Know Your Customer (KYC)** is the process by which financial institutions verify the identity of their customers (that they are who they claim to be). In digital products, this involves collecting and validating information such as:
- name and date of birth
- phone number or email
- government-issued identification
- proof of address
- biometric verification such as selfies or face matching

KYC is therefore a core requirement in financial services because companies must comply with regulations designed to prevent fraud, identity theft, money laundering, terrorist financing and unauthorized account use. 

For a FinTech company, KYC is not just a compliance step. It is often the entry point to product activation. If a user fails to verify their identity, they cannot fully use the platform i.e. fund accounts, access credit, or generate revenue. A FinTech company can spend heavily to acquire users, but if those users fail during verification, acquisition efforts do not translate into active customers. Therefore, this makes KYC one of the most important operational and product journeys in the business.

KYC onboarding is a multi-step funnel, not a single event. A typical KYC flow includes:
- Identity Verification – Uploading government-issued IDs (passport, driver's license)
- Biometric Verification – Taking a selfie or recording a video for face matching
- Address Verification – Submitting utility bills or bank statements
- Phone/Email Verification – Confirming contact methods via OTP
- Risk Assessment – Background checks and fraud screening

Users move through stages such as:starting KYC, verifying phone or email, entering personal information, uploading documents, completing biometric checks, passing manual or automated review and getting approved. At each stage, some users succeed, some fail, and some abandon the process altogether. 

Without funnel drop-off analysis, teams may know that KYC completion is low, but they will not know why it is low or where to focus improvement efforts. This analysis is especially important in FinTech because even small inefficiencies in onboarding can lead to:
- lower activation rates
- wasted acquisition/marketing spend
- more manual review workload
- increased customer support volume
- reduced lifetime value


## Project Goal
Identify where users abandon the oboarding journey, why they leave, which users are most affected and provide data-backed recommendations to improve the **KYC Completion Rate**.
Key questions
1. Where does the biggest drop-off occur?
2. What causes failure or abandonment?
3. Which segments are most impacted?
4. What improvements should be prioritized?


<img width="639" height="130" alt="image" src="https://github.com/user-attachments/assets/abd09db9-06e3-48b2-a5d9-9a7ed2d60b76" />

## Respository Structure
```
KYC-Funnel-Drop-Off-Analysis/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   └── FinTech KYC Funnel Analysis.ipynb
│
├── outputs/
│   ├── figures/
│   └── reports/
│
├── src/
│   ├── config.py
│   ├── data_loader.py
│   ├── preprocessing.py
│   ├── feature_engineering.py
│   ├── eda.py
│   ├── funnel_analysis.py
│   ├── root_cause_analysis.py
│   ├── segmentation.py
│   ├── summary.py
│   └── recommendations.py
│
└── scripts/
    ├── run_pipeline.py
    ├── run_eda.py
    ├── run_funnel.py
    └── run_segmentation.py
```
## 📂 Data Schema

The analysis uses five core datasets:

| File | Description | Key Fields |
| --- | --- | --- |
| `fintech_users.csv` | User demographic and acquisition data. | `user_id`, `country`, `age`, `acquisition_source` |
| `fintech_devices.csv` | Hardware specifications for the user's primary device. | `user_id`, `os`, `device_model`, `camera_quality_score` |
| `network_logs.csv` | Telemetry regarding the user's connectivity during KYC. | `user_id`, `network_type`, `latency_ms`, `upload_speed_mbps` |
| `sessions.csv` | High-level session metadata. | `session_id`, `user_id`, `session_start`, `session_end` |
| `kyc_events.csv` | Granular event logs for every step of the KYC journey. | `session_id`, `event_name`, `status`, `error_code`, `timestamp` |

---

## The Funnel Stages

The analysis tracks users through the following stages:

1. `start_kyc` ➔ 2. `phone_verification` ➔ 3. `personal_information` ➔ 4. `document_upload` ➔ 5. `document_validation` ➔ 6. `selfie_capture` ➔ 7. `face_match` ➔ 8. `address_verification` ➔ 9. `manual_review` ➔ 10. `kyc_approved`.

<img width="1408" height="768" alt="image" src="https://github.com/user-attachments/assets/3f471b70-b789-42a7-bd7b-3c83890e3a0e" />


---

## Tech Stack

* **Language:** Python 3.10+
* **Analysis:** `Pandas`, `NumPy`
* **Visualization:** `Matplotlib`, `Seaborn`, `Plotly` (for interactive funnels)
* **Statistical Modeling:** `SciPy` or `Statsmodels` (for segment significance testing)

---

## Analysis Workflow

1. **Data Audit:** Check for referential integrity (e.g., do all `kyc_events` have a matching `user_id` in the users table?).
2. **Feature Engineering:** Calculate `retry_count`, `step_duration`, and bucket technical metrics like `latency` into high/medium/low.
3. **Funnel Visualization:** Identify the friction point (the step with the highest % drop-off).
4. **Root Cause Analysis (RCA):** Correlate hardware (camera quality) and network (upload speed) with failure events.
5. **Segmentation:** Compare completion rates across iOS vs. Android, and Organic vs. Paid acquisition.
6. **Strategic Recommendations:** Propose UX/Technical changes and design experiments (A/B tests).

---

## Success Metrics

* **Primary:** KYC Completion Rate (CR).
* **Secondary:** Average Steps to Approval, Retry Rate per Step, and Time-to-Verify (TTV).

---

Copyright (c) 2026 Mapenzi Supaki

Shield: [![CC BY-NC 4.0][cc-by-nc-shield]][cc-by-nc]

This work is licensed under a
[Creative Commons Attribution-NonCommercial 4.0 International License][cc-by-nc].

[![CC BY-NC 4.0][cc-by-nc-image]][cc-by-nc]

[cc-by-nc]: https://creativecommons.org/licenses/by-nc/4.0/
[cc-by-nc-image]: https://licensebuttons.net/l/by-nc/4.0/88x31.png
[cc-by-nc-shield]: https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg
