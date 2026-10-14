# Project Roadmap

**Project:** Document Intelligence Pipeline  
**Version:** 0.2  
**Last updated:** 2026-10-13  
**Current phase:** Planning & Architecture

## 1. Purpose

This document tracks project progress, current priorities, upcoming milestones, and future ideas.

It should provide a quick overview of the project's state without requiring the reader to revisit all other documentation.

## 2. Current Status

**Phase:** Planning and architectural design.

**Current focus:** Evaluate the initial document domain, establish the technical architecture, and prepare for proof-of-concept implementation.

### Completed

- [x] Defined the initial product concept and objectives.
- [x] Established the multi-stage document-processing approach.
- [x] Clarified the single-model, chained-prompt strategy.
- [x] Defined preliminary MVP requirements.
- [x] Established initial system boundaries.
- [x] Selected Next.js, React, and TypeScript for the frontend.
- [x] Created the initial documentation structure.
- [x] Drafted documentation revisions for v0.2.

### In Progress

- [ ] Review and finalize documentation v0.2.
- [ ] Evaluate construction specifications as the initial document domain.
- [ ] Define the detailed technical architecture.

### Not Started

- Backend technology selection.
- Detailed data modeling.
- Proof-of-concept implementation.
- AI integration.
- Evaluation framework.
- Full-stack application development.

## 3. Development Milestones

### Milestone 0 — Product Discovery

**Status:** Completed

**Objective:** Establish the project's vision, problem, intended users, and general solution.

**Outcome:** Defined the concept of a source-linked AI document intelligence application.

---

### Milestone 1 — Documentation and Architecture

**Status:** In Progress

**Objective:** Establish a sufficiently clear technical foundation to begin development.

**Tasks**

- [ ] Finalize documentation v0.2.
- [ ] Examine representative construction project specifications.
- [ ] Select the initial document domain.
- [ ] Define system components and responsibilities.
- [ ] Evaluate Python versus TypeScript for the backend.
- [ ] Select an initial technology stack.
- [ ] Define the data structures exchanged between pipeline stages.
- [ ] Design source-reference handling.
- [ ] Define the processing job lifecycle.
- [ ] Establish the initial application structure.

**Deliverable:** An agreed architecture and implementation plan for the proof of concept.

---

### Milestone 2 — Core Pipeline Proof of Concept

**Status:** Not Started

**Objective:** Validate the document-processing workflow before building the complete application.

**Tasks**

- [ ] Implement basic PDF extraction.
- [ ] Implement source-linked chunking.
- [ ] Integrate an initial AI model.
- [ ] Implement structured information extraction.
- [ ] Implement output validation.
- [ ] Implement consolidation.
- [ ] Implement report generation.
- [ ] Implement source-based verification.
- [ ] Produce inspectable structured output.
- [ ] Handle basic processing failures.

**Deliverable:** A working pipeline that transforms a supported PDF into structured, verifiable information.

A CLI or developer-facing script is sufficient for this milestone.

---

### Milestone 3 — Evaluation and Reliability

**Status:** Not Started

**Objective:** Evaluate pipeline quality and improve reliability.

**Tasks**

- [ ] Collect representative test documents.
- [ ] Create manually reviewed reference annotations.
- [ ] Implement a simple summarization baseline.
- [ ] Measure information recall.
- [ ] Validate source references.
- [ ] Evaluate factual claim support.
- [ ] Track processing time and API costs.
- [ ] Identify common failure patterns.
- [ ] Improve prompts and processing logic.
- [ ] Document evaluation results.

**Deliverable:** An evaluated pipeline with documented strengths, limitations, costs, and quality measurements.

---

### Milestone 4 — Full-Stack MVP

**Status:** Not Started

**Objective:** Build a usable web application around the processing pipeline.

**Tasks**

- [ ] Implement frontend structure.
- [ ] Build PDF upload functionality.
- [ ] Connect the frontend and backend.
- [ ] Implement processing status reporting.
- [ ] Implement appropriate storage.
- [ ] Build the structured report viewer.
- [ ] Present extracted information by category.
- [ ] Display supporting source references.
- [ ] Display verification warnings.
- [ ] Implement clear error handling.
- [ ] Test end-to-end functionality.

**Deliverable:** A functional application allowing users to upload supported documents and review structured, source-linked results.

---

