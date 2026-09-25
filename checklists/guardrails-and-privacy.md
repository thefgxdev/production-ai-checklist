# Guardrails and privacy checklist

## Data before tokens

- [ ] Decide which data may leave the company at all. Sensitive categories (health, financial, children, biometrics) get an explicit decision and a documented legal basis.
- [ ] Vendor contracts checked for training on your data, retention, region. The answer is written in the architecture record.
- [ ] Self-hosted or private-endpoint models considered for sensitive workloads; the decision is documented, not defaulted.
- [ ] Pseudonymise before sending where the task allows it (names, ids, addresses replaced by tokens and restored after).

## Input guardrails

- [ ] Schema validation on every input; size limits.
- [ ] Prompt-injection detection on content that comes from outside (documents, web, email), with the rule that content is data, not instruction.
- [ ] Rate limits per user and per tenant; abuse detection.

## Output guardrails

- [ ] Sensitive-data detection on outputs (personal data, secrets, internal identifiers) before they reach a user or a log.
- [ ] Forbidden-action detection for agents: an output that proposes an action outside the allowed set is blocked and reported.
- [ ] Format and schema enforced; malformed outputs are retried or refused, never passed through.
- [ ] Refusal path tested and human-friendly.

## Audit trail

- [ ] Every answer reproducible: input, context, prompt version, model version, output, cost, latency, user, tenant.
- [ ] Human approvals recorded with who and when.
- [ ] Retention of the trail defined; personal data in the trail covered by the same retention rules as everywhere else.

## Rights and transparency (LGPD/GDPR)

- [ ] Users know when they are interacting with a model and when a decision was automated.
- [ ] A path for a human review of an automated decision that affects a person.
- [ ] Deletion requests reach the vector index, the logs and the vendor.

## Security of the integration

- [ ] API keys per environment and per purpose, rotated, never in client code.
- [ ] Egress from the model integration limited to the vendor endpoint.
- [ ] Vendor incidents monitored; a fallback model or a graceful "temporarily unavailable" exists.
