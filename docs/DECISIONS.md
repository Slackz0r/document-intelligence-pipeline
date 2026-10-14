# Decision Log

**Project:** Document Intelligence Pipeline  
**Version:** 0.2  
**Last updated:** 2026-10-13

## 1. Purpose

This document records significant product and technical decisions, including the reasoning behind them and alternatives considered.

Its purpose is to preserve context, support deliberate engineering choices, and prevent previous decisions from being forgotten or silently changed.

### Decision Statuses

- **Proposed:** Under consideration; not yet accepted.
- **Accepted:** Currently guiding the project.
- **Superseded:** Replaced by a later decision.
- **Rejected:** Considered but deliberately not selected.

Accepted decisions describe the intended approach. They do not necessarily indicate that the corresponding functionality has been implemented.

## 2. Decision Overview

| ID      | Decision                                      | Status     |
| ------- | --------------------------------------------- | ---------- |
| ADR-001 | Software specifications as the initial domain | Superseded |
| ADR-002 | Preserve original source information          | Accepted   |
| ADR-003 | Controlled multi-stage AI workflow            | Accepted   |
| ADR-004 | Structured intermediate data                  | Accepted   |
| ADR-005 | Limited initial document size and format      | Accepted   |
| ADR-006 | Verification as a core feature                | Accepted   |
| ADR-007 | Evaluation and baseline comparison            | Accepted   |
| ADR-008 | Backend programming language                  | Proposed   |
| ADR-009 | Orchestration implementation                  | Proposed   |
| ADR-010 | Single-model strategy                         | Accepted   |
| ADR-011 | PDF parsing strategy                          | Proposed   |
| ADR-012 | Persistence and background processing         | Proposed   |
| ADR-013 | Next.js/React/TypeScript frontend             | Accepted   |
| ADR-014 | Construction as the initial document domain   | Proposed   |
| ADR-015 | Documentation as a maintained source of truth | Accepted   |

## 3. Accepted Decisions

### ADR-002 — Preserve Original Source Information

**Status:** Accepted  
**Date:** 2026-10-13

**Context**

Aggressively filtering document content before subsequent processing could permanently discard important information.

**Decision**

Preserve the original document and its source mappings throughout the pipeline.

Extract and organize information before significant summarization or consolidation.

**Rationale**

This supports traceability, verification, debugging, and future reprocessing.

---

### ADR-003 — Controlled Multi-Stage AI Workflow

**Status:** Accepted  
**Date:** 2026-10-13

**Context**

The application requires several distinct AI processing tasks.

A controlled workflow provides predictable execution without introducing autonomous agents.

**Decision**

Use a predefined processing pipeline consisting of specialized stages:

1. Parsing and chunking.
2. Information extraction.
3. Consolidation.
4. Summarization and structuring.
5. Verification.

**Rationale**

Specialized stages are easier to understand, test, debug, and improve independently.

**Consequences**

The application will control workflow execution and data exchange between stages.

The model strategy is documented separately in ADR-010.

---

### ADR-004 — Structured Intermediate Data

**Status:** Accepted  
**Date:** 2026-10-13

**Context**

Passing unrestricted natural-language responses between processing stages makes validation and downstream processing difficult.

**Decision**

Use predefined structured data representations for AI-generated intermediate results wherever practical.

**Rationale**

Structured information enables validation, persistence, testing, and more predictable processing.

**Consequences**

Data schemas and validation will be important parts of the architecture.

Exact schemas remain undecided.

---

### ADR-005 — Limit Initial Document Size and Format

**Status:** Accepted  
**Date:** 2026-10-13

**Decision**

Initially target one text-based PDF containing approximately 20–50 pages.

**Rationale**

This provides a manageable environment for validating the processing pipeline before introducing large-document complexity.

**Consequences**

500+ page PDFs, OCR, and scanned-document processing are postponed.

---

### ADR-006 — Verification as a Core Feature

**Status:** Accepted  
**Date:** 2026-10-13

**Context**

Generated summaries may contain unsupported claims or omit relevant information.

**Decision**

Include source-based verification within the core workflow.

Verification will evaluate factual support and coverage of extracted information.

**Rationale**

Traceable, verifiable results are central to the application's value.

**Consequences**

The architecture must preserve source evidence and communicate unresolved verification issues.

Verification is not a guarantee of complete correctness.

---

### ADR-007 — Evaluation and Baseline Comparison

**Status:** Accepted  
**Date:** 2026-10-13

**Decision**

Evaluate the multi-stage pipeline against manually reviewed reference documents and compare it with a simpler summarization baseline.

**Rationale**

Additional processing stages should provide measurable benefits rather than complexity for its own sake.

**Consequences**

The project will need evaluation data, quality metrics, and processing cost measurements.

---

### ADR-010 — Use One AI Model With Chained Prompts

**Status:** Accepted  
**Date:** 2026-10-13

**Context**

The original intention was to use one AI model repeatedly with different prompts, not to connect multiple models or autonomous agents.

Earlier discussions introduced those alternatives due to a misunderstanding of the initial proposal.

**Decision**

The MVP will use a single underlying AI model across multiple specialized, chained processing stages.

Each stage will have distinct instructions, inputs, and expected outputs.

**Rationale**

- Reduces implementation complexity.
- Makes individual stages easier to evaluate.
- Avoids unnecessary differences between model providers.
- Preserves flexibility for later improvements.

**Consequences**

Multiple models and autonomous agents are not part of the MVP.

