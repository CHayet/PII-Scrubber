# PII Scrubber

A Python-based Natural Language Processing (NLP) tool for detecting and redacting Personally Identifiable Information (PII) from free-text fields.

This tool is built on top of the open-source [`pii_codex`](https://github.com/EdyVision/pii-codex) library, with custom enhancements to improve detection performance on narrative text such as incident or event descriptions.

---

## 🔍 Overview

Organizations often collect open-ended textual data (e.g., incident reports, customer support notes, user feedback) that may contain PII such as names, addresses, national ID numbers, or other sensitive identifiers.

This tool enables automated redaction of PII to support safe data sharing, privacy compliance (e.g., GDPR, HIPAA), and downstream analytics—all while preserving valuable non-sensitive context.

---

## ✨ Features

- Automatically detects and redacts common types of PII from unstructured text
- Outputs sanitized text using `<REDACTED>` placeholders
- Built on a customizable, open-source PII detection framework (`pii_codex`)
- Lightweight and easy to integrate into ETL pipelines or analysis workflows

---

## 🧩 Tech Stack

- Python
- [`pii_codex`](https://github.com/EdyVision/pii-codex) – Pre-trained PII redaction library
- Custom enhancements for more accurate PII recognition in narrative formats

---

## 🛠️ Installation & Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/<your-username>/pii-scrubber.git
   cd pii-scrubber
   ```

2. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

3. **Install and customize `pii_codex`:**

   - Follow the installation instructions on [`pii_codex`](https://github.com/EdyVision/pii-codex)
   - After installation, replace the following two files in your Python environment with the versions provided in the `custom_pii_codex` folder. These custom files are configured to prevent redaction of date information, which is often critical in safety-related incident descriptions. By preserving dates, the tool ensures that temporal context—essential for analysis and reporting—is retained while still protecting personally identifiable information.
     - `pii_type_mappings.csv`
     - `microsoft_presidio_pii.py`

   ### Example file paths:
   Replace accordingly in your environment:

   ```text
   <env_path>/site-packages/pii_codex/data/v1/pii_type_mappings.csv
   <env_path>/site-packages/pii_codex/models/microsoft_presidio_pii.py
   ```

---

## 🧪 Input/Output Example

**Original Text:**
```
Upon arrival, Officer Thomas and I contacted the victim, a male Hispanic, later identified as David Khols by his national ID. Donald said the suspect was wearing a red hoodie.
```

**Scrubbed Text:**
```
Upon arrival, Officer <REDACTED> and I contacted the victim, a male <REDACTED>, later identified as <REDACTED> by his national ID. <REDACTED> said the suspect was wearing a red hoodie.
```

---

## ▶️ Usage

Run the main script with your own input file:

```bash
python scrubber.py --input data/input_file.txt --output data/cleaned_output.txt
```

Sample code is provided in `scrubber.py` for processing text files line-by-line using the customized PII detection pipeline.

---

## 📁 Project Structure

```
pii-scrubber/
├── custom_pii_codex/           # Modified files for pii_codex
│   ├── pii_type_mappings.csv
│   └── microsoft_presidio_pii.py
├── data/                       # Folder for input/output text files
│   ├── input_file.txt
│   └── cleaned_output.txt
├── scrubber.py                 # Main PII redaction script
├── requirements.txt            # Python dependencies
└── README.md
```

---

## ⚠️ Disclaimer

This repository does **not** contain any real or internal data. All input/output examples are synthetically generated for demonstration purposes only. When using this tool with real-world data, ensure your use complies with relevant privacy laws and organizational policies.

---

## 🙌 Acknowledgments

- [pii_codex](https://github.com/EdyVision/pii-codex) for the foundational PII detection framework
