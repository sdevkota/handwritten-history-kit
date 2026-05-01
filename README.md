# Handwritten History Kit

Human-in-the-loop repair queues for historical handwriting and damaged records.

> Version: 1.0.0 | License: MIT | Status: production-oriented v1 foundation

## Problem

Historical OCR fails hardest on rare scripts, local names, faded ink, and unfamiliar layouts, exactly where preservation value is highest.

## What this project solves

A confidence-aware transcription workflow that packages page metadata, OCR candidates, uncertainty spans, and reviewer decisions into reusable open data.

Handwritten History Kit ships as a small, dependency-free CLI and library. It validates a domain-specific JSON packet, emits actionable findings, and gives contributors a concrete surface for adding adapters, richer checks, schemas, and integrations.

## Who it is for

Archivists, libraries, historians, civic record digitization teams.

## Quick start

```bash
npm test
npm start -- sample
```

Analyze your own packet:

```bash
handwritten-history-kit ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | node src/cli.js
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

```js
const { analyze } = require("./src/index.js");

const report = analyze({
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
});
console.log(report.summary);
```

## v1 behavior

- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Suggests next actions and contributor extension points.
- Runs fully offline with no API keys and no network access.

## Contribution map

Good first contributions:

- Add IIIF adapters.
- Add Transkribus imports.
- Add name authority linking.
- Add multimodal model adapters.

Larger contributions:

- Add a JSON Schema and compatibility tests.
- Build import/export adapters for popular AI frameworks.
- Add real-world fixtures from public, non-sensitive examples.
- Improve scoring with transparent, documented heuristics.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.

## GitHub Pages

The marketing site lives in `site/index.html`. Enable GitHub Pages from the `site` folder or use the included Pages workflow after publishing.

## Security

This project does not process secrets by default. If you build adapters that touch production systems, keep least privilege, explicit consent, and auditable logs in the design.
