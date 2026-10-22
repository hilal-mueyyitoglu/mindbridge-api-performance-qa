# API Test Cases — MindBridge Education

**Environment:** Simulated local MindBridge learning application, `http://localhost:3000`.
**Approach:** Positive and negative API contract validation using Postman.

## TC-API-01 — Retrieve course catalogue

- **Method:** GET
- **Endpoint:** `/api/courses`
- **Precondition:** Application available on port 3000.
- **Steps:** Send GET in Postman; inspect response status and JSON structure.
- **Expected:** HTTP **200 OK** with top-level `courses` property containing an array.
- **Prior lab notes:** Course activity indicated the expected response and passing scripted assertions.
- **Preserved execution evidence in this repository:** Not available. Reconstructed test request has not been independently rerun.

## TC-API-02 — Registration with invalid body

- **Method:** POST
- **Endpoint:** `/api/auth/register`
- **Request:** `Content-Type: application/json`; body `{}`.
- **Steps:** Send POST in Postman; inspect status and JSON `error.code`.
- **Expected:** HTTP **400 Bad Request** with `error.code = "validation_error"`; registration is rejected.
- **Prior lab notes:** Course activity indicated an expected 400 and passing checks.
- **Preserved execution evidence in this repository:** Not available. Reconstructed test request has not been independently rerun.

## Rationale

Testing only successful API calls may miss broken server-side validation. The second scenario covers the negative path. The Postman collection contains four reusable assertions across two requests and requires the original local lab server.

**Evidence policy:** Lab instructions and expected results are not substitutes for original screenshots or test run exports.
