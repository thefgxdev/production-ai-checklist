# RAG checklist

Retrieval-augmented generation is a data pipeline with a language model at the end. Most failures are pipeline failures: the right passage was never indexed, was chunked in half, or was outranked by a near-duplicate.

## Ingestion

- [ ] Every source has an owner, an update cadence and a way to detect changes (hash, modified date, webhook).
- [ ] Documents are converted to clean text with structure preserved (headings, tables, lists). Check a sample by eye; PDF extraction lies.
- [ ] Access control is captured at ingestion: each chunk carries who may read it.
- [ ] Deleted or updated sources are removed or replaced in the index within a defined delay.

## Chunking

- [ ] Chunk boundaries respect the document's structure (sections, paragraphs), not a fixed character count alone.
- [ ] Each chunk carries context: document title, section path, date, source URL.
- [ ] Chunk size chosen by measuring retrieval quality on your golden set, not by copying a default.

## Retrieval

- [ ] Hybrid retrieval (vector plus keyword) unless measurement shows one alone is enough. Exact identifiers, codes and names need keyword search.
- [ ] Filters applied before ranking: tenant, permissions, date range, document type.
- [ ] Re-ranking step evaluated: does it improve precision on the golden set enough to justify the latency?
- [ ] Near-duplicate suppression so the context window is not filled with five copies of the same paragraph.

## Generation

- [ ] The system prompt instructs: answer from the context, cite what was used, say when the context does not contain the answer.
- [ ] Citations are verified: every cited chunk id exists and was in the context.
- [ ] The refusal path is tested: questions the corpus cannot answer must be declined, not invented.
- [ ] Output format enforced with a schema when the answer feeds another system.

## Evaluation

- [ ] Golden set: questions with known relevant chunks and known good answers, covering each source and each failure mode.
- [ ] Retrieval metrics (recall@k, precision@k) tracked separately from answer quality.
- [ ] Regression run on every change to chunking, embedding model, retrieval parameters or prompt.
- [ ] Production sampling with human review, weekly, with findings fed back into the golden set.

## Operations

- [ ] Index rebuild is scripted and can run without downtime (build new, swap).
- [ ] Embedding model version recorded per chunk; a model change triggers a full re-embed.
- [ ] Latency budget per stage; the slowest stage has a fallback.
- [ ] Logs record query, retrieved chunk ids, prompt version and model version for every answer, so any answer can be reproduced.
