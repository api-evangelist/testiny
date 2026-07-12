# Testiny (testiny)

Testiny is a modern test management platform for QA teams that keeps manual and automated test cases, test plans, test runs, and results in a single place, with reporting and integrations for Jira, GitLab, and GitHub. Everything in the product is backed by a documented REST API (base `https://app.testiny.io/api/v1`, authenticated with an `X-Api-Key` header) that exposes projects, test cases, test case folders, test plans, test runs, and automated test runs and results over a consistent CRUD / find / bulk / mapping pattern. Testiny publishes a live OpenAPI schema at `https://app.testiny.io/api/v1/swagger.json`, ships a CLI and npm package (`@testiny/cli`), and offers an HTTP MCP server so AI assistants can manage test cases, runs, and results.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/testiny/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/testiny/refs/heads/main/apis.yml)

## Access Model (honest summary)

- **Public, documented REST API.** Real and live: base `https://app.testiny.io/api/v1`, OpenAPI 3.0.4 schema at `https://app.testiny.io/api/v1/swagger.json` (124 paths), authenticated with an `X-Api-Key` header. Endpoint paths and the auth scheme in this repo are grounded in that live schema.
- **Per-seat SaaS, not open source.** A free-forever tier (up to 3 users, 1,000 combined items) plus paid Starter, Business, and Enterprise tiers. Custom Enterprise adds invoice billing and self-hosting via **Testiny Server**.
- **API is included on every plan.** The REST API, CLI, and npm package are available on all tiers (API keys are a Free-tier feature). The **MCP server** requires a paid or trial plan.
- **No public WebSocket / SSE.** The public surface is request/response REST. The MCP server uses HTTP transport (not a WebSocket). See `review.yml`.
- **Modeled vs. sourced.** Endpoint paths, base URL, auth, and pricing are grounded in Testiny's live docs, OpenAPI schema, and pricing page. Request/response bodies in `openapi/testiny-openapi.yml` are simplified/modeled from the entity pattern; consult the live `swagger.json` for the complete, authoritative schema. Rate limits are modeled from plan/upload limits (Testiny does not publish numeric request-rate limits).

## Tags

- Test Runs
- Test Management
- QA
- Test Cases
- Test Automation
- Quality Assurance
- Testing

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Testiny Test Runs API

Create, read, update, delete, and search test runs, then record results by mapping test cases to a run (result status per test case, with per-step results and attachments). Covers the "test runs" workflow end to end - spin up a run, execute its cases, and capture pass/fail outcomes and evidence.

- **Human URL:** [https://www.testiny.io/docs/rest-api/test-run/](https://www.testiny.io/docs/rest-api/test-run/)
- **Base URL:** `https://app.testiny.io/api/v1`

#### Tags

- Test Runs
- Test Execution
- Results
- QA

#### Properties

- [Documentation](https://www.testiny.io/docs/)
- [API Reference](https://www.testiny.io/docs/rest-api/test-run/)
- [OpenAPI](openapi/testiny-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/testiny.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/testiny.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Testiny Test Cases API

Manage the manual and automated test cases that make up your test library - create, get, update, delete, bulk-edit, and query test cases, organize them into test case folders, save reusable test case queries, and upload attachments to a case.

- **Human URL:** [https://www.testiny.io/docs/rest-api/test-case/](https://www.testiny.io/docs/rest-api/test-case/)
- **Base URL:** `https://app.testiny.io/api/v1`

#### Tags

- Test Cases
- Test Management
- Folders

#### Properties

- [API Reference](https://www.testiny.io/docs/rest-api/test-case/)
- [OpenAPI](openapi/testiny-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/testiny.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/testiny.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Testiny Test Plans API

Create, get, update, delete, search, and bulk-manage test plans - the curated selections of test cases that get executed as test runs - and map test cases into a plan.

- **Human URL:** [https://www.testiny.io/docs/rest-api/test-plan/](https://www.testiny.io/docs/rest-api/test-plan/)
- **Base URL:** `https://app.testiny.io/api/v1`

#### Tags

- Test Plans
- Test Management
- Planning

#### Properties

- [API Reference](https://www.testiny.io/docs/rest-api/test-plan/)
- [OpenAPI](openapi/testiny-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/testiny.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/testiny.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Testiny Projects API

List and retrieve the projects that scope all test cases, plans, and runs, and check the projects the current API key has permission to access. The top-level container every other Testiny resource belongs to.

- **Human URL:** [https://www.testiny.io/docs/rest-api/](https://www.testiny.io/docs/rest-api/)
- **Base URL:** `https://app.testiny.io/api/v1`

#### Tags

- Projects
- Organization
- Test Management

#### Properties

- [API Reference](https://www.testiny.io/docs/rest-api/)
- [OpenAPI](openapi/testiny-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/testiny.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/testiny.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Testiny Automation API

Submit and collect automated test runs and results from CI/CD - manage automation test cases (`atm-testcase`) and automation test runs (`atm-testrun`), submit results, and complete a run. Built for pushing framework output into Testiny and detecting flaky tests.

- **Human URL:** [https://www.testiny.io/docs/rest-api/automation-test-case/](https://www.testiny.io/docs/rest-api/automation-test-case/)
- **Base URL:** `https://app.testiny.io/api/v1`

#### Tags

- Test Automation
- CI/CD
- Automated Test Runs

#### Properties

- [API Reference](https://www.testiny.io/docs/rest-api/automation-test-case/)
- [OpenAPI](openapi/testiny-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/testiny.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/testiny.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/testiny-domain-security.yml)
- [Authentication](authentication/testiny-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/testiny)
- [Website](https://www.testiny.io)
- [Documentation](https://www.testiny.io/docs/)
- [Sign Up](https://app.testiny.io/)
- [Plans](plans/testiny-plans-pricing.yml)
- [Pricing](https://www.testiny.io/pricing/)
- [Rate Limits](rate-limits/testiny-rate-limits.yml)
- [Fin Ops](finops/testiny-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
