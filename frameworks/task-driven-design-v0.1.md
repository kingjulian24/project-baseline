# Task-Driven Design v0.1

## 1. Purpose

Task-Driven Design is a software development methodology for building applications through a sequence of small, explicit, executable tasks.

The central idea is:

> **The task is the unit of development.**

Rather than asking an AI coding agent to build an application from a large, continuously evolving prompt, the project is decomposed into discrete tasks. Each task provides the agent with a bounded objective, the context required to execute it, and clear verification criteria.

The resulting task files form a persistent record of the project's development.

Task-Driven Design is intended to make AI-assisted software development more:

* Focused
* Incremental
* Reviewable
* Reproducible
* Context-efficient
* Recoverable
* Easier to direct

Task-Driven Design does not attempt to replace software architecture, system design, or product discovery. It provides a practical mechanism for moving from decisions and requirements to implementation.

---

## 2. Core Principle

Traditional development often treats implementation as a continuous stream of work:

```text
Requirement
    ↓
Development
    ↓
More requirements
    ↓
More development
    ↓
Changing implementation
```

Task-Driven Design instead creates explicit implementation boundaries:

```text
Requirement
    ↓
Task
    ↓
Implementation
    ↓
Verification
    ↓
Completed Task
    ↓
Next Task
```

Each task should represent a meaningful increment of progress.

The goal is not to make every task small for its own sake.

The goal is to make each task **small enough to understand and large enough to produce meaningful progress**.

---

# 3. The Task as the Unit of Development

A task should answer four questions:

1. **Why are we doing this?**
2. **What should the agent do?**
3. **What should the human care about?**
4. **How do we know it is complete?**

The task therefore contains both human-oriented and agent-oriented information.

The basic structure is:

```text
Task
├── For Me
├── For Agent
└── Completion
```

The first two sections are created before implementation.

The Completion section is populated after implementation.

---

# 4. Task Structure

## 4.1 For Me

`For Me` is the human-facing portion of the task.

It explains why the task exists and what the human should pay attention to when reviewing the result.

It should be concise.

It is not an implementation specification.

It may include:

* The purpose of the task
* The desired outcome
* Important design or product decisions
* Things the human should review
* Judgment criteria that cannot easily be expressed as automated tests

Example:

```markdown
## For Me

Add the Writing section to the homepage.

I want the section to feel like part of the editorial portfolio rather
than a separate blog application.

### Review

- Does the section feel visually consistent with Work?
- Is the hierarchy easy to scan?
- Are the articles clearly presented as external writing?
- Does anything feel unnecessarily complicated?
```

The human does not need to understand every implementation detail to review the result.

---

## 4.2 For Agent

`For Agent` is the operational portion of the task.

It contains the instructions required for the coding agent to execute the task.

It should generally include:

* Objective
* Relevant context
* Scope
* Implementation requirements
* Verification requirements

The exact structure may vary by task.

The task template provides a baseline rather than a rigid schema.

Example:

```markdown
## For Agent

### Objective

Implement the Writing section using the existing structured writing data.

### Context

Read:

- README.md
- designs/personal-website-v1.md
- AGENTS.md
- current task

### Scope

- Create the Writing component.
- Reuse existing SectionHeader and EditorialLink components.
- Consume writing data from the data layer.
- Integrate Writing into App.tsx.
- Remove the temporary writing anchor.
- Leave Contact untouched.

### Verification

- Run npm run build.
- Verify external links.
- Verify responsive behavior.
- Verify semantic heading structure.
```

The agent should not need to infer the intended scope from a long conversational history when the relevant information can be represented in the task.

---

# 5. Completion

`Completion` is an agent-owned section.

The agent updates the current task file after completing the task.

The Completion section provides a concise human-readable record of what happened.

It should answer:

> **What did we actually accomplish?**

It should not simply reproduce the implementation plan.

A typical structure is:

```markdown
## Completion

### What Changed

Implemented the Writing section and integrated it into the homepage.
Writing entries now come from the structured data layer and link to their
original publications.

### Verification

- `npm run build` — passed
- Responsive layout reviewed
- External links verified

### Notes

The existing SectionHeader and EditorialLink components were reused.
No changes were made to the Contact section.
```

The Completion section is therefore the bridge between **planned work** and **actual work**.

---

# 6. Human-Agent Responsibilities

Task-Driven Design intentionally separates responsibilities.

## Human

The human is responsible for:

* Deciding what should be built
* Defining the desired outcome
* Providing relevant context
* Establishing scope boundaries
* Providing judgment criteria
* Reviewing the completed result
* Deciding what should happen next

The human does not need to micromanage implementation details that can reasonably be delegated to the agent.

## Agent

The agent is responsible for:

