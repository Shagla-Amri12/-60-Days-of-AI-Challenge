# PaperMind AI - Session Schema

Version: 1.0

Author: Shagla Amri

Project: PaperMind AI

---

# Overview

PaperMind AI v1.0 does not use a database.

The application stores all information in memory during the user's session.

When the backend stops or restarts, all session data is cleared.

This approach keeps the architecture simple and aligns with the project's 10-day implementation scope.

---

# Session Object

The backend maintains one active session.

```python
Session = {
    "document": {...},
    "summary": {...},
    "insights": [...],
    "chat_history": [...]
}
```

---

# Document Model

Stores information about the uploaded PDF.

```python
Document = {
    "filename": "research-paper.pdf",
    "pages": 12,
    "file_size": "2.4 MB",
    "uploaded_at": "2026-07-22T14:35:20",
    "text": "Complete extracted PDF text..."
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| filename | String | Uploaded file name |
| pages | Integer | Number of pages |
| file_size | String | Size of PDF |
| uploaded_at | DateTime | Upload timestamp |
| text | String | Extracted document text |

---

# Summary Model

Stores AI-generated summaries.

```python
Summary = {
    "short_summary": "...",
    "detailed_summary": "...",
    "generated_at": "2026-07-22T14:36:12"
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| short_summary | String | Quick overview |
| detailed_summary | String | Full summary |
| generated_at | DateTime | Generation timestamp |

---

# Insight Model

Stores extracted key insights.

```python
Insight = [
    {
        "title": "...",
        "description": "..."
    }
]
```

Example

```text
Insight 1

Title:
Main Contribution

Description:
The paper proposes...

----------------

Insight 2

Title:
Results

Description:
Accuracy improved by 14%.
```

---

# Chat Message Model

```python
ChatMessage = {
    "role": "user",
    "message": "...",
    "timestamp": "2026-07-22T14:40:11"
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| role | String | user / assistant |
| message | String | Chat content |
| timestamp | DateTime | Message time |

---

# Chat History

```python
ChatHistory = [
    ChatMessage,
    ChatMessage,
    ChatMessage
]
```

Example

```text
User:
Summarize the methodology.

Assistant:
The methodology focuses on...

User:
Explain Figure 3.

Assistant:
Figure 3 shows...
```

---

# Complete Session Structure

```python
Session = {

    "document": {

        "filename": "...",

        "pages": 15,

        "text": "..."
    },

    "summary": {

        "short_summary": "...",

        "detailed_summary": "..."
    },

    "insights": [

        {},

        {},

        {}

    ],

    "chat_history": [

        {},

        {},

        {}

    ]
}
```

---

# Session Lifecycle

### Step 1

Upload PDF

↓

Create Document Object

---

### Step 2

Extract Text

↓

Save inside Session

---

### Step 3

Generate Summary

↓

Save Summary Object

---

### Step 4

Generate Insights

↓

Save Insight List

---

### Step 5

User asks questions

↓

Append Chat History

---

### Step 6

Session Ends

↓

Memory Cleared

---

# Validation Rules

## Upload

- Only PDF files accepted
- Maximum file size: 20 MB
- Empty PDFs rejected
- Corrupted PDFs rejected

---

## Summary

Cannot generate summary before a PDF is uploaded.

---

## Insights

Insights require extracted document text.

---

## Chat

Questions can only be answered after a successful upload.

---

# Future Database Schema (v2.0)

When persistence is introduced, the following collections/tables may be added:

- Users
- Documents
- Summaries
- Insights
- ChatSessions
- Messages

This is intentionally deferred to keep v1.0 focused and achievable.

---

# Schema Summary

Storage Type:
In-Memory

Persistence:
No

Authentication:
No

Database:
None

Scalability:
Database support planned for v2.0
