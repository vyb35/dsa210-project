# DSA 210 Term Project: WhatsApp Conversational Dynamics & Activity Analysis

## Project Overview
This repository contains the dataset, exploratory data analysis (EDA), and hypothesis testing for the **DSA 210 (Introduction to Data Science)** term project at Sabancı University.

The project investigates personal communication behaviors, conversational tempo, reciprocity, and circadian rhythms using anonymized WhatsApp messaging data spanning August 2024 to November 2026.

---

## Dataset Structure
All datasets are located in the [`whatsapp-data/`](./whatsapp-data/) directory:

| File | Description |
|---|---|
| [`wa_messages.csv`](./whatsapp-data/wa_messages.csv) | Message-level feature matrix (43,474 messages) with character counts, emoji counts, response latency, session and turn identifiers. |
| [`wa_chat_summary.csv`](./whatsapp-data/wa_chat_summary.csv) | Chat-level summary metrics (114 chats) with participant counts, message share, and median response latency. |
| [`wa_daily.csv`](./whatsapp-data/wa_daily.csv) | Daily time series (842 days) tracking message volume, character volume, and late-night activity ratios. |
| [`wa_hourly.csv`](./whatsapp-data/wa_hourly.csv) | Hourly activity matrix (20,208 bins) for circadian and weekday/weekend patterns. |
| [`data_dictionary.md`](./whatsapp-data/data_dictionary.md) | Comprehensive data dictionary with descriptions, data types, and visual mappings for all features. |

---

## Privacy & Anonymization
All data in this repository has been strictly anonymized and preprocessed in accordance with privacy guidelines:
* **Zero raw text:** Message bodies have been transformed into numerical attributes (length, word count, emoji count) and removed.
* **No personally identifiable information (PII):** Participant names, contact numbers, and chat titles have been replaced with anonymous identifiers (`c001`, `u01`, `self`, `other`).
* **Zero leaks:** Scanned and verified for zero external identifiers, emails, phone numbers, or URLs.

---

## Research Questions & Hypotheses
1. **Conversational Tempo & Reciprocity:** Does response latency exhibit entrainment (faster responses elicit faster replies)?
2. **Group vs. 1-on-1 Dynamics:** How do response latencies, turn lengths, and initiative vary between one-on-one and group chats?
3. **Burstiness & Human Dynamics:** Do inter-message time intervals follow heavy-tailed power-law distributions characteristic of human communication?
4. **Circadian Rhythms:** How does late-night communication correlate with activity onset and communication volume across the semester?
