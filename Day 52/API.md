# PaperMind AI - API Documentation

Version: 1.0

Author: Shagla Amri

Project: PaperMind AI

---

# Overview

PaperMind AI exposes a simple REST API that allows the frontend to:

- Upload a PDF
- Generate AI summaries
- Extract key insights
- Ask questions about the uploaded PDF

Base URL (Development)

```
http://localhost:8000
```

Production

```
https://your-render-app.onrender.com
```

---

# API Flow

```
Frontend (React)

↓

REST API

↓

FastAPI

↓

Gemini API

↓

JSON Response
```

---

# Authentication

Version 1.0 does not require authentication.

No login or API token is required from users.

The backend securely stores the Gemini API key using environment variables.

---

# Common Response Format

## Success Response

```json
{
    "success": true,
    "message": "Operation completed successfully",
    "data": {}
}
```

## Error Response

```json
{
    "success": false,
    "error": "Description of the error"
}
```

---

# 1. Upload PDF

## Endpoint

```
POST /upload
```

Purpose

Upload and process a PDF document.

---

Request

Content-Type

```
multipart/form-data
```

Parameter

| Name | Type | Required |
|------|------|----------|
| file | PDF | Yes |

---

Success Response

```json
{
    "success": true,
    "message": "PDF uploaded successfully",
    "pages": 12,
    "filename": "research.pdf"
}
```

---

Validation

- Only PDF files allowed
- Maximum size: 20 MB
- Empty files rejected
- Corrupted PDFs rejected

---

Possible Errors

400 Bad Request

```json
{
    "error": "Invalid PDF file"
}
```

413 Payload Too Large

```json
{
    "error": "File exceeds size limit"
}
```

500 Internal Server Error

```json
{
    "error": "Unable to process PDF"
}
```

---

# 2. Generate Summary

## Endpoint

```
POST /summary
```

Purpose

Generate AI summary for the uploaded PDF.

---

Request

No additional body required.

---

Success Response

```json
{
    "success": true,
    "data": {
        "short_summary": "...",
        "detailed_summary": "..."
    }
}
```

---

Possible Errors

404

```json
{
    "error": "No PDF uploaded"
}
```

500

```json
{
    "error": "Gemini API unavailable"
}
```

---

# 3. Extract Key Insights

## Endpoint

```
POST /insights
```

Purpose

Generate important bullet-point insights from the uploaded PDF.

---

Success Response

```json
{
    "success": true,
    "insights": [
        {
            "title": "Main Contribution",
            "description": "..."
        },
        {
            "title": "Methodology",
            "description": "..."
        },
        {
            "title": "Results",
            "description": "..."
        }
    ]
}
```

---

Possible Errors

404

```json
{
    "error": "Document not found"
}
```

500

```json
{
    "error": "Unable to generate insights"
}
```

---

# 4. Chat with PDF

## Endpoint

```
POST /chat
```

Purpose

Answer user questions using the uploaded PDF as context.

---

Request

```json
{
    "question": "What is the main objective of this paper?"
}
```

---

Success Response

```json
{
    "success": true,
    "answer": "The paper focuses on..."
}
```

---

Validation

- Question cannot be empty
- PDF must already be uploaded

---

Possible Errors

400

```json
{
    "error": "Question cannot be empty"
}
```

404

```json
{
    "error": "Please upload a PDF first"
}
```

500

```json
{
    "error": "Gemini API request failed"
}
```

---

# HTTP Status Codes

| Code | Meaning |
|------|----------|
| 200 | Success |
| 400 | Bad Request |
| 404 | Resource Not Found |
| 413 | Payload Too Large |
| 429 | Rate Limit Exceeded |
| 500 | Internal Server Error |

---

# API Sequence

```
Upload PDF

↓

Extract Text

↓

Store Session

↓

Generate Summary

↓

Generate Insights

↓

Ask Questions

↓

Return AI Response
```

---

# Future API (v2.0)

The following endpoints may be introduced in future versions:

```
POST /login

POST /register

GET /history

DELETE /document

POST /upload/multiple

GET /documents

POST /citations

POST /export-summary
```

These APIs are intentionally excluded from v1.0 to keep the project focused and achievable.

---

# API Summary

Framework:
FastAPI

Protocol:
REST

Authentication:
None (v1.0)

Data Format:
JSON

File Upload:
multipart/form-data

AI Provider:
Google Gemini 2.5 Flash

Persistence:
In-memory session
