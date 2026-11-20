# MedLens — Comprehensive Lab Result & Health Trend Analyzer

MedLens is a Python command-line diagnostic translation and health-tracking application designed to make routine hospital laboratory results easier to understand and monitor over time. Routine lab printouts—such as Complete Blood Count (CBC), Urinalysis, Blood Chemistry panels, and Vital Signs—often rely on medical abbreviations and raw numbers without context. MedLens translates those readings into clear, everyday language, organizes multi-visit records using persistent JSON data, highlights potential cross-metric patterns, tracks trends across checkups, and prepares summaries for doctor consultations.

> **Medical Disclaimer:** MedLens is an educational and health-monitoring tool intended to support understanding and record organization. It does not provide medical diagnoses or replace professional medical advice, diagnosis, or treatment.

---

## What MedLens Does

* **Multi-Panel Lab Record Management:** Supports creating, viewing, updating, and deleting patient profiles and multi-visit laboratory records across CBC, Blood Chemistry, Urinalysis, and Vital Signs, including partial panels and chronological history.
* **Age- and Sex-Adjusted Plain-Language Explanations:** Compares biomarker readings against age- and sex-specific clinical reference ranges and explains what each test measures, what elevated or low values may suggest, and common non-alarming factors such as dehydration.
* **Cross-Metric Pattern Detection (Smart Insights):** Evaluates combinations of results across panels—such as potential dehydration or infection/inflammation indicators—to provide educational context beyond single numbers in isolation.
* **Longitudinal Trends & Descriptive Statistics:** Tracks changes across multiple visits by calculating metrics like minimum, maximum, mean, standard deviation, range, and percentage change, alongside text-based trend charts.
* **Doctor Consultation Summary Export:** Compiles patient details, flagged results, observed trends, and suggested questions into a readable `.txt` summary for follow-up appointments.
* **Input Validation & Safety Guardrails:** Checks data types and realistic physiological bounds to catch entry mistakes early, paired with confirmation prompts before deleting records.

---

## Who It's For

MedLens is built primarily for patients, families, and caregivers tracking routine or recurring lab tests, as well as individuals monitoring long-term health indicators and organizing notes for medical consultations.

---

## Proposal & Documentation

Full project details, objectives, data fields, logic plan, and wireframes are available in [`docs/Proposal.md`](docs/Proposal.md).

---

## Team

Sosobrado, Dagani, Ballesteros
