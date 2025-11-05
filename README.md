# CareFlow Intake & Safety Copilot (Medical Document Processor)

## Executive Summary
A multi-agent system to automate medical intake: extract patient data from forms/cards (vision), validate and classify, and prepare it for safety checks and scheduling. Built on Groq for real-time performance with optional MCP integrations for RxNav, insurance eligibility, scheduling, and notifications.

## Quick Start
1) Install system dependencies:
- Tesseract OCR (for images; PDFs and .txt can also be parsed without OCR)
- Python 3.10+

2) Install Python deps:
```bash
python -m venv venv
source venv/bin/activate           # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3) Configure environment:
```bash
cp .env.example .env
# Edit .env and set GROQ_API_KEY=your_key_here
```

4) Run the demo:
```bash
python demo.py
```

This will:
- Process sample docs in data/sample_documents
- Run OCR/text ingestion → LLM extraction → validation → classification
- Save structured JSON to data/extracted_data
- Print timings to console

## Roadmap
- Step 1 (this commit): OCR → Extraction → Validation → Classification → JSON output
- Step 2: MCP integrations
  - Drug safety checks (RxNav)
  - Insurance eligibility (mock)
  - Hospital DB (SQLite)
  - Alerts (Slack/SMS)
- Step 3: Scheduling + notifications + benchmarks and final demo video

## Notes
- Use only synthetic or de-identified documents
- Speed is a focus: we log per-agent and total latencies
- Everything is modular so you can swap agents or integrations