### Milestone 5 — Portfolio Preparation

**Status:** Not Started

**Objective:** Prepare the application for technical demonstration.

**Tasks**

- [ ] Improve usability and accessibility.
- [ ] Review security and resource limits.
- [ ] Configure a safe deployment or reliable local demo.
- [ ] Finalize setup instructions.
- [ ] Document implemented architecture and tradeoffs.
- [ ] Present evaluation findings.
- [ ] Add demonstration screenshots or video.
- [ ] Verify reproducible setup and execution.

**Deliverable:** A polished and documented software engineering portfolio project.

## 4. Immediate Next Steps

### Priority 1 — Finalize Documentation

Review v0.2 and ensure it accurately represents our current decisions and open questions.

### Priority 2 — Evaluate Initial Document Domain

Inspect a small number of representative construction project specifications.

Determine:

- Whether their text can be reliably extracted.
- How the documents are structured.
- Which information categories matter.
- Whether external drawings or references are essential.
- Whether they are suitable and authorized for AI-based processing.

### Priority 3 — Detailed Technical Architecture

Define component responsibilities, processing flow, source preservation, and interfaces.

### Priority 4 — Backend Technology Evaluation

Compare Python and TypeScript with respect to:

- AI integration.
- PDF processing.
- Workflow orchestration.
- Data validation.
- Development complexity.
- Learning objectives.

### Priority 5 — First Proof of Concept

Begin with the smallest functional workflow that can parse a document and produce useful structured results.

Avoid introducing unnecessary infrastructure before the core pipeline is validated.

## 5. Open Questions

### Product and Domain

- Will construction be the initial domain?
- Which types of construction documents should be supported?
- What information should be extracted from them?

### Architecture

- Python or TypeScript backend?
- Which PDF parsing approach?
- How should chunking work?
- What schemas should connect stages?
- How should processing state be managed?

### AI and Evaluation

- Which initial model should be selected?
- How should prompts and outputs be validated?
- What constitutes a sufficiently supported claim?
- Which evaluation metrics and thresholds are realistic?

See [DECISIONS.md](DECISIONS.md) for the decision history and detailed alternatives.

## 6. Future Backlog

The following are potential enhancements, not committed deliverables.

### Document Processing

- 500+ page documents.
- OCR and scanned PDFs.
- Advanced table and drawing interpretation.
- Additional document types.
- Multi-document analysis.

### AI Capabilities

- Retrieval-augmented generation.
- Document Q&A.
- Domain-specific processing profiles.
- Model comparison and routing.
- Advanced verification.
- Conditional reprocessing.
- Autonomous agents where justified.

### Application Features

- Saved document history.
- Searchable document libraries.
- Report exporting.
- Advanced report editing.
- User accounts.
- Collaboration and sharing.

### Engineering Improvements

- Parallel processing.
- Workflow checkpoints.
- Background jobs and advanced retries.
- Improved monitoring.
- Automated AI evaluations.
- Performance and cost optimization.

## 7. Known Risks

**Scope creep:** Adding advanced functionality before validating the core pipeline.

**AI reliability:** Missing, misinterpreted, or unsupported information.

**Document complexity:** Inconsistent layouts, scanned pages, and external references.

**Data confidentiality:** Potential use of sensitive real-world project documentation.

**API costs:** Repeated processing of long documents through several AI stages.

**Implementation complexity:** Introducing too many unfamiliar technologies simultaneously.

These risks should guide implementation and scope decisions.

## 8. Documentation Maintenance

- **PROJECT.md:** Update when the product vision or objectives change.
- **REQUIREMENTS.md:** Update when capabilities or acceptance criteria change.
- **ARCHITECTURE.md:** Update when system design changes.
- **DECISIONS.md:** Record significant choices and their rationale.
- **ROADMAP.md:** Update progress, priorities, and upcoming work.

Avoid repeating detailed information across documents.

Each topic should have one authoritative location.

## 9. Next Planned Discussion

**Topic:** Initial Document Domain and Detailed Technical Architecture.

**Goals:**

1. Evaluate construction documentation as the first practical use case.
2. Identify the main system components.
3. Define the processing workflow and data flow.
4. Compare Python and TypeScript backend approaches.
5. Prepare for detailed data modeling and implementation.

**Expected outcome:** A clear technical direction supporting development of the initial proof of concept.
