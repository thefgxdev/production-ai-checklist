# Cost and latency checklist

A feature that works and costs more than it earns is a feature that gets turned off.

## Know the numbers

- [ ] Cost per request measured (input tokens, output tokens, retrieval, re-ranking, tool calls), per feature, per tenant.
- [ ] Monthly budget per feature with alerts at 80 % and 100 %.
- [ ] Latency budget per feature (p50, p95) agreed with product, and per stage inside the feature.

## Reduce

- [ ] Cache: identical or near-identical requests served from cache with a TTL that matches how fast the underlying data changes.
- [ ] Route by difficulty: a small model for classification and extraction, a large one only where measured quality requires it.
- [ ] Trim context: fewer, better chunks beat more chunks. Measure with the golden set.
- [ ] Stream outputs to the user so perceived latency drops even when total latency does not.
- [ ] Batch offline work (embeddings, summaries) and run it off-peak.

## Protect

- [ ] Per-user and per-tenant rate limits on the expensive path.
- [ ] Hard caps on tokens and steps per request.
- [ ] Circuit breaker on the vendor: after N failures or timeouts, fall back to a cheaper model or a non-model path.
- [ ] Timeouts shorter than the caller's timeout at every stage.

## Design to swap

- [ ] The model call is behind one interface with the prompt, the parameters and the version as inputs.
- [ ] Prompts are versioned and can differ per model.
- [ ] Switching vendors is a configuration change plus an eval run, not a rewrite.

## Review monthly

- [ ] Cost per feature trend.
- [ ] Which requests are cached, which are routed to the small model, and whether quality held.
- [ ] Vendor pricing and limits; renegotiate or re-route.
