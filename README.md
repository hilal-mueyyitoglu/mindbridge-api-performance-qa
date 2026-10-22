# MindBridge Education | API & Performance QA Portfolio

**Postman · REST API Validation · Negative Testing · Apache JMeter · Performance SLO Analysis**

A software QA case study based on hands-on **Microsoft Junior QA/Software Tester Professional Certificate** labs (October 2026). The application is a simulated, local education platform: **training work, not production/client testing**.

## Project at a glance

| Focus | Endpoint and scenario | Acceptance criteria |
| --- | --- | --- |
| API positive path | `GET /api/courses` | HTTP 200 and a JSON `courses` array |
| API negative path | `POST /api/auth/register` with `{}` | HTTP 400 and `validation_error` |
| Performance | `GET /api/courses`, 10 users, 1-second ramp-up, 10 loops | 95th-percentile latency **below 2,000 ms** |

**Why this matters:** An API can be functionally correct but slow under concurrent traffic. Positive and negative checks should be complemented with risk-based performance evaluation.

## Repository structure

```text
postman/
  MindBridge_API_Tests.postman_collection.json
  MindBridge_Local.postman_environment.json
jmeter/
  MindBridge_Load_Test.jmx
  README.md
docs/
  API_Test_Cases.md
  Performance_Test_Report.md
  Risk_and_Defect_Analysis.md
evidence/
  README.md
```

## 1. API testing with Postman

The included collection has **two requests and four assertions**:

- **GET Courses — happy path:** HTTP 200 and a JSON response containing a `courses` array.
- **POST Register — invalid request:** an empty JSON object `{}` is rejected with HTTP 400 and `error.code = "validation_error"`.

The course activity indicated successful validations. **The collection in this repository is recreated from documented lab steps, not an exported original execution**, and it was not rerun during publication.

**To run:** start the original MindBridge training application locally on port 3000, import the Postman collection and environment, select `MindBridge Local`, run both requests, and inspect the Postman Test Results. The application server itself is **not** included in this repository.

## 2. Performance testing with Apache JMeter

The reconstructed JMeter test plan uses the following workload:

| Setting | Value |
| --- | --- |
| Endpoint | `GET http://localhost:3000/api/courses` |
| Virtual users | 10 |
| Ramp-up period | 1 second |
| Loop count | 10 per user |
| Expected request attempts | 100 |
| Service Level Objective | **p95 < 2,000 ms** |

Read the **95% Line** from JMeter's *Aggregate Report*. A result **at or above 2,000 ms** is a failure against this strict SLO.

The course scenario described latency degradation under concurrent use and previous lab notes indicated a breach. **The original raw results, exported Aggregate Report, exact p95, and dated run evidence were not available when this portfolio was assembled.** Accordingly, the reconstructed JMX is a test design, not proof of a measured performance failure. See [Performance Test Report](docs/Performance_Test_Report.md).

To reproduce, run the local training application, open [MindBridge_Load_Test.jmx](jmeter/MindBridge_Load_Test.jmx) in JMeter, execute, export the Aggregate Report, and record the observed figures.

## Documentation

- [API test cases and expected results](docs/API_Test_Cases.md)
- [Performance test report and evidence status](docs/Performance_Test_Report.md)
- [Risk and defect analysis](docs/Risk_and_Defect_Analysis.md)
- [Instructions for preserving original evidence](evidence/README.md)
- [JMeter run instructions](jmeter/README.md)

## Evidence integrity

No screenshots, numerical p95 measurements, or production testing results have been fabricated. The Postman collection and JMeter configuration are reusable **reconstructions of course-lab exercises**. Preserve genuine output files in `evidence/` if the exercises are rerun, and update the reporting with exact metrics and run conditions. See [Attribution and scope](LICENSE_NOTES.md).

## Other QA portfolio projects

- [GreenLeaf Grocers — Manual Testing, Playwright, SQL & Defect Reports](https://github.com/hilal-mueyyitoglu/greenleaf-grocers-qa-portfolio)
- [MindBridge Education — Playwright Automation, SQL & QA Reporting](https://github.com/hilal-mueyyitoglu/mindbridge-education-qa-portfolio)

**Connect:** [LinkedIn](https://www.linkedin.com/in/hilal-mueyyitoglu/) · [GitHub profile](https://github.com/hilal-mueyyitoglu)
