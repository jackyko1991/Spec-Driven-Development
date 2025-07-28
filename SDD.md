# Spec-Driven Development Workflow

This page illustrates the structured execution flow of spec-driven development when using agentic development tools. It separates planning and execution stages to enhance clarity, maintainability, and traceability in the software development lifecycle.

## Workflow Overview

```mermaid
graph TD
    A[Project Initialization<br>Steering Architect Mode] --> B[Planning Phase<br>Planner Mode]
    
    B1[Phase 1: Requirements<br>- Scenario definition<br>- User story draft<br>- EARS format<br>- requirements.md] 
    B2[Phase 2: Design<br>- Module design<br>- API definition<br>- Sequence diagrams<br>- design.md]
    B3[Phase 3: Tasks<br>- Task breakdown<br>- Dependency analysis<br>- Prioritization<br>- tasks.md]
    
    B --> B1
    B --> B2
    B --> B3

    B --> C[Execution Phase<br>Executor Mode]
    
    C1[Execution Loop<br>1. Pick next task from tasks.md<br>2. Refer to requirements.md & design.md<br>3. Develop & test based on user story<br>4. Mark task as complete]
    C --> C1

    B3 --> D[specs/feature-name/<br>- requirements.md<br>- design.md<br>- tasks.md]
    D --> D1[Delivery Criteria:<br>- User acceptance<br>- Integration tests<br>- Manual QA<br>- Consistency checked]

    C1 --> E[Project Codebase<br>- Implemented features<br>- File structure aligned<br>- Passes tests<br>- Meets requirements]

    style A fill:#e74c3c,color:#fff
    style B fill:#8e44ad,color:#fff
    style B1 fill:#9b59b6,color:#fff
    style B2 fill:#9b59b6,color:#fff
    style B3 fill:#9b59b6,color:#fff
    style C fill:#27ae60,color:#fff
    style C1 fill:#2ecc71,color:#fff
    style D fill:#ecf0f1,color:#000
    style D1 fill:#bdc3c7,color:#000
    style E fill:#f1c40f,color:#000
```

## Why Spec-Driven?

- **Clarity:** Clear separation of planning and execution enhances team collaboration.
- **Traceability:** Requirements and designs are explicitly versioned and referenced.
- **Quality Assurance:** Each feature must meet documented delivery criteria before merging.

## Folder Structure

```text
specs/
  └── feature-name/
      ├── requirements.md
      ├── design.md
      └── tasks.md
```

Each file contains structured documentation to guide development and verification. This enforces discipline and reduces ambiguity across feature development.
