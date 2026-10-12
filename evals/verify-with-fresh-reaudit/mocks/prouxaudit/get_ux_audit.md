---
expect:
  auditHandle: string
---

{
  "auditHandle": "pat_Zy9xWv8uTs7rQp6oNm5lKj4iHg3fEd2c",
  "status": "completed",
  "comparison": {
    "status": "comparable",
    "previousCompletedAt": "2026-10-01T09:30:00.000Z",
    "currentCompletedAt": "2026-10-08T11:00:00.000Z",
    "noLongerDetected": 1,
    "stillDetected": 1,
    "newFindings": 0,
    "changes": [
      { "ruleId": "form.label-missing", "location": "/", "status": "no_longer_detected", "previousCount": 1, "currentCount": 0 },
      { "ruleId": "contrast.body-text-low", "location": "/", "status": "still_detected", "previousCount": 1, "currentCount": 1 }
    ]
  }
}