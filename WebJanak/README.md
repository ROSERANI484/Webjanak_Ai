# WebJanak 🇮🇳  
### Fine-Tuned LLM–Driven Front-End UI Generation Platform

**WebJanak** is a research-oriented AI system for automated front-end UI generation from natural language.  
It is designed around **fine-tuned base language models**, not prompt chaining or thin API wrappers.

The platform targets **government, academic, and institutional use cases**, where transparency, sovereignty, and architectural clarity matter.

---

## Purpose

WebJanak exists to demonstrate that **UI generation is a reasoning problem**, not a prompt-engineering trick.

It focuses on:
- Intent understanding
- Layout reasoning
- Component hierarchy synthesis
- Accessibility-aware markup generation

---

## What WebJanak Is

- A **model-first** UI generation system  
- A framework for **fine-tuned LLM inference**
- A front-end code synthesis engine
- A government-grade, accessibility-aware design generator

## High-Level Architecture

```

User Intent
↓
Intent Normalization
↓
Fine-Tuned LLM (UI-Aware)
↓
Component & Layout Reasoning
↓
Structured Front-End Code
↓
Live Preview + Project Storage

````

> The **LLM performs the reasoning**.  
> The application layer only orchestrates inference and rendering.

---

### Intended Final System

**Fine-Tuned Base LLM (Qwen Family)**

- Trained on:
  - Government website layouts
  - UI component patterns
  - Accessibility standards (WCAG)
  - Responsive design principles
- Fully self-hosted inference
- No API quotas
- No external dependency
- Full data sovereignty

Conceptual interface:

```ts
generateUI(intent: StructuredIntent): UIGraph
````

---

## Core Features

* Natural language → front-end UI code
* Deterministic layout generation
* Responsive design synthesis
* Accessibility-aware HTML structure
* Bilingual intent handling (English / Hindi)
* Live UI preview
* Local project persistence
* Fallback templates for reliability

---

## Technology Stack

### Frontend

* React (Vite)
* TypeScript
* Semantic HTML
* Minimal CSS
* Prism.js for code visualization

### Backend

* Node.js
* Express
* TypeScript
* Local filesystem-based project storage

---

## Design System (Indian Government)

* Tricolor-inspired palette
* High contrast typography
* Minimal animation
* WCAG-aligned spacing and sizing
* Formal, documentation-friendly UI

```css
Saffron:   #FF9933
White:     #FFFFFF
Green:     #138808
Navy Blue: #000080
```

---

## Use Cases

* Government microsites
* Academic and C-DEC projects
* Student research submissions
* Small enterprises without UI teams
* AI research on code generation
* Offline or sovereign AI deployments

---

## What This Project Demonstrates

* Fine-tunable LLM system design
* Separation of intelligence and tooling
* UI generation as structured reasoning
* Replaceable inference backends
* Responsible AI architecture for public systems

---

## Roadmap

* Fine-tuned Qwen LLM integration
* Component-graph supervision
* Multi-file UI generation
* RAG-assisted standards enforcement
* Offline inference mode
* UI quality evaluation benchmarks

---

## License

MIT License

---

## Attribution

Developed for **India’s digital public infrastructure** 🇮🇳
Focused on **AI sovereignty, research clarity, and long-term deployability**

**WebJanak — Empowering structured UI generation through fine-tuned language models**


