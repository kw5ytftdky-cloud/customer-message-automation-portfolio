# Demo walkthrough

## What you are looking at

This is a documentation showcase of an existing private Flask application.
The JSON responses were captured by running its free local demo with network
sockets blocked. The illustrated cards are rendered from those responses;
they are not screenshots of a customer-facing dashboard or a real mailbox.

No OpenAI model runs in this demo. A small keyword-based classifier supplies the
category, priority and demo summary. Notification text is prepared for inspection,
with no SMTP connection or email transmission.

## A three-minute walkthrough

### 1. Start with a fictional message

Open [fictional-messages.json](demo/fictional-messages.json). The support example is:

```json
{
  "name": "Client Démo D",
  "email": "client.demo.d@example.com",
  "message": "Panne critique : notre accès au service est bloqué."
}
```

English description: a technical service outage is blocking access.
This description is explanatory; the original request remains in French.

### 2. Show the authentication boundary

The first recorded scenario uses an incorrect shared key and receives `401`.
It does not return a category, destination or notification preview.
No credential value is included in this showcase.

### 3. Follow a valid request

The support case receives `200` and contains the following excerpt:

```json
{
  "mode": "demo",
  "analysis_source": "local_rules_demo",
  "recipient": "support@example.com",
  "notification": {
    "status": "simulated",
    "smtp_submitted": false,
    "delivery_confirmed": false
  }
}
```

This is an excerpt, not the entire response. The recorded response also contains
category `support`, priority `high`, a demo summary and a recommended action.
See [recorded-results.json](demo/recorded-results.json) for all fields.

### 4. Compare departments and priorities

The quote case is routed to the fictional commercial address with priority `low`.
The blocked order and support incident are `high`; the billing question is `mid`.
Routing selects an internal service. It does not email the fictional customer.

### 5. Read the notification preview

The preview contains the original message, category, priority, summary and a
recommended next action. The notification is **not sent**. A live SMTP submission,
if later validated, would still not prove receipt in a mailbox.

## Suggested client-facing narration

> A request enters a structured webhook rather than an unreviewed automation.
> Invalid access is rejected. A valid fictional request is categorized, prioritized
> and assigned an internal destination. The prepared notification keeps the original
> context for the receiving team. For this free demonstration, classification is
> simulated locally and no email is sent. Live provider integration is a separate
> validation step before a client rollout.

## How to describe the visuals

- **Overview:** a portfolio illustration with counts derived from the five demo cases.
- **Workflow:** a simplified diagram based on the inspected implementation.
- **Demo results:** a data presentation of actual captured responses, with English case labels.
- **Notification preview:** a presentation of the recorded text and status flags, not a Gmail UI.

The public repository intentionally contains no runnable application or internal
test code. A private walkthrough can be arranged after discussing the project scope.
