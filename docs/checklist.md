# Agent Safety Review Checklist

Mark each item **Yes / No / Partial / N/A** and note evidence in the [review record](../templates/review-record.md). Treat a "Yes" without evidence as "Partial".

This is a review aid, not enforcement. See the [README](../README.md#a-review-is-not-enforcement).

## 1. Scope and inventory

- [ ] The agent's purpose is written in one or two sentences.
- [ ] Every tool the agent can call is listed, with what it can read, write, send, spend, or delete.
- [ ] The environments are listed (development, staging, production) and which tools exist in each.
- [ ] The model(s), prompt version, tool/schema versions, and deployed configuration revision under review are recorded.
- [ ] An owner is named for the agent and for each high-risk tool.

## 2. Tool permission boundaries

- [ ] Each tool has the narrowest scope that does the job (read-only where possible, limited resources, limited recipients).
- [ ] Permissions are enforced by the tool or gateway, not only described in the prompt.
- [ ] The agent cannot grant itself new tools, scopes, or credentials.
- [ ] Tool arguments are validated server-side (allowed paths, domains, amounts, recipients).
- [ ] Denied calls fail closed and are logged.

See scenario [S1](scenarios.md#s1-tool-permission-boundary).

## 3. Irreversible and externally visible actions

- [ ] Actions that send, publish, pay, delete, or change access are listed as high-risk.
- [ ] High-risk actions require an explicit approval step, or are not available to the agent.
- [ ] The approval shows the exact action: target, recipient, amount, content.
- [ ] Where possible, a reversible path exists (draft, soft delete, hold period).

See scenario [S2](scenarios.md#s2-irreversible-action).

## 4. Approval outside untrusted context

- [ ] The human approver is authenticated outside model-controlled content; the model may request approval but cannot mint or alter the authorization.
- [ ] Text in tool results, documents, web pages, or emails cannot count as approval.
- [ ] The approver sees the actual parameters to be executed, not the agent's summary only.
- [ ] Approvals are bound to one action and its server-validated execution parameters, expire, and cannot be replayed; changed parameters require new approval.

See scenario [S3](scenarios.md#s3-approval-from-untrusted-context).

## 5. Retries, loops, and budgets

- [ ] Limits exist for steps, tool calls, tokens, spend, and wall-clock time per run.
- [ ] Side-effecting calls reuse the same operation key across retries, with atomic deduplication at the side-effect boundary; unknown outcomes are reconciled before retrying.
- [ ] Retries back off and stop; a failed approval is never retried automatically.
- [ ] Hitting a limit stops the run and alerts someone, rather than silently continuing.

See scenario [S4](scenarios.md#s4-retry-loop-and-runaway-budget).

## 6. Credentials and redaction

- [ ] Credentials are injected by the runtime and are not placed in the prompt or model-visible context.
- [ ] Credentials are scoped per agent and per environment, and can be revoked quickly.
- [ ] Inputs, tool arguments/results, approvals, logs, and traces are minimized and redacted for secrets and personal data before storage or display.
- [ ] The agent cannot echo a credential into an outbound message or file.

See scenario [S5](scenarios.md#s5-credential-exposure).

## 7. Tool-result and content injection

- [ ] Content from tools, files, web pages, and messages is treated as data, not instructions.
- [ ] Untrusted content cannot change the agent's goal, recipients, or permissions.
- [ ] High-risk actions triggered after reading untrusted content require approval.
- [ ] Injection cases have been exercised in a non-production environment.

See scenario [S6](scenarios.md#s6-tool-result-injection).

## 8. Audit evidence

- [ ] Each run records sufficient minimized, redacted evidence of who started it, relevant inputs, tool calls with arguments, results, approvals, and outcome; raw sensitive payloads are not required.
- [ ] Records are stored where the agent cannot edit or delete them.
- [ ] A reviewer can reconstruct why a given action happened.
- [ ] Retention period and access to records are defined.

See scenario [S7](scenarios.md#s7-missing-audit-evidence).

## 9. Human stop and cancel

- [ ] A named person can stop a running agent quickly, and knows how.
- [ ] Stop blocks new dispatch and cancels queued work, not only the chat; non-cancellable in-flight operations are documented and their outcomes reconciled.
- [ ] Partial work after a stop is visible, and compensation or manual cleanup steps are documented.
- [ ] Stop has been exercised in a non-production environment.

See scenario [S8](scenarios.md#s8-cannot-stop-or-cancel).

## 10. Change and re-review

- [ ] Triggers for re-review are defined (new tool/schema version, configuration revision, new scope, model or prompt change, new environment).
- [ ] Open gaps have owners and target dates.
- [ ] The review record is dated and versioned.
