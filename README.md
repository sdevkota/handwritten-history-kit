# Handwritten History Kit

Human-in-the-loop repair queues for historical handwriting and damaged records.

> Version: 2.0.0 | Runtime: Python | License: MIT | Status: production-oriented v2 foundation

## Problem

Historical OCR fails hardest on rare scripts, local names, faded ink, and unfamiliar layouts, exactly where preservation value is highest.

## What this project solves

A confidence-aware transcription workflow that packages page metadata, OCR candidates, uncertainty spans, and reviewer decisions into reusable open data.

Handwritten History Kit is now Python-first. It ships as a dependency-free Python package and CLI that validates a domain-specific JSON packet, emits actionable findings, and gives contributors a practical foundation for adapters, datasets, evals, and workflow integrations.

## Quick start

```bash
python3 -m unittest discover -s tests
python3 -m handwritten_history_kit.cli sample
```

Analyze your own packet:

```bash
python3 -m handwritten_history_kit.cli ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | python3 -m handwritten_history_kit.cli
```

## Example packet

```json
{
  "page": {
    "id": "ledger-1842-p7",
    "language": "en",
    "condition": "faded"
  },
  "ocr": {
    "text": "Jon Smyth paid 4 shillings",
    "confidence": 0.62
  },
  "review": {
    "required": true,
    "uncertainSpans": [
      "Jon Smyth",
      "4 shillings"
    ]
  }
}
```

## Library usage

```python
from handwritten_history_kit import analyze

report = analyze({
  "page": {
    "id": "ledger-1842-p7",
    "language": "en",
    "condition": "faded"
  },
  "ocr": {
    "text": "Jon Smyth paid 4 shillings",
    "confidence": 0.62
  },
  "review": {
    "required": True,
    "uncertainSpans": [
      "Jon Smyth",
      "4 shillings"
    ]
  }
})
print(report["summary"])
```

## v2 behavior

- Python-first CLI and importable library.
- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Runs fully offline with no API keys and no network access.

## Contribution map

- Add IIIF adapters.
- Add Transkribus imports.
- Add name authority linking.
- Add multimodal model adapters.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.
