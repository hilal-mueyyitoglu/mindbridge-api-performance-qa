# Risk and Defect Analysis

## API contract risks

| Observation if detected | Risk | Follow-up |
| --- | --- | --- |
| `GET /api/courses` returns unexpected status | Routing/service availability regression | Capture HTTP request, response, app version and logs |
| `courses` is absent or not an array | Breaking API contract | Report expected schema, actual body and impact |
| `POST /api/auth/register` accepts `{}` | Missing required-field validation | Capture reproducible evidence and verify invalid accounts cannot be created |
| Invalid POST produces 500 rather than 400 | Unhandled validation error | Capture status, response and correlation IDs; investigate validation flow |

## Potential performance defect — analysis scenario

**Title:** Course catalogue exceeds the p95 latency SLO during concurrent traffic.

**Planned scenario:** 10 virtual users ramped up over 1 second; 10 GET `/api/courses` requests per user.

**Expected:** p95 latency strictly below 2,000 ms.

**Actual:** No preserved measured p95 in this repository. Course lab notes describe an SLO breach, but **this is not a verified defect report from the published JMeter plan**.

**Potential impact:** Slower course discovery and increased abandonment at peak load even if responses return HTTP 200.

### Investigation and verification

1. Reproduce with matching workload and capture an Aggregate Report plus server telemetry.
2. Inspect request queues, CPU/memory saturation, connection pools, database query performance, locks and downstream requests.
3. Compare unloaded response times against the same environment under 10 concurrent users.
4. Validate any fix with the original profile and compare actual p95 to SLO.
5. Record remaining risks and a justified release recommendation.

**Severity/priority:** Determine from verified reproduction and user/business context; do not invent.
