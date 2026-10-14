# System Architecture

**Project:** Document Intelligence Pipeline  
**Version:** 0.2  
**Status:** Proposed — High-Level Architecture  
**Last updated:** 2026-10-13

## 1. Purpose

This document describes the planned architecture, component responsibilities, processing workflow, and data flow of Document Intelligence Pipeline.

The architecture is currently conceptual. Detailed interfaces, schemas, infrastructure, and backend implementation choices have not yet been finalized.

## 2. Architectural Approach

The system will use a modular, application-controlled AI workflow.

The initial implementation will use **one AI model called repeatedly with specialized, chained prompts**.

Each processing stage will have a defined responsibility, input, and expected output.

The application, not an autonomous AI agent, will control the overall execution sequence.

The architecture should emphasize:

- Separation of concerns.
- Structured and validated data exchange.
- Source preservation and traceability.
- Clear error handling.
- Testability and observability.
- Simplicity and extensibility.

## 3. System Components

### 3.1 Frontend

**Selected stack:** Next.js, React, TypeScript.

Responsibilities:

- Document upload.
- Processing status display.
- Structured report presentation.
- Browsing extracted information.
- Inspecting source references.
- Displaying verification warnings and failures.

The frontend technology choice is accepted.

### 3.2 Backend and Orchestration

**Implementation language:** Undecided.

Responsibilities:

- Validate upload requests.
- Coordinate document processing.
- Execute pipeline stages in the correct sequence.
- Integrate with the AI model API.
- Validate intermediate results.
- Manage processing state and errors.
- Coordinate persistence.
- Collect operational metrics.

Python and TypeScript are the main implementation candidates.

The backend should initially remain as simple as practical.

### 3.3 AI Processing

The AI processing layer will perform specialized operations using one underlying model.

Each stage may use different prompts, inputs, output schemas, and configuration settings.

The initial design does not require multiple model providers or autonomous agents.

The system should nevertheless separate model integration from processing logic so that changing models later does not require redesigning the workflow.

### 3.4 Storage

The system will need to manage:

- Original documents or secure document references.
- Extracted document content.
- Source chunks and metadata.
- Extracted information.
- Consolidated results.
- Generated reports.
- Verification results.
- Processing state.

The database and document storage strategy remain undecided.

PostgreSQL is a candidate for structured application data.

## 4. Proposed Processing Pipeline

The workflow consists of five main stages.

### Stage 1 — Parsing and Chunking

**Input:** Uploaded PDF.

**Responsibilities:**

- Validate the document.
- Extract readable text.
- Preserve page references and available document structure.
- Divide content into manageable chunks.
- Associate chunks with original source locations.

**Output:** Source chunks and document metadata.

This stage does not necessarily require AI.

Chunking should favor logical section boundaries where possible.

The exact chunking strategy and parsing tools remain open decisions.

### Stage 2 — Information Extraction

**Input:** Source chunks and relevant context.

**AI task:** Identify and classify relevant information.

Potential information includes:

- Technical requirements.
- Specifications.
- Materials or components.
- Constraints.
- Responsibilities.
- Dependencies.
- Other domain-specific information.

**Output:** Structured extracted items with source references.

The information categories will be refined after selecting representative documents.

Individual chunks may be processed separately or in parallel.

The original source material must remain available.

### Stage 3 — Consolidation

**Input:** Structured extracted items.

**AI task:** Identify related information, duplicates, and potential inconsistencies.

Responsibilities:

- Group related items.
- Consolidate genuinely equivalent information.
- Preserve supporting evidence.
- Avoid losing meaningful differences.
- Flag potential contradictions where feasible.

**Output:** Consolidated structured information.

Consolidation should not silently resolve conflicting source statements.

### Stage 4 — Summarization and Structuring

**Input:** Consolidated information.

**AI task:** Produce an organized and readable report.

Responsibilities:

- Generate a concise document overview.
- Organize information into meaningful categories.
- Preserve associations between claims and source evidence.
- Produce structured report data suitable for the frontend.

**Output:** Structured report.

The report should be based on validated intermediate information rather than unrestricted summarization of the entire original document.

### Stage 5 — Verification

**Input:** Generated report, extracted information, and original source passages.

**AI task:** Evaluate factual support and information coverage.

Responsibilities:

- Check generated factual claims against source evidence.
- Identify unsupported or potentially misleading statements.
- Check whether verified extracted information is represented in the report.
- Return structured verification results.
- Flag unresolved issues.

**Output:** Verification results and report status information.

Targeted revisions may be added later.

The verification stage will initially use the same AI model as the other stages.

It should receive original source evidence, not rely solely on previous AI-generated outputs.

Using the same model for verification cannot guarantee independent judgment. Programmatic checks and external evaluation remain necessary.

## 5. Conceptual Data Flow

The proposed sequence is:

1. User uploads a PDF through the frontend.
2. Backend validates the upload and initiates processing.
3. Parser extracts text and source metadata.
4. Chunking divides the content into source-linked sections.
5. AI extraction identifies relevant structured information.
6. AI consolidation groups related information.
7. AI summarization produces a structured report.
8. AI verification checks claims and report coverage.
9. Backend stores and returns the results.
10. Frontend presents the report, evidence, and warnings.

