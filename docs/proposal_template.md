# 📌 Project Proposal (Draft)

## 📝 Project Title  
**MedLens — Comprehensive Lab Result & Health Trend Analyzer**  

---

## 🔍 Problem Statement  
- **Issue / Need Identified:** When patients receive routine hospital laboratory results—such as a Complete Blood Count (CBC), Urinalysis, Blood Chemistry panel, or Vital Signs—the printouts are filled with medical abbreviations (e.g., WBC, Hgb, RBC, SGPT, LDL) and raw numerical values without context. Because of this, patients and caregivers often feel anxious or confused, unsure which values require urgent medical attention, which are minor fluctuations, or how their current results compare to previous checkups.
- **Why This Problem Is Relevant and Worth Solving:** Making diagnostic results accessible empowers patients, families, and individuals with chronic conditions to understand their health status, track long-term biomarkers (such as blood glucose, cholesterol, and kidney function), and communicate more effectively with physicians during follow-up visits.
- **Relation to the Selected Dataset:** MedLens directly addresses this challenge using structured medical JSON datasets (`data/patients.json` and `data/reference_ranges.json`). By storing longitudinal patient lab records alongside age- and sex-adjusted clinical reference thresholds, the application acts as a personal medical translator that organizes multi-visit records, explains biomarkers in plain English, detects cross-metric health patterns, and prepares structured consultation summaries.

---

## 🎯 Project Objectives  
- **Objective 1:** To store, manage, and analyze multi-visit hospital laboratory records and clinical reference ranges using structured JSON datasets (`patients.json` and `reference_ranges.json`).
- **Objective 2:** To help patients and caregivers gain meaningful health insights by translating medical abbreviations into plain language, flagging age- and sex-adjusted abnormalities, detecting cross-metric patterns, and generating longitudinal descriptive statistics and ASCII trend charts.
- **Objective 3:** To practice modular Python programming, JSON file handling (CRUD operations), conditional pattern detection, iterative statistical analysis, and strict input validation.

---

## ⚙️ Planned Features  
- **Feature 1: Multi-Panel Lab Record Management (Full CRUD):** Allows users to Create, Read, Update, and Delete patient profiles and multi-visit laboratory records categorized into CBC, Blood Chemistry, Urinalysis, and Vital Signs in `patients.json`. Users can log partial or complete lab panels, browse a chronological visit timeline, update profile details (such as age and weight), add late-arriving test results, and safely delete duplicate records using confirmation prompts.
- **Feature 2: Age- and Sex-Adjusted Plain-Language Translator:** Uses modular Python functions to evaluate individual biomarkers against age- and sex-specific clinical limits in `reference_ranges.json`. Translates medical abbreviations and numerical readings into clear everyday language, explaining what each test measures, what elevated or decreased levels indicate, and common non-alarming factors (such as dehydration).
- **Feature 3: Cross-Metric Pattern Detector (Smart Insights):** Applies conditional logic and arrays to evaluate combinations of biomarkers across panels rather than checking metrics in isolation—such as flagging a *Possible Dehydration* pattern (elevated urine specific gravity paired with slightly elevated hemoglobin) or an *Infection/Inflammation Indicator* (elevated WBC count)—storing generated flags in `flagged_insights` as educational insights.
- **Feature 4: Longitudinal Trend Analysis and Descriptive Statistics:** Uses iterative loops to analyze historical checkup records for a patient, computing minimum, maximum, mean (average), standard deviation, range, and percentage change from the prior visit, while rendering chronological ASCII trend charts for key markers like fasting glucose and total cholesterol.
- **Feature 5: Doctor Consultation Preparation and Exportable Summary:** Compiles patient demographics, flagged abnormal results, longitudinal trends, and suggested physician questions into a clean, printable `.txt` consultation checklist saved in the `/outputs` directory.
- **Feature 6: Strict Input Validation and Educational Medical Disclaimer:** Enforces data-type and realistic physiological range checks (preventing typos like entering `140` instead of `14.0` g/dL for hemoglobin) and displays an educational disclaimer clarifying that MedLens supports health monitoring and does not replace professional medical diagnosis.

---