* Reading the required project context
* Understanding the current task
* Implementing the requested changes
* Respecting scope boundaries
* Running appropriate verification
* Updating the current task's Completion section
* Reporting meaningful deviations or follow-up considerations

The agent should not expand the task simply because additional improvements are possible.

---

# 7. Task Lifecycle

The basic Task-Driven Design workflow is:

```text
1. Identify work
       ↓
2. Create task
       ↓
3. Human defines For Me
       ↓
4. Human defines For Agent
       ↓
5. Agent reads project context
       ↓
6. Agent implements task
       ↓
7. Agent verifies implementation
       ↓
8. Agent updates Completion
       ↓
9. Human reviews result
       ↓
10. Create next task
```

The human should generally return to the project at the boundaries between tasks rather than continuously directing implementation.

This allows the agent to work independently while preserving human control over direction.

---

# 8. Task Sequencing

Tasks are executed sequentially.

A project may therefore contain:

```text
Task 001 — Establish Design Foundation
Task 002 — Implement Navigation
Task 003 — Implement Hero
Task 004 — Implement Selected Work
Task 005 — Implement Elsewhere
Task 006 — Implement Writing
Task 007 — Update Writing Content
Task 008 — Implement Contact
Task 009 — Update Project Content
Task 010 — Final Integration & Review
```

The exact numbering and sequence are project-specific.

A completed task should establish a known state from which the next task can proceed.

This creates a chain:

```text
Task N
  ↓
Known project state
  ↓
Task N+1
  ↓
New known project state
```

---

# 9. Task Boundaries

A task should have a clear boundary.

A useful task typically changes one meaningful aspect of the system.

Examples:

### Good

```text
Implement Writing Section
```

```text
Update Substack Content
```

```text
Add SEO Metadata
```

```text
Implement Contact Section
```

### Too Broad

```text
Finish the Website
```

### Too Narrow

```text
Change the font size of the Writing heading from 40px to 42px
```

The appropriate size depends on the work.

Task-Driven Design does not prescribe a fixed number of files, commits, components, or lines of code per task.

---

# 10. Scope Boundaries

Tasks should explicitly identify what is not part of the task when there is a meaningful risk of scope expansion.

For example:

```markdown
### Scope

- Implement Writing.
- Reuse existing components.
- Integrate Writing into App.tsx.
- Do not implement Contact.
- Do not redesign the existing Work section.
- Do not add RSS integration.
```

Scope boundaries are particularly important when working with AI coding agents because an agent may identify adjacent improvements that are technically reasonable but outside the intended task.

A useful task therefore distinguishes:

```text
Required
Optional
Out of scope
```

The agent should prioritize the first category.

---

# 11. Context References

Tasks should identify the project context the agent needs.

Typical references include:

```text
README.md
AGENTS.md
designs/
frameworks/
src/
current task
```

The task should not duplicate information that already exists in authoritative project documents unless the duplicated information is necessary to clarify the task.

This keeps task files focused.

The task should tell the agent **where to look**, not attempt to reproduce the entire project.

---

# 12. The Task Template

Projects using Task-Driven Design should maintain a reusable task template.

The template provides a baseline structure for creating tasks.

Conceptually:

```text
Task
├── Title
├── Filename
│
├── For Me
│   ├── Purpose
│   └── Review
│
├── For Agent
│   ├── Objective
│   ├── Context
│   ├── Scope
│   └── Verification
│
└── Completion
    ├── What Changed
    ├── Verification
    └── Notes
```

The template should remain flexible.

Not every task requires every subsection.

The purpose of the template is to reduce the cognitive overhead of creating a good task, not to create bureaucratic requirements.

---

# 13. Completion as Project History

Completed tasks form a lightweight project history.

For example:

```text
Task 001
  → Established design system

Task 002
  → Implemented navigation

Task 003
  → Implemented hero

Task 004
  → Implemented selected work

Task 005
  → Implemented elsewhere

...
```

The task files therefore become development artifacts rather than disposable instructions.

A future developer—or an AI agent—can inspect completed tasks to understand how the project evolved.

---

# 14. Follow-Up Tasks

A completed task does not have to be considered perfect.

After reviewing the Completion section and the implementation, the human may:

### Continue normally

```text
Task 011
→ Task 012
```

### Create a corrective task

```text
Task 011 completed
       ↓
Review
       ↓
Task 012 — Correct Writing Layout
```

### Create a refinement task

```text
Task 011 completed
       ↓
Review
       ↓
Task 012 — Refine Mobile Navigation
```

The original task should remain a historical record.

It should not be rewritten to pretend that the original implementation request included changes that were discovered later.

---

# 15. Human Review

Human review should focus primarily on whether the result is **correct and appropriate**, not whether the human personally implemented every technical detail.

The review may include:

