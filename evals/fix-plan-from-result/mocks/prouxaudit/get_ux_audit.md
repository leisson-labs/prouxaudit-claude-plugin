---
expect:
  auditHandle: string
---

{
  "auditHandle": "pat_Ab3dEf6hIj9kLm2nOp5qRs8tUv1wXy4z",
  "status": "completed",
  "result": {
    "schemaVersion": 1,
    "status": "completed",
    "score": 72,
    "overallAssessment": "Solid structure with a few clarity and accessibility gaps.",
    "summary": "The page explains the offer clearly but the primary action competes with secondary links, one form field has no label and body text contrast is low.",
    "findings": [
      {
        "ruleId": "cta.primary-not-distinct",
        "severity": "high",
        "title": "Primary action is not visually distinct",
        "explanation": "The main call to action has the same weight as three neighbouring links.",
        "recommendation": "Give the primary action a single dominant button style.",
        "evidence": [{ "label": "Competing links within 80px", "value": 3 }]
      },
      {
        "ruleId": "form.label-missing",
        "severity": "medium",
        "title": "Email field has no visible label",
        "explanation": "The newsletter field relies on placeholder text only.",
        "recommendation": "Add a persistent visible label.",
        "evidence": [{ "label": "Unlabelled inputs", "value": 1 }]
      },
      {
        "ruleId": "contrast.body-text-low",
        "severity": "medium",
        "title": "Body text contrast is below the recommended ratio",
        "explanation": "Grey body text on a white background is hard to read.",
        "recommendation": "Raise the text colour contrast to at least 4.5:1.",
        "evidence": [{ "label": "Measured contrast ratio", "value": 3.2 }]
      },
      {
        "ruleId": "nav.skip-link-missing",
        "severity": "low",
        "title": "No skip link before the navigation",
        "explanation": "Keyboard users must tab through every navigation item first.",
        "recommendation": "Add a skip-to-content link as the first focusable element.",
        "evidence": [{ "label": "Navigation items before main", "value": 9 }]
      }
    ],
    "opportunities": [],
    "strengths": [
      {
        "ruleId": "content.value-proposition-clear",
        "title": "Value proposition is stated above the fold",
        "explanation": "The headline names the product and the audience.",
        "evidence": []
      }
    ],
    "recommendations": [],
    "coverage": {
      "coverageScore": 0.8,
      "coverageLabel": "medium",
      "confidenceScore": 0.7,
      "confidenceLabel": "medium",
      "evaluatedDimensions": 8,
      "totalDimensions": 10,
      "passedDimensions": 4,
      "flaggedDimensions": 4,
      "uncertainDimensions": 0,
      "skippedDimensions": 2,
      "evidenceDensityScore": 0.6,
      "evidenceCompletenessNote": "Two dimensions were skipped because only the landing page was captured.",
      "missingEvidence": ["checkout flow"],
      "cleanResultJustified": false,
      "minimumOutputSatisfied": true,
      "checkedDimensions": []
    },
    "measurementScope": {
      "auditedUrl": "https://prouxaudit.com/",
      "capturedUrl": "https://prouxaudit.com/",
      "completedAt": "2026-10-01T09:30:00.000Z",
      "captureMethod": "browser",
      "evaluationVersion": "v1",
      "limitations": ["Only the landing page was captured.", "No authenticated pages were evaluated."]
    },
    "publicReportUrl": null
  }
}