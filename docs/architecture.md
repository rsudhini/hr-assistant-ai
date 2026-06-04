# HR Assistant AI

## Overview

AI-powered HR assistant that provides grounded answers from HR policy documents using RAG.

## Functional Requirements
Document Upload
Support:
PDF
DOCX
Max upload size:
1 MB per document
Query Processing

Token limits:
8k tokens/request
50k/session
100k/day/user
Limits include:
prompt + retrieved context + generated output
Retrieval & Responses
Responses must be grounded only on retrieved HR documents

Citations must include:
document name
section/page if available

Fallback Behavior
If information unavailable:
"I don't know. Please contact hr@company.com"



## Non-Functional Requirements

Security
Only authenticated employees can access
Read-only access
Retrieved content treated as untrusted input
Never follow instructions embedded inside documents
Performance
Response SLA:
10 sec max
Timeout:
graceful fallback
Rate Limiting
Max 10 requests/hour/user
Detect excessive token usage
Observability

Monitor:

prompt injection attempts
latency
token usage
retrieval failures
hallucination/fallback frequency
UI
Responsive web application
Desktop-first

## High-Level Architecture

...

## Ingestion Pipeline

...

## Retrieval Pipeline

...

## Architectural Decisions

### ADR-001: Use Spring AI

Decision:
Use Spring AI for integration with LLMs, embeddings, and vector databases.

Reason:
Aligns with Spring Boot ecosystem and reduces custom integration effort.

---

### ADR-002: Use Qdrant as Vector DB

Decision:
Use Qdrant for storing embeddings and performing vector similarity search.

Reason:
Open-source, easy local setup, good Spring AI integration.

---

### ADR-003: Top-K Set to 3

Decision:
Retrieve top 3 chunks during vector search.

Reason:
Good balance between context quality, latency, and token usage for Phase 1.

---

### ADR-004: Single Active Document Version

Decision:
Only the latest version of a document is searchable.

Reason:
Prevents conflicting answers from multiple policy versions.

---

### ADR-005: JWT Authentication

Decision:
Use JWT-based authentication.

Reason:
Stateless authentication suitable for web applications and API access.