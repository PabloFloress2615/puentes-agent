# Puentes — Architecture

## Overview

Puentes is a multi-step reasoning agent built on Microsoft Foundry Agent Service. It combines a curated knowledge base of 33 verified human rights documents with a transparent 5-step reasoning chain to deliver empathetic, cited answers about diverse communities in Latin America.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                     User Question                           │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│              Microsoft Foundry Agent Service                │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌─────────────────────────┐   │
│  │ ANALYZE  │→ │  PLAN    │→ │       RESEARCH          │   │
│  │          │  │          │  │  (queries knowledge base)│   │
│  │ Detects  │  │ Selects  │  └────────────┬────────────┘   │
│  │ bias in  │  │ perspec- │               │                 │
│  │ question │  │ tives    │  ┌────────────▼────────────┐   │
│  └──────────┘  └──────────┘  │       CONTRAST          │   │
│                               │  Multi-perspective view  │   │
│  ┌─────────────────────────┐  └────────────┬────────────┘   │
│  │     SAFETY LAYER        │               │                 │
│  │ Refuses harmful prompts │  ┌────────────▼────────────┐   │
│  └─────────────────────────┘  │      SYNTHESIZE         │   │
│                               │  Cited empathic answer  │   │
│  ┌─────────────────────────┐  └─────────────────────────┘   │
│  │    Bing Web Search      │                                 │
│  │    (fallback tool)      │                                 │
│  └─────────────────────────┘                                 │
└─────────────────────────────────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│              Knowledge Base — Azure AI Search               │
│                                                             │
│  33 verified documents (~2,500 pages)                       │
│  • UN / OHCHR reports      • ILO Conventions               │
│  • IACHR rulings           • Freedom House                 │
│  • HRW country reports     • Yogyakarta Principles         │
│  • Amnesty International   • U.S. State Dept. reports      │
│                                                             │
│  Communities: Maya peoples · Garífuna · LGBT+ persons       │
└─────────────────────────────────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│            Cited, Empathic Response to User                 │
│         With sources + links for deeper reading             │
└─────────────────────────────────────────────────────────────┘
```

---

## Components

### Microsoft Foundry Agent Service
- Hosts the Puentes agent
- Runs the 5-step reasoning chain
- Manages conversation context
- Enforces safety guardrails

### GPT-4.1-mini (via Azure OpenAI)
- Powers the reasoning at each step
- Follows the system prompt instructions
- Generates cited, structured responses

### Azure AI Search — Vector Index
- Indexes all 33 knowledge base documents
- Enables semantic search across ~2,500 pages
- Returns relevant passages for the RESEARCH step
- Index name: `puentes-knowledge-base`

### Bing Web Search (fallback tool)
- Activated when knowledge base lacks current information
- Grounds responses in recent verified sources
- Secondary to the curated knowledge base

### Safety Layer
- Built into the system prompt
- Refuses hateful or dehumanizing prompts
- Labels content by source type
- Flags uncertainty

---

## Data Flow

1. User submits a question via the Foundry playground or API
2. **ANALYZE** — Agent evaluates the question for bias or stereotypes
3. **PLAN** — Agent identifies which perspectives to consult
4. **RESEARCH** — Azure AI Search queries the knowledge base; Bing Search as fallback
5. **CONTRAST** — Agent compares perspectives and surfaces internal community diversity
6. **SYNTHESIZE** — Agent produces a cited, empathetic response
7. Response is returned to the user with sources and deeper reading links

---

## Microsoft Foundry Resources

| Resource | Name |
|---|---|
| Foundry resource | `puentes-foundry` |
| Project | `puentes-agent` |
| Agent | `puentes-agent` |
| Vector index | `puentes-knowledge-base` |
| Region | East US 2 |
| Model | GPT-4.1-mini (Global Standard) |

---

## Security & Privacy

- No user data is stored between sessions
- Knowledge base contains only publicly available documents
- Agent does not collect or transmit personal information
- All sources are cited and verifiable
