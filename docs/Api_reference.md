# API Reference

## Base URL

http://localhost:8000

## Authentication

All protected APIs require:

Authorization: Bearer <jwt>

---

## 1. Login

### POST /api/v1/auth/login

### Request

{
  "username": "bob_eng",
  "password": "eng123"
}

### Response

{
  "access_token": "<jwt>",
  "token_type": "bearer",
  "role": "engineering",
  "departments_allowed": ["engineering"]
}

---

## 2. Ingest Document

### POST /api/v1/ingest

**Access:** Admin only

### Request

Content-Type: multipart/form-data

- file: PDF or TXT file
- metadata: JSON containing department, category, version, doc_date and chunking_strategy

### Response

{
  "job_id": "<uuid>",
  "status": "processing",
  "doc_id": "<uuid>"
}

---

## 3. Chat

### POST /api/v1/chat

### Request

{
  "query": "What is the annual leave policy?",
  "filters": {
    "department": "hr",
    "category": "policy"
  },
  "retrieval_mode": "hybrid",
  "session_id": "optional-existing-session-id"
}

### Response

{
  "answer": "Employees are entitled to...",
  "sources": [],
  "retrieval_mode_used": "hybrid",
  "confidence": "high",
  "session_id": "..."
}

---

## 4. List Documents

### GET /api/v1/documents

### Query Parameters

- department
- category
- page
- page_size

### Response

{
  "documents": [],
  "total": 42,
  "page": 1
}

---

## 5. Submit Feedback

### POST /api/v1/feedback

### Request

{
  "session_id": "...",
  "query": "...",
  "helpful": true,
  "comment": "Good answer"
}

### Response

{
  "status": "recorded"
}
