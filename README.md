# Project Baseline

A reusable foundation for structuring project context, task-driven workflows, and human-AI collaborative engineering.

---

## Overview

**Project Baseline** provides reusable frameworks, operating models, and templates for building software with AI agents.

The project separates two related concerns:

* **Context System Design** — how information is structured, maintained, and made useful to humans and AI systems.
* **Task-Driven Design** — how implementation work is defined, executed, verified, and recorded.

Together, they provide a lightweight foundation for directing AI-assisted development without relying on large, continuously evolving prompts.

The baseline is intended to evolve through use. As additional applications are built with these practices, the frameworks, templates, and examples can be refined based on what works.

---

## Repository Structure

```text
.
├── designs/                             # System and architecture design documents
├── frameworks/
│   ├── context-system-design-v0.2.md    # Framework for Context System Design
│   └── task-driven-design-v0.1.md       # Framework for Task-Driven Design
├── tasks/                               # Active and completed task definitions
├── templates/
│   └── task-base-template.md            # Reusable task definition template
├── .gitignore
└── README.md
```

---

## Frameworks

### Context System Design (v0.2)

Context System Design is an engineering discipline focused on designing how information is discovered, structured, validated, assembled, delivered, and maintained across human-AI systems.

Key concepts include:

* **Core Principles:** Treating context as a first-class system concern, decoupling participant capability from context quality, and designing information around its intended purpose.
* **Context Lifecycle:** `Generation → Discovery → Modeling → Assembly → Validation → Delivery → Decision/Action → Evaluation → Evolution`.
* **Quality Dimensions:** Relevance, completeness, freshness, consistency, traceability, and source reliability.

See [`frameworks/context-system-design-v0.2.md`](frameworks/context-system-design-v0.2.md).

### Task-Driven Design (v0.1)

Task-Driven Design is a methodology for organizing implementation work into discrete, bounded, verifiable tasks.

A task acts as the interface between human direction and AI execution.

The human establishes the direction and desired outcome. The agent executes the task, verifies the implementation, and records what was completed.

See [`frameworks/task-driven-design-v0.1.md`](frameworks/task-driven-design-v0.1.md).

---

## Templates & Tasks

### Task Base Template

[`templates/task-base-template.md`](templates/task-base-template.md) provides the baseline structure for individual tasks stored in the `tasks/` directory.

A task generally contains three sections:

* **For Me** — Human-authored rationale, desired outcome, and review criteria.
* **For Agent** — Human-authored execution instructions, context references, scope, and verification requirements.
* **Completion** — Agent-authored record of what was actually completed, including verification and relevant notes.

The template is intentionally flexible. It provides a starting structure rather than a rigid specification.

---

## Using Project Baseline

### 1. Review the frameworks

Start with the relevant framework documents to understand the principles behind the development process.

### 2. Establish project context

For a new application, establish the project's authoritative context, such as:

```text
README.md
AGENTS.md
design documents
framework documents
structured data
other project-specific artifacts
```

The exact context depends on the project.

### 3. Define the first task

Copy [`templates/task-base-template.md`](templates/task-base-template.md) into `tasks/` and define the first task.

For example:

```text
tasks/Task-001-Establish-Project-Foundation.md
```

### 4. Execute tasks sequentially

The agent completes the current task, verifies the result, and updates its `Completion` section.

The human reviews the completed work and determines the next task.

```text
Human direction
      ↓
    Task
      ↓
Agent execution
      ↓
  Completion
      ↓
Human review
      ↓
  Next task
```

---

## Projects Built With the Baseline

Project Baseline is intended to accumulate examples over time.

Applications built using the frameworks can be added to the repository as examples or referenced as separate projects.

The purpose is not simply to document a methodology.

It is to **use the methodology, observe where it works and where it fails, and improve the baseline through practice.**

---

## Guiding Principle

> **Context provides the information. Tasks provide the direction. The agent executes. The human decides what comes next.**
