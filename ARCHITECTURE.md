# System Architecture

## Agents (MVP in Step 1)
- OCR Agent: Parse PDFs/images (or .txt) into raw text
- Extraction Agent: Convert raw text to strict JSON schema via Groq LLM
- Validation Agent: Check required fields and normalize formats
- Classification Agent: Route to department/type based on content
- Orchestrator: Coordinates the entire flow and logs timings

## Data Flow
```
Image/PDF/.txt
   ↓
[OCR Agent] → OcrOutput(text)
   ↓
[Extraction Agent] → ExtractedPatientData (JSON)
   ↓
[Validation Agent] → ValidationResult (missing fields, notes)
   ↓
[Classification Agent] → ClassificationResult (doc_type, department)
   ↓
[Orchestrator] → FinalProcessingResult (saved to data/extracted_data)
```

## Models (Groq)
- Extraction: mixtral-8x7b-32768 (fast) or llama-3.x depending on quality needs
- Orchestrator/logging: local Python orchestration

## Upcoming MCP Integrations (Step 2+)
- RxNav drug interactions (safety_agent)
- Insurance eligibility (mock REST)
- Hospital DB (SQLite persistence)
- Alerts (Slack/Twilio)
- Scheduler (mock or Google Calendar)