## ⌨️ Planned Inputs and Outputs  

- **Inputs**  
  - **Patient Profile Details:** Patient ID, full name, age (in years), biological sex (`M`/`F`), and weight (`kg`).
  - **Laboratory Visit Metadata:** Visit ID, date tested (`YYYY-MM-DD`), and optional clinic notes (e.g., fasting status or follow-up reason).
  - **Biomarker Measurements (by Panel):**
    - *CBC:* Hemoglobin (`g/dL`), WBC Count (`10^9/L`), Platelet Count (`10^9/L`).
    - *Blood Chemistry:* Fasting Glucose (`mg/dL`), Total Cholesterol (`mg/dL`), Creatinine (`mg/dL`).
    - *Urinalysis:* Urine pH, Specific Gravity.
    - *Vital Signs:* Systolic Blood Pressure (`mmHg`), Diastolic Blood Pressure (`mmHg`).
  - **Navigation & Action Choices:** Menu selections (`1–6`), target patient/visit IDs for updates or deletion, biomarker selection for trend tracking, and deletion confirmations.

- **Outputs**  
  - **Plain-Language Diagnostic Translation Report:** A structured console table displaying each recorded biomarker, measured value, age/sex-adjusted normal range, status flag (Normal, Low, High), and plain-English explanation.
  - **Cross-Metric Smart Insights:** Educational alerts highlighting combined biomarker patterns (e.g., possible dehydration or inflammation indicators).
  - **Longitudinal Statistics & ASCII Trend Graphs:** Summary metrics (min, max, mean, standard deviation, range, and visit-over-visit percentage change) paired with a text-based chronological trend chart.
  - **Exportable Doctor Consultation Sheet (`.txt`):** A formatted text report saved inside `/outputs` containing patient summary details, abnormal values, observed trends, and tailored questions to ask a doctor.

---

## 🧠 Logic Plan  

### Pseudocode  
```text
START MedLens
DISPLAY educational medical disclaimer
LOAD "data/patients.json" and "data/reference_ranges.json"

PROMPT user to select an existing patient profile OR create a new patient profile
SET active_patient

LOOP until user chooses Exit:
    DISPLAY active patient header (Name, Age/Sex, Total Visits) and Main Menu:
        [1] Log New Laboratory Results (Create)
        [2] View Plain-Language Lab Report & Smart Insights (Read)
        [3] Track Longitudinal Trends & Statistics
        [4] Export Doctor Consultation Sheet (.txt)
        [5] Edit or Delete Patient / Visit Records (Update / Delete)
        [6] Exit Program

    PROMPT user for menu choice (1–6) and VALIDATE input

    IF choice == "1":
        PROMPT for visit date (YYYY-MM-DD) and optional clinic notes
        PROMPT for biomarker values across CBC, Blood Chemistry, Urinalysis, and Vitals
        VALIDATE data types and physiological bounds against reference ranges
        EVALUATE biomarkers against age- and sex-specific ranges
        RUN cross-metric conditional rules to generate flagged_insights
        APPEND visit record to active_patient in "data/patients.json"

    ELSE IF choice == "2":
        PROMPT user to select a recorded visit
        DISPLAY structured biomarker table with status flags and plain-language explanations
        DISPLAY any cross-metric Smart Insights for that visit

    ELSE IF choice == "3":
        PROMPT user to choose a biomarker (e.g., Hemoglobin, Fasting Glucose, WBC)
        RETRIEVE all historical values and dates for active_patient
        COMPUTE min, max, mean, standard deviation, range, and percentage change
        RENDER chronological ASCII trend chart in console

    ELSE IF choice == "4":
        COMPILE active_patient info, flagged abnormal results, trends, and doctor questions
        WRITE formatted summary to "/outputs/<patient_id>_consultation_sheet.txt"
        DISPLAY confirmation and file path

    ELSE IF choice == "5":
        PROMPT user to update profile/visit data OR delete a record with confirmation
        SAVE updated records to "data/patients.json"

    ELSE IF choice == "6":
        SAVE all pending changes to "data/patients.json"
        BREAK loop
END LOOP

DISPLAY closing message
END MedLens
