# Validation and evidence boundaries

Prepared on **24 November 2026**. A successful local demonstration is evidence
about the application workflow, not a substitute for live integration testing.

## Results and attribution

| Check | Result | Provenance |
| --- | --- | --- |
| Windows local tests | 42 passed | Confirmed by the project owner in the preparation request |
| Windows free demo | Verified | Confirmed by the project owner; no Windows screenshot is fabricated here |
| Linux rerun of the private implementation's tests | 42 passed, no skips | Executed during this preparation using Python 3.12.14 |
| Free demo captured again | 5 responses: 401, 200, 200, 200, 200 | Executed locally with sockets prohibited |
| SMTP submissions during demo | 0 | All successful responses state `smtp_submitted: false` |
| OpenAI / Gmail real integration | Not validated | No paid model call or real email transmission performed |

The private source revision and file fingerprints are retained in owner-only
review notes. The core code and demo examples were checked against the private
GitHub repository before capturing the demonstration. Internal tests are not
included in this public showcase.

## What the tests establish

- Missing, incorrect and oversized authentication keys are rejected appropriately.
- Invalid JSON, field types, missing data and oversized payloads are handled.
- Category and priority values are constrained and routing uses configured destinations.
- Invalid or incomplete model responses are refused in simulated tests.
- Missing configuration is detected before external processing.
- OpenAI and SMTP failures are handled using mocks, without exposing raw exception text.
- Demo mode avoids provider construction and marks notifications as simulated.

SMTP TLS configuration and timeouts are specified in the implementation. Provider
connections and their certificates are not validated by the mocked test suite.
The tests are not a penetration test, load test or accuracy benchmark.

## What was captured

[recorded-results.json](demo/recorded-results.json) holds the actual free-demo
responses captured for this showcase. [fictional-messages.json](demo/fictional-messages.json)
contains the corresponding fictional input cases. No real client record or
credential is included. Addresses use the reserved `example.com` domain.

The PNG illustrations present this recorded data with readable typography. They
do not reproduce a Windows terminal, live application dashboard, Gmail inbox,
or GitHub Actions result. The workflow SVG is a diagram, not a screenshot.

## Still to validate before a client rollout

1. OpenAI account access, model compatibility, structured responses and provider errors.
2. Classification quality against a human-reviewed, authorized reference dataset.
3. Gmail authentication, SMTP submission and actual mailbox delivery where needed.
4. The intended HTTP environment, hosting, TLS, access controls and operational limits.
5. Privacy, retention, budget, duplicate/retry behavior and monitoring requirements.

The owner has confirmed the Windows demo and test results. No additional Windows
or PowerShell execution was performed in this cloud preparation. The Flask test
client exercises local request handling without establishing external HTTP reachability.

## Status language

Use **“local workflow validated; demonstration simulated”**.
Do not describe the project as production-certified, AI-accuracy-verified, or proven
to deliver real emails. An HTTP `200` in demo mode is not a delivery receipt.
