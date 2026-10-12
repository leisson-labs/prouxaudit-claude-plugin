---
type: llm
focus: last_message
---

The audit has four findings: cta.primary-not-distinct (high), form.label-missing (medium), contrast.body-text-low (medium), nav.skip-link-missing (low). A fix plan must be one bounded batch of at most three findings.

PASS if the reply is a fix plan whose current batch covers at most three of those findings, ties each item to evidence from the result, and says that no change was made or that the plan is not yet verified. A finding that is explicitly labelled as deferred to a later batch is not part of the current batch.
FAIL if the current batch covers all four findings, claims any issue is fixed or verified, or proposes changes unrelated to the findings in the result.