# Agent Safety Review Record

Copy this file for each agent and environment you review. Do not paste real secrets, credentials, or personal data into it.

This record documents a review. It does not enforce anything. See the [README](../README.md#a-review-is-not-enforcement).

## Summary

| Field | Value |
| --- | --- |
| Agent name | |
| Purpose (1-2 sentences) | |
| Environment reviewed | |
| Model / prompt version | |
| Tool/schema versions | |
| Deployed configuration revision | |
| Agent owner | |
| Reviewer(s) | |
| Review date | |
| Record version | |
| Next re-review trigger | |

Include changes to tools/schemas, configuration, scopes/permissions, models, prompts, and environments as re-review triggers.

## Tool inventory

| Tool | Can read | Can write / send / spend / delete | Scope limit | Enforced where | High-risk? |
| --- | --- | --- | --- | --- | --- |
| | | | | | |

## Checklist results

Use [docs/checklist.md](../docs/checklist.md). Status: Yes / No / Partial / N/A.

| Section | Status | Evidence reference | Notes |
| --- | --- | --- | --- |
| 1. Scope and inventory | | | |
| 2. Tool permission boundaries | | | |
| 3. Irreversible actions | | | |
| 4. Approval outside untrusted context | | | |
| 5. Retries, loops, budgets | | | |
| 6. Credentials and redaction | | | |
| 7. Tool-result injection | | | |
| 8. Audit evidence | | | |
| 9. Human stop and cancel | | | |
| 10. Change and re-review | | | |

## Scenarios exercised

From [docs/scenarios.md](../docs/scenarios.md). Non-production only.

| Card | Environment | What was tried | Result | Evidence reference |
| --- | --- | --- | --- | --- |
| | | | | |

## Evidence index

Evidence must be minimized and redacted before storage or display, including inputs, tool arguments/results, and approvals. Use access-controlled evidence locations; do not publish operational review records by default.

| Ref | Description | Location | Redacted? |
| --- | --- | --- | --- |
| E1 | | | |

## Open gaps

| Gap | Risk | Owner | Target date | Status |
| --- | --- | --- | --- | --- |
| | | | | |

## Decision

- [ ] Proceed as reviewed
- [ ] Proceed with listed restrictions
- [ ] Do not proceed until gaps are closed

Decision notes:

Signed off by (name, role, date):
