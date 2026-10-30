# CodeCelix  – Classification Module

## 1. Project Overview

The CodeCelix Lead Finder Classification Module is a Python-based component designed to classify business leads using deterministic, rule-based logic.

It identifies WhatsApp availability, WhatsApp automation, website chatbot providers, and potential hot leads based on predefined technical rules.

## 2. Features

- UAE phone number validation and normalization.
- International phone number formatting using E.164.
- WhatsApp classification: `CONFIRMED`, `PROBABLE`, and `INSUFFICIENT`.
- WhatsApp type detection: `MANUAL`, `AUTOMATED`, and `UNKNOWN`.
- Detection of six approved WhatsApp automation providers.
- Website chatbot detection across 11 recognized vendors.
- Chatbot classification: `YES`, `NO`, and `UNKNOWN`.
- Hot lead evaluation based on WhatsApp type and chatbot status.
- Evidence and UTC observation timestamp in the classification response.
- Automated testing using pytest.

## 3. Technologies Used

- Python 3
- phonenumbers
- pytest

## 4. Project Structure

```text
CodeCelix_classification/
│
├── app/
│   ├── __init__.py
│   └── domain/
│       ├── __init__.py
│       │
│       ├── classification/
│       │   ├── __init__.py
│       │   ├── phone_normalizer.py
│       │   ├── whatsapp_classifier.py
│       │   ├── chatbot_classifier.py
│       │   ├── hot_lead_evaluator.py
│       │   └── lead_classifier.py
│       │
│       └── tests/
│           └── test_classification.py
│
├── requirements.txt
└── README.md
```

## 5. Module Description

| Module | Responsibility |
|---|---|
| `phone_normalizer.py` | Validates phone numbers and converts valid numbers into E.164 format. |
| `whatsapp_classifier.py` | Detects WhatsApp evidence and identifies automation signals. |
| `chatbot_classifier.py` | Detects recognized chatbot vendors from website HTML content. |
| `hot_lead_evaluator.py` | Determines whether a lead meets the hot-lead criteria. |
| `lead_classifier.py` | Combines the classification modules into one structured response. |

## 6. Classification Rules

### WhatsApp Classification

- `CONFIRMED`: A recognized WhatsApp link or WhatsApp keyword near a verified phone number is detected.
- `PROBABLE`: A valid mobile number is available without explicit WhatsApp evidence.
- `INSUFFICIENT`: The phone number is invalid, unparseable, or an unsupported number type.

### WhatsApp Type

- `MANUAL`: Confirmed WhatsApp evidence without an approved automation signal.
- `AUTOMATED`: An approved WhatsApp automation provider or the `START_BOT` parameter is detected.
- `UNKNOWN`: The available evidence is insufficient to determine the type.

### Chatbot Classification

- `YES`: A recognized chatbot vendor signature is detected.
- `NO`: Website inspection is complete, but no recognized chatbot signature is found.
- `UNKNOWN`: Website inspection is incomplete or unsuccessful.

### Hot Lead Criteria

A lead is classified as HOT only when both conditions are satisfied:

1. WhatsApp type is `MANUAL`.
2. Chatbot status is `NO`.

## 7. Supported WhatsApp Automation Providers

- WATI
- Interakt
- AiSensy
- Gallabox
- Respond.io
- Botmaker

## 8. Supported Chatbot Vendors

1. Intercom
2. Tidio
3. Zendesk
4. Drift
5. Crisp
6. LiveChat
7. Tawk.to
8. Freshchat
9. HubSpot Chat
10. ManyChat
11. JivoChat

## 9. Installation

Clone or download the project and open its root directory in the terminal.

Install the required dependencies:

```bash
python -m pip install -r requirements.txt
```

## 10. Running Tests

Run the following command from the project root:

```bash
python -m pytest -v
```

The current test suite contains **23 passing tests** covering phone validation, WhatsApp classification, automation detection, chatbot detection, inspection failures, and hot-lead evaluation.

## 11. Integration

The main entry point is `classify_lead()` in `lead_classifier.py`.

It accepts:
- Phone number
- WhatsApp evidence
- Website HTML content
- Website inspection status
- Source URL

It returns a structured classification result containing WhatsApp information, chatbot information, evidence metadata, and the hot-lead decision.

## 12. Scope and Limitations

This module implements classification logic only.

The following operations are handled separately by other backend components:

- Website fetching and live inspection
- Database operations
- API endpoints
- Frontend integration

The classification functions use the evidence supplied to them and do not independently access websites.

---

**Project:** CodeCelix Lead Finder  
**Component:** Backend Classification Logic  
**Developer:** Ayesha  
**Testing Framework:** pytest