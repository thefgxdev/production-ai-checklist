# Agents checklist

An agent is a loop that reads, decides and acts. The loop is not the hard part. The actions are.

## Tools and permissions

- [ ] Each tool has a written contract: inputs, outputs, side effects, cost, failure modes.
- [ ] Tools that write are separated from tools that read, with separate permissions.
- [ ] The agent runs with the permissions of the principal who started it, never with a service account that can do everything.
- [ ] Destructive tools (delete, send, pay) require an explicit confirmation step or are not exposed.

## Actions are safe to repeat

- [ ] Every action the agent can take is idempotent. An agent that retries a step it already completed is not being thorough; it is sending the email twice.
- [ ] Actions carry an idempotency key derived from the task and the step.
- [ ] Actions are reversible, or the irreversible ones are gated by a human.

## Budgets and stopping

- [ ] Maximum steps, maximum tokens, maximum cost and maximum wall time per task. All four.
- [ ] A stopping condition that is checked by code, not only by the model deciding it is done.
- [ ] Loops detected: the same tool with the same arguments twice in a row ends the task with a report.

## Human in the loop

- [ ] The points where a human approves are chosen by the acceptable-error question, and are part of the design, not a fallback.
- [ ] The human sees what the model saw: inputs, retrieved context, tool results. Approval without context is theatre.
- [ ] Every decision records who approved it, when, and what version of the prompt and model produced the proposal.

## Prompt injection

- [ ] Content read by the agent (web pages, emails, documents, tool outputs) is data, never instructions. The system prompt says so and the tests prove it.
- [ ] Instructions found inside content are surfaced to the human, not executed.
- [ ] Tool outputs are validated against schemas before being fed back.

## Observability

- [ ] Every task has a trace: each step, the prompt, the tool call, the result, the cost.
- [ ] Dashboards for tasks per hour, success rate, cost per task, human-override rate.
- [ ] Alerts on cost spikes and on override rate changes, which are the first sign the model or the data changed.

## Evaluation

- [ ] A set of tasks with known good outcomes, run on every prompt or model change.
- [ ] Adversarial tasks in the set: injection attempts, ambiguous instructions, tools that fail.
- [ ] Production sampling reviewed by humans weekly.
