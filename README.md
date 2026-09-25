# Production AI Checklist

What it takes for a language-model feature to work on Monday morning, with real data, impatient users and mistakes that cost money. Not a demo checklist. By [Felipe Guedes](https://fgxdev.com), who operates AI systems in production, including a news portal run daily by eleven specialised agents under human editorial responsibility.

The model is the smallest part of the system. Everything else is on this list.

## The first question

**Which error is acceptable?**

- If none: the model does not decide. It suggests, and a human approves. Design the review step first.
- If some: measure the rate, define the limit, and build the evaluation that measures it before shipping.

Model, vendor and architecture come after that answer, never before.

## Checklists

- [`checklists/rag.md`](checklists/rag.md): retrieval is a data pipeline with a language model at the end. Ingestion, chunking, indexing, retrieval quality, citation, refusal.
- [`checklists/agents.md`](checklists/agents.md): tools, permissions, idempotent actions, budgets, stopping conditions, human-in-the-loop.
- [`checklists/evals.md`](checklists/evals.md): golden sets, regression on every change, production sampling, what to measure.
- [`checklists/guardrails-and-privacy.md`](checklists/guardrails-and-privacy.md): input and output filters, prompt injection, data residency, LGPD/GDPR, audit trail.
- [`checklists/cost-and-latency.md`](checklists/cost-and-latency.md): budgets, caching, fallbacks, model routing.

## Principles

1. **Every model output is a hypothesis.** It needs evidence (citations, tool results) before it becomes a fact in your system.
2. **Every action a model takes is idempotent and reversible**, or it is not an action the model takes.
3. **A human is accountable for every decision.** The system records who, and shows them what the model saw.
4. **Evaluate continuously.** A set of cases with known answers, run on every change, plus sampled human review in production. Without this it is not a system, it is a bet.
5. **Sensitive data stays where the law and common sense say it should.** Decide and document before the first token leaves.
6. **Design to swap the model.** Vendors change prices, limits and behaviour. The integration is a boundary; treat it like one.

## Em português

O que é preciso para uma funcionalidade com modelos de linguagem funcionar na segunda-feira de manhã, com dados reais. Checklists de RAG, agentes, avaliação, guardrails e privacidade (LGPD), custo e latência. Serviço de IA em produção em [fgxdev.com/pt/inteligencia-artificial-para-empresas](https://fgxdev.com/pt/inteligencia-artificial-para-empresas/).

## License

MIT.
