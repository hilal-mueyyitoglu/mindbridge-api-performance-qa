# Performance Test Report — MindBridge Course Catalogue

**Source:** Microsoft Junior QA/Software Tester course exercise, October 2026, simulated lab.
**Endpoint:** `GET http://localhost:3000/api/courses`
**Objective:** Determine whether the course catalogue meets its latency SLO during concurrent requests.

## Workload and acceptance criteria

| Parameter | Planned value |
| --- | --- |
| Virtual users | 10 |
| Ramp-up period | 1 second |
| Loops | 10 per user |
| Expected attempted requests | 100 |
| Metric | 95th percentile response time (p95) |
| SLO | **p95 < 2,000 ms** |
| Source for metric | JMeter Aggregate Report, `95% Line` |

## Results and evidence status

| Field | Current status |
| --- | --- |
| Lab scenario | Designed to reveal performance degradation under concurrent traffic |
| Historical lab notes | Reported SLO breach; exact number not retained |
| Observed p95 | **Not available** |
| Original Aggregate Report CSV | **Not available** |
| Screenshot of actual run | **Not available** |
| Verified execution of published `.jmx` | **Not yet performed** |
| Reproducible test design | [JMeter file](../jmeter/MindBridge_Load_Test.jmx) |

**Decision rule:** p95 strictly below 2000 ms = PASS; p95 **at or above** 2000 ms = FAIL. Averages alone do not establish SLO compliance.

**Verdict for this published test artifact:** **UNVERIFIED**. Lab notes describe a threshold breach, but raw evidence and an independently executed measurement are absent. Do not state a measured value or a proven failure for this particular reconstructed JMeter plan.

## Risk assessment and recommended actions

If a verified run breaches the SLO, users may experience slow course search/catalogue loading during traffic spikes. Investigate server concurrency limits, query/lock contention, connection pooling, downstream dependencies, request queues and resource utilization.

To finalize this report:

1. Run the original local application and execute the included JMeter plan.
2. Export the **Aggregate Report**, preserving `95% Line`; do not confuse it with the Summary Report.
3. Save real raw data and a screenshot under `evidence/`.
4. Record run date, environment, JMeter version, exact p95, sample count, error rate and throughput.
5. Assign PASS/FAIL from the observed value; rerun after any fix.

**Integrity note:** A sample or course reference CSV must not be represented as evidence from a real execution.