* Does it solve the intended problem?
* Does it match the design?
* Does it fit the existing system?
* Does the implementation feel unnecessarily complicated?
* Did the agent make unexpected decisions?
* Is anything missing?
* Is anything present that should not be?

The human may inspect technical implementation when necessary.

However, Task-Driven Design does not require the human to deeply inspect every implementation detail after every task.

The level of review should correspond to the risk and importance of the task.

---

# 16. Review Depth

Different tasks require different levels of human attention.

### Low-risk task

Examples:

* Content update
* Copy change
* Metadata update

Review may primarily be visual or functional.

### Medium-risk task

Examples:

* New UI section
* New component
* Navigation change

Review should include behavior, design, and basic implementation sanity.

### High-risk task

Examples:

* Data architecture
* Authentication
* Payment processing
* Major system changes

Review should be significantly deeper.

Task-Driven Design therefore does not require the human to spend an arbitrary amount of time reviewing every task.

The task determines the appropriate level of scrutiny.

---

# 17. AI Agent Interaction Model

Task-Driven Design changes the relationship between the human and the AI coding agent.

Instead of:

```text
Human
  ↓
Large prompt
  ↓
Agent
  ↓
Large implementation
  ↓
Human corrections
  ↓
More prompts
```

the interaction becomes:

```text
Human
  ↓
Task
  ↓
Agent
  ↓
Completed implementation
  ↓
Completion record
  ↓
Human review
  ↓
Next task
```

The human remains responsible for direction.

The agent is responsible for execution.

The task is the interface between the two.

---

# 18. Relationship to Context System Design

Task-Driven Design and Context System Design are related but distinct.

**Context System Design** concerns the design of the information and context surrounding a system.

It asks questions such as:

* What information is needed?
* Where does it come from?
* How should it be structured?
* How should it be retrieved?
* How should its quality be evaluated?
* How does context change over time?

**Task-Driven Design** concerns how implementation work is organized and executed.

It asks:

* What should be done?
* What is the scope?
* What context does the agent need?
* How should the work be verified?
* What happened after implementation?
* What should happen next?

They can therefore work together:

```text
Context System Design
        ↓
Provides the context
        ↓
Task-Driven Design
        ↓
Structures the implementation
        ↓
AI Coding Agent
        ↓
Application
```

Neither methodology is a replacement for the other.

---

# 19. Reusability

Task-Driven Design is intended to be reusable across projects.

A baseline repository may contain:

```text
/docs
    task-driven-design.md
    context-system-design.md

/templates
    Task-base-template.md

/examples
    project-001/
    project-002/
    project-003/
```

Each application can use the same underlying methodology while maintaining its own:

* `AGENTS.md`
* Design documents
* Task files
* Source code
* Project-specific context

The methodology should evolve as additional projects reveal weaknesses or opportunities for improvement.

---

# 20. Design Principles

Task-Driven Design v0.1 is based on the following principles.

### 1. Direction over micromanagement

The human determines the direction.

The agent handles implementation details where appropriate.

### 2. Tasks over giant prompts

Work should be represented as discrete, meaningful tasks rather than one continuously expanding instruction.

### 3. Context over repetition

Tasks should reference authoritative project context rather than unnecessarily duplicating it.

### 4. Explicit scope

The agent should know what the task includes and, when necessary, what it does not include.

### 5. Verification is part of the task

A task is not complete merely because code was written.

### 6. Completion becomes history

The task records both intended work and actual outcome.

### 7. Human review remains the control point

The agent executes.

The human evaluates direction and result.

### 8. Keep the process lightweight

The methodology should reduce cognitive overhead, not create process for its own sake.

---

# 21. What Task-Driven Design Is Not

Task-Driven Design is not:

* A project-management platform
* A replacement for system design
* A replacement for product requirements
* A rigid ticketing system
* A requirement to create extremely small tasks
* A requirement for extensive documentation
* A replacement for human judgment
* A specific AI coding tool
* A particular programming language or framework

It is a development structure that can be applied to different technologies and AI coding agents.

---

# 22. Version 0.1

This document defines the initial working model of Task-Driven Design.

It is intentionally versioned because the methodology is expected to evolve through use.

Future versions may refine:

* Task decomposition
* Context references
* Review practices
* Agent instructions
* Completion records
* Task dependencies
* Project history
* Evaluation criteria

Changes should be based on observed experience rather than theoretical complexity.

The objective is not to design the perfect development process in advance.

The objective is to establish a simple process that works, observe it across real projects, and improve it deliberately.

---

# 23. Central Principle

> **The task is the interface between human direction and AI execution.**

The human decides where the project should go.

The task gives the agent a bounded piece of that direction.

The agent executes it.

The Completion record captures what actually happened.

The human reviews the result and determines what comes next.

That cycle is the foundation of Task-Driven Design.