They may be evaluated in the future if a specific need or measurable advantage emerges.

---

### ADR-013 — Frontend Technology Stack

**Status:** Accepted  
**Date:** 2026-10-13

**Decision**

Use Next.js, React, and TypeScript for the application frontend.

**Rationale**

These technologies are familiar, suitable for the intended application, and allow development effort to focus on the less familiar AI and backend challenges.

**Consequences**

Frontend language and framework selection is closed unless future requirements justify reconsideration.

The backend language remains undecided.

---

### ADR-015 — Maintain Documentation as a Source of Truth

**Status:** Accepted  
**Date:** 2026-10-13

**Context**

The project involves multiple interconnected design decisions, technical investigations, and potential future features.

Without consistent documentation, important context may be lost.

**Decision**

Maintain concise, version-controlled Markdown documentation alongside the project.

Each document should have a clearly defined responsibility.

**Rationale**

- Preserves decisions and reasoning.
- Reduces repeated discussions.
- Makes it easier to resume development.
- Improves project maintainability.
- Demonstrates professional engineering practices.

**Consequences**

Documentation should be updated when meaningful decisions or changes occur.

Duplication should be minimized, with each topic having one primary source of truth.

## 4. Superseded Decisions

### ADR-001 — Software Specifications as the Initial Domain

**Status:** Superseded  
**Originally proposed:** 2026-10-13  
**Revisited:** 2026-10-13

**Original Direction**

Focus the MVP on software project specifications.

**Reason for Reconsideration**

This direction was suggested before the original interest in construction project documents was clarified.

Potential access to real construction specifications and industry feedback makes construction a strong alternative.

**Current Position**

The application's purpose remains domain-independent.

The initial document domain is not yet finalized.

Construction is the leading candidate, subject to evaluation.

See ADR-014.

## 5. Proposed Decisions

### ADR-008 — Backend Programming Language

**Status:** Proposed

**Question**

Should the backend be implemented primarily in Python or TypeScript?

**Options**

- Python with a framework such as FastAPI.
- TypeScript with Node.js.
- A hybrid architecture using both languages.

**Considerations**

Python offers a strong document-processing and AI ecosystem, along with an opportunity to develop deeper Python skills.

TypeScript offers familiarity and a more uniform development environment across the application.

A hybrid approach could offer benefits but would introduce additional integration and maintenance complexity.

**Next Step**

Compare practical implementation approaches during technical architecture planning.

---

### ADR-009 — Orchestration Implementation

**Status:** Proposed

**Question**

Should pipeline orchestration use custom application logic or a dedicated framework?

**Options**

- Custom workflow functions.
- An orchestration framework such as LangGraph.

**Current Preference**

Start with a straightforward custom implementation unless technical requirements justify additional tooling.

**Next Step**

Define the execution flow, interfaces, and failure handling before selecting an orchestration approach.

---

### ADR-011 — PDF Parsing Strategy

**Status:** Proposed

**Question**

Which tools and techniques should be used to extract text and structural information from PDFs?

**Options**

- Lightweight PDF text extraction libraries.
- More advanced document-processing tools such as Docling.

**Considerations**

The solution must preserve source references and handle the structure of representative technical documents.

**Next Step**

Evaluate parsing approaches using real sample documents.

---

### ADR-012 — Persistence and Background Processing

**Status:** Proposed

**Question**

How should documents, processing jobs, intermediate results, and reports be stored and managed?

**Candidates**

- PostgreSQL for structured data.
- Separate storage for PDF files.
- Background processing through an appropriate job queue.

**Current Position**

The required data and processing lifecycle must be defined before selecting infrastructure.

A lightweight implementation may be sufficient for the initial proof of concept.

---

### ADR-014 — Construction as the Initial Document Domain

**Status:** Proposed  
**Date:** 2026-10-13

**Context**

The original project idea was inspired by construction project documentation.

There may be access to real historical construction specifications and feedback from someone with industry experience.

**Proposal**

Use construction project specifications as the initial MVP evaluation domain.

**Advantages**

- Access to potentially realistic documents.
- Opportunity for meaningful domain-expert feedback.
- Clear practical use case.
- Strong demonstration of applied problem-solving.

**Risks and Considerations**

- Domain-specific terminology.
- Complex layouts and technical references.
- Potential dependencies on drawings or external standards.
- Confidentiality and permission requirements.

**Decision Pending**

Evaluate representative construction specifications before committing.

The underlying architecture should remain extensible to other document domains.

## 6. Decision-Making Principles

New technical decisions should be evaluated against the following questions:

1. What problem are we solving?
2. Which alternatives are available?
3. What are the advantages and disadvantages?
4. Does the proposed complexity provide meaningful value?
5. Can the approach be tested or evaluated?
6. Does it support maintainability and future development?
7. Do we understand the reasoning well enough to explain the decision?

Decisions should be driven by requirements and evidence rather than technological popularity.

## 7. Maintaining the Decision Log

When a significant decision is made:

1. Record the context and alternatives.
2. Explain the chosen direction.
3. Document important tradeoffs and consequences.
4. Update the decision status.
5. Update the architecture, requirements, or roadmap when relevant.

Superseded decisions should be retained for historical context.

## 8. Related Documentation

- [PROJECT.md](PROJECT.md) — Product objectives.
- [REQUIREMENTS.md](REQUIREMENTS.md) — Functional requirements.
- [ARCHITECTURE.md](ARCHITECTURE.md) — Current design.
- [ROADMAP.md](ROADMAP.md) — Upcoming work.
