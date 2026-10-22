# JMeter test execution and interpretation

**Scope:** Simulated MindBridge course-lab service only: `http://localhost:3000/api/courses`. Never direct this workload at an unrelated production service.

1. Start the original MindBridge lab app on port 3000.
2. Open `MindBridge_Load_Test.jmx` in Apache JMeter.
3. Check settings: **10 users**, **1-second ramp-up**, **10 loops**, GET `/api/courses`.
4. Run the test; inspect **Summary Report** and **Aggregate Report**.
5. Read `95% Line` (milliseconds) from the Aggregate Report.
6. Export the real **Aggregate Report → Save Table Data** to `evidence/aggregate_report.csv`.
7. Record run date, test environment, p95, sample count, errors, throughput and PASS/FAIL in `docs/Performance_Test_Report.md`.

**SLO decision:** `p95 < 2000 ms` = PASS. `p95 >= 2000 ms` = FAIL.

**Evidence notice:** The JMX was recreated from the course exercise. It has not been run as part of assembling this portfolio. No authentic run results are bundled.

After starting the local lab app, an optional JMeter command-line run is:

```bash
jmeter -n -t jmeter/MindBridge_Load_Test.jmx -l evidence/results.jtl
```

To generate an HTML dashboard from an actual result file, use an empty output directory:

```bash
jmeter -g evidence/results.jtl -o evidence/html-report
```

Do not publish an unsupported numeric performance result.
