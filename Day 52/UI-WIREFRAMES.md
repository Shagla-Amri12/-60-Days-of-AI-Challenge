# PaperMind AI - UI Wireframes

Version: 1.0

Author: Shagla Amri

Project: PaperMind AI

---

# Overview

This document describes the user interface, screen flow, navigation, and low-fidelity wireframes for PaperMind AI v1.0.

The UI is designed to be clean, responsive, and beginner-friendly while keeping the project achievable within the 10-day implementation timeline.

---

# Design Principles

- Clean and minimal interface
- Responsive layout (Desktop & Mobile)
- Fast PDF upload workflow
- Simple navigation
- Accessible typography
- Clear loading and error states

---

# User Journey

```
Landing Page
      │
      ▼
Upload PDF
      │
      ▼
PDF Processing
      │
      ▼
Dashboard
 ┌──────────────┐
 │ Summary      │
 │ Insights     │
 │ Chat         │
 └──────────────┘
      │
      ▼
Ask Questions
      │
      ▼
AI Response
```

---

# Navigation Flow

```
Home
 │
 ▼
Upload PDF
 │
 ▼
Dashboard
 ├── Summary
 ├── Key Insights
 └── Chat
```

---

# Screen 1 - Landing Page

Purpose:
Allow users to upload a PDF.

```
+--------------------------------------------------+
|                  PaperMind AI                    |
|      AI-Powered PDF Knowledge Assistant          |
|                                                  |
|      [ Upload PDF ]                              |
|                                                  |
|      Drag & Drop Supported                       |
|                                                  |
+--------------------------------------------------+
```

Components

- App Logo
- Title
- Subtitle
- Upload Button
- Drag & Drop Area

---

# Screen 2 - Upload Processing

```
+--------------------------------------------------+
| Uploading PDF...                                 |
|                                                  |
| ████████████████ 75%                             |
|                                                  |
| Extracting Text...                               |
+--------------------------------------------------+
```

Components

- Progress Bar
- Loading Spinner
- Status Message

---

# Screen 3 - Dashboard

```
+--------------------------------------------------+
| PaperMind Dashboard                              |
|--------------------------------------------------|
| Uploaded PDF : research.pdf                      |
|                                                  |
| [ Generate Summary ] [ Key Insights ]            |
|                                                  |
| Summary Card                                     |
|                                                  |
| Insights Card                                    |
|                                                  |
| Chat Section                                     |
+--------------------------------------------------+
```

Components

- PDF Information
- Action Buttons
- Summary Card
- Insights Card
- Chat Panel

---

# Screen 4 - Summary

```
+--------------------------------------------------+
| Summary                                          |
|--------------------------------------------------|
| Short Summary                                    |
|                                                  |
| Detailed Summary                                 |
|                                                  |
+--------------------------------------------------+
```

---

# Screen 5 - Key Insights

```
+--------------------------------------------------+
| Key Insights                                     |
|--------------------------------------------------|
| • Main Contribution                              |
| • Methodology                                    |
| • Results                                        |
| • Limitations                                    |
| • Future Work                                    |
+--------------------------------------------------+
```

---

# Screen 6 - Chat Interface

```
+--------------------------------------------------+
| Ask Anything                                     |
|--------------------------------------------------|
| User: What is the main objective?                |
|                                                  |
| AI: The paper focuses on...                      |
|                                                  |
| ____________________________________________     |
| | Type your question...                     |    |
| |___________________________________________|    |
|                  [ Send ]                        |
+--------------------------------------------------+
```

Components

- Chat History
- Input Box
- Send Button
- AI Response Area

---

# Responsive Design

## Desktop

```
---------------------------------------------
| Sidebar | Summary | Insights | Chat       |
---------------------------------------------
```

## Tablet

```
-----------------------
| Summary             |
-----------------------
| Insights            |
-----------------------
| Chat                |
-----------------------
```

## Mobile

```
------------------
Upload

Summary

Insights

Chat
------------------
```

---

# Color Palette

Primary:
- #2563EB (Blue)

Background:
- #F8FAFC

Surface:
- White

Success:
- #22C55E

Warning:
- #F59E0B

Error:
- #EF4444

Text:
- #1F2937

---

# Typography

Heading:
- Inter Bold

Body:
- Inter Regular

Code:
- JetBrains Mono

---

# Icons

Suggested Icon Library

- Lucide React
- Heroicons

Icons

- Upload
- File
- Chat
- Lightbulb
- Summary
- Send

---

# Loading States

- Upload Spinner
- AI Thinking Animation
- Skeleton Cards
- Disabled Buttons During Processing

---

# Error States

- Invalid PDF
- Empty PDF
- Upload Failed
- AI API Error
- Internet Connection Error

---

# Accessibility

- Keyboard Navigation
- Focus Indicators
- High Color Contrast
- Screen Reader Friendly Labels
- Responsive Font Sizes

---

# Future UI Enhancements (v2.0)

- Dark Mode
- PDF Page Preview
- Highlighted Citations
- Multiple Documents
- Search History
- User Accounts
- Export Summary (PDF/Markdown)

---

# UI Summary

Framework:
React + Vite

Styling:
CSS

Icons:
Lucide React

Responsive:
Desktop, Tablet, Mobile

Theme:
Light (v1.0)

Navigation:
Single-page Dashboard
