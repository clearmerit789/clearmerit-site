# CLEAR MERIT n8n Reliability Templates

Practical workflow templates focused on the boring-but-expensive part of automation: **duplicate actions, stale states, retries, human approval, and operational handoffs**.

These templates are adapted from CLEAR MERIT's own **Internal / Working Demo** systems. They are operating proof, **not external client case studies**.

## Template 01 — Due Action Human Alert

**File:** `CLEAR_MERIT_Due_Action_Human_Alert.json`

### Problem it solves

Teams often store a "next action" and due time in Airtable, but someone still has to remember to open the table and check what is late.

This workflow:

1. checks Airtable every 10 minutes,
2. finds records whose `Next Action At` has passed,
3. excludes closed/rejected/suppressed items,
4. creates an idempotency key so the same due action is not alerted repeatedly,
5. sends **one internal Gmail alert**,
6. leaves the final follow-up to a human.

It deliberately does **not** auto-send customer, candidate, or employee messages.

## Required Airtable fields

- `Status`
- `Next Action`
- `Next Action At`
- `Company`, `Name`, or `Title` as a display label

## Setup

1. Import the JSON into n8n.
2. Connect your Airtable credential.
3. Replace `YOUR_AIRTABLE_BASE_ID` and `YOUR_TABLE_ID`.
4. Connect Gmail.
5. Replace `you@example.com`.
6. Adjust the closed-status values to match your process.
7. Run the **Manual Test** trigger before activating the schedule.

## Reliability checks before activation

Test at least:

- one due item,
- one repeated schedule run,
- one manual rerun,
- one changed next-action time.

Confirm the same record + due time + next action creates only one alert.

## Why human-in-the-loop?

The workflow automates **detection**, not judgment. For customer-facing or sensitive actions, CLEAR MERIT defaults to keeping the final action behind human approval unless stronger safeguards are in place.

## About CLEAR MERIT

CLEAR MERIT helps small teams reduce work that only moves forward when somebody remembers to check, chase, or update it.

https://clearmerit.kr

> Internal / Working Demo disclosure: this template is derived from CLEAR MERIT's own operating systems and is not presented as an external client deployment.