The original PDF and extracted source material remain accessible throughout the workflow.

This is a conceptual sequence, not a finalized service architecture.

## 6. Preliminary Data Model

The following are **conceptual entities**, not finalized programming variables, type names, or database table identifiers.

### Document

Represents an uploaded document and its metadata.

### Document Chunk

Represents extracted source content and its location within the original document.

### Extracted Item

Represents a requirement, specification, constraint, or other relevant information identified by the AI.

### Source Reference

Connects extracted information or report claims to supporting source material.

### Consolidated Item

Represents related information that has been grouped or consolidated without discarding underlying evidence.

### Report

Represents the structured information presented to the user.

### Verification Result

Represents the outcome of evaluating extracted information or report claims against source evidence.

### Processing Job

Represents one document-processing execution, including status, progress, and errors.

### Naming Conventions

These entities are written in plain English to distinguish domain concepts from implementation identifiers.

When defining actual code and database schemas, naming conventions should follow the relevant language and technology.

For example:

- TypeScript types/interfaces: `ExtractedItem`
- TypeScript variables: `extractedItem`
- Python variables: `extracted_item`
- SQL tables: `extracted_items` (if using snake_case conventions)

Exact schemas, field names, identifiers, and relationships will be defined during detailed architecture design.

## 7. Source Traceability

Source references are essential to the system's reliability.

Each extracted item should retain sufficient information to locate its supporting source material.

Potential reference properties include:

- Document identifier.
- Chunk identifier.
- Original page number or page range.
- Source text or text-span reference.
- Source position or section metadata.

Page numbers alone may not provide sufficient precision for documents containing many requirements per page.

Source references should therefore be designed to support more precise text locations where practical.

Two checks must remain distinct:

**Reference validity:** Does the source reference point to existing document content?

**Factual support:** Does that source content actually support the generated statement?

A reference may be valid without supporting the claim.

## 8. Workflow Orchestration

The initial workflow will be sequential and application-controlled.

One model will perform multiple specialized operations through different prompts.

An orchestration framework is not required for the initial design.

Potential future capabilities include:

- Parallel extraction.
- Processing checkpoints.
- Background job queues.
- Retry mechanisms.
- Conditional execution.
- Targeted reprocessing.

A custom orchestration implementation or a framework such as LangGraph may be considered when specific technical requirements justify the choice.

## 9. Technology Decisions

### Confirmed

| Component    | Technology / Approach                       |
| ------------ | ------------------------------------------- |
| Frontend     | Next.js, React, TypeScript                  |
| AI Workflow  | One model with multiple chained prompts     |
| Processing   | Structured intermediate data and validation |
| Architecture | Modular, controlled workflow                |

### Under Evaluation

| Component             | Candidate Approaches                                    |
| --------------------- | ------------------------------------------------------- |
| Backend               | Python/FastAPI or TypeScript/Node.js                    |
| AI Provider           | OpenAI, Anthropic, or another suitable provider         |
| PDF Processing        | Lightweight PDF parser or Docling                       |
| Validation            | Pydantic or Zod, depending on backend                   |
| Storage               | PostgreSQL and appropriate document storage             |
| Background Processing | To be selected if required                              |
| Orchestration         | Custom implementation initially; framework if justified |

Technology selection should balance technical suitability, maintainability, complexity, and learning objectives.

See [DECISIONS.md](DECISIONS.md) for decision rationale.

## 10. Reliability and Error Handling

The system should distinguish between:

- Invalid or unsupported documents.
- Parsing failures.
- AI API failures.
- Invalid structured outputs.
- Storage errors.
- Verification failures.
- Incomplete processing.

Failures must be communicated clearly rather than silently producing misleading results.

The architecture should permit future retry and recovery mechanisms without tightly coupling the individual processing stages.

## 11. Security Considerations

Uploaded documents must be treated as untrusted input.

Instructions found inside document content must not be treated as application-level instructions.

Important concerns include:

- File validation.
- Upload limits.
- Secure API credentials.
- Protected document storage.
- Access control.
- Log hygiene.
- Data retention and deletion.
- Protection against unnecessary API usage or resource consumption.

If real construction documents are used, permission and confidentiality requirements must be established before sending them to an external AI provider.

## 12. Open Architectural Questions

The next architecture phase should resolve:

1. Backend language and application structure.
2. Initial PDF parsing strategy.
3. Chunking boundaries and context preservation.
4. Structured schemas connecting pipeline stages.
5. Source-reference representation.
6. AI model and API integration.
7. Storage and processing job lifecycle.
8. Verification statuses and failure handling.
9. Appropriate level of orchestration complexity.

These decisions should be evaluated before implementing the complete application.

## 13. Related Documentation

- [PROJECT.md](PROJECT.md) — Product vision.
- [REQUIREMENTS.md](REQUIREMENTS.md) — Functional requirements.
- [DECISIONS.md](DECISIONS.md) — Architectural decisions.
- [ROADMAP.md](ROADMAP.md) — Implementation milestones.
