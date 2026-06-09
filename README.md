# Puentes

> AI reasoning agent for understanding diverse community perspectives in Latin America

**Agents League Hackathon 2026 — Reasoning Agents Track — Hack for Good**

---

## What is Puentes?

Puentes is a multi-step reasoning agent built on Microsoft Foundry that helps educators, NGOs, and public service staff access nuanced, verified, and empathetic information about marginalized communities in Guatemala and Central America — including **LGBT+ persons**, **Maya peoples**, and the **Garífuna community**.

It fights misinformation with a transparent 5-step reasoning chain grounded in 33 verified documents (~2,500 pages) from the UN, IACHR, Amnesty International, Human Rights Watch, ILO, Freedom House, and the U.S. State Department.

---

## 5-Step Reasoning Chain

| Step | Action |
|---|---|
| **1. Analyze** | Detects bias or stereotypes in the question and reformulates respectfully |
| **2. Plan** | Identifies perspectives needed: community voice, legal frameworks, historical context |
| **3. Research** | Queries the curated knowledge base of 33 verified documents |
| **4. Contrast** | Presents multiple perspectives including internal community debates |
| **5. Synthesize** | Delivers empathetic, cited response with sources for deeper reading |

---

## Architecture

- **Platform:** Microsoft Foundry (Agent Service)
- **Search:** Azure AI Search (vector index)
- **Knowledge base:** 33 documents (~2,500 pages)
- **Web grounding:** Bing Search (fallback)
- **Model:** GPT-4.1-mini

---

## Knowledge Base Sources

| Category | Sources |
|---|---|
| **LGBT+** | HRW country reports · IACHR LGBTI reports · Amnesty International · U.S. State Dept. |
| **Maya peoples** | UNDRIP · ILO Convention 169 · OHCHR Guatemala reports · IACHR indigenous rulings |
| **Garífuna** | HRW Honduras · IACHR Garífuna cases · U.S. State Dept. Honduras |
| **Legal framework** | Yogyakarta Principles · American Convention on Human Rights · IACHR annual reports |

---

## Safety & Reliability

- Refuses hateful or dehumanizing prompts
- Never speaks FOR communities — amplifies their own voices
- Labels every claim by source type: community voice, legal framework, or external analysis
- Flags uncertainty — never invents citations

---

## Demo Questions

1. *"Why do Maya communities in Guatemala resist certain development projects on their territories?"*
2. *"What are the main challenges faced by LGBT+ persons in accessing healthcare in Central America?"*

---

## Repository Structure

- **agent/system_prompt.md** — Full agent instructions (5-step reasoning chain)
- **docs/architecture.md** — Architecture description and diagram
- **knowledge-base/sources.md** — Full list of all 33 curated documents

---

## Built With

- [Microsoft Foundry Agent Service](https://ai.azure.com)
- [Azure AI Search](https://azure.microsoft.com/en-us/products/ai-services/ai-search)
- GPT-4.1-mini via Azure OpenAI

---

## License

MIT License — open source for educational and social impact use.
