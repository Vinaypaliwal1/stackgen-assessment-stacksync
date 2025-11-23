---

description: Explain how to set up and monitor StackSync AI Connector in StackBuilder.

title: StackSync AI Connector

read\_time: '4 min read'

customFields:

&nbsp; ai\_index: true

&nbsp; clusters:

&nbsp;   - appStack

&nbsp;   - cloud2code

audience:

&nbsp; - developer

&nbsp; - DevOps

product\_version: '1.0'

---



\# StackSync AI Connector



\## Overview

StackSync AI Connector synchronizes configuration changes from \*\*appStack\*\* to \*\*Cloud2Code\*\*, ensuring that downstream AI tooling remains up to date. The connector triggers asynchronously (webhook-based) and integrates with \*\*StackBuilder\*\* so users can view sync status. In release X.Y, the UI button label for manual sync changes from \*\*Sync Now\*\* to \*\*Run AI Sync\*\*.



\*\*Where it fits\*\*

\- Source of truth: `appStack` (configuration)

\- Destination: `Cloud2Code` (AI indexing and processing)

\- User-facing monitor: StackBuilder (sync status and basic insights)

\- Trigger: async webhook from appStack that starts the sync job



\## Set up and usage

> Notes: these instructions are based on engineering and product notes from the team (dev Slack thread). Treat some values as placeholders — replace with your environment values.



\### Prerequisites

\- Access to StackBuilder (account + permissions to view stacks)

\- `appStack` and `Cloud2Code` credentials or service accounts

\- Network access to receive webhook callbacks



\### Install / Enable

1\. Ensure `appStack` sends change events to the StackSync webhook endpoint:

&nbsp;  - Configure appStack webhook URL: `https://<STACKBUILDER\_HOST>/api/stacksync/webhook`

2\. In Cloud2Code, enable the StackSync import adapter (see cloud2code docs).

3\. In StackBuilder, enable the StackSync AI Connector for the target stack.



\### Running a sync

\- Manual: In StackBuilder, click \*\*Run AI Sync\*\* (formerly \*\*Sync Now\*\*) on a stack page.

\- Automatic: appStack posts change events to the webhook. StackSync queues an async job to push changes to Cloud2Code.



\### Monitoring

\- Open the stack page in StackBuilder.

\- Look for the StackSync activity panel and recent job entries.

\- If you do not see logs in StackBuilder, check the adapter job queue in Cloud2Code (DevOps access required).



\## Troubleshooting



\### Common error: missing metadata fields



\*\*Problem:\*\* The sync fails when `metadata.json` lacks required fields such as `ai\_index` or `clusters`.  

\*\*Symptom:\*\* Sync job fails quickly or produces a validation error in the job log.



\*\*Steps\*\*



1\. Validate `metadata.json` before pushing:

&nbsp;  - Required fields: `ai\_index` (boolean), `clusters` (array), plus standard metadata (name, version).

2\. Example minimal `metadata.json`:

```json

{

&nbsp; "name": "example-stack",

&nbsp; "version": "1.0.0",

&nbsp; "ai\_index": true,

&nbsp; "clusters": \["appStack", "cloud2code"]

}

```

3\. If validation fails:

&nbsp; - Confirm `ai\_index` exists and is a boolean.

&nbsp; - Confirm `clusters` exist and contain at least one cluster name.

&nbsp; - Re-run the push or re-trigger the webhook.



\### Sync failures



* Verify webhook delivery from `appStack` (retry/backoff logs).
* Check the Cloud2Code adapter queue for processing errors.
* Confirm StackBuilder has permission to display connector logs.



\### If you can’t find logs



* Check Cloud2Code ingestion service logs (ask DevOps).
* Confirm the webhook hit StackBuilder (use delivery IDs or timestamps).
* If unknown, escalate to DevOps — include `metadata.json` and webhook payload.



\## Try it out (Cloud2Code import snippet)



```shell

cloud2code import \\

&nbsp; --source-url "https://appstack.example.com/stacks/<STACK\_ID>/config" \\

&nbsp; --metadata-file ./metadata.json \\

&nbsp; --target cloud2code://<ORG>/<REPO> \\

&nbsp; --auth-token $CLOUD2CODE\_TOKEN

```



\## Assumptions



1. The connector uses an async webhook trigger `appStack` to start sync jobs.
2. StackBuilder surfaces sync status and a manual button (label changing to "Run AI Sync").
3. `ai\_index` and `clusters` are mandatory metadata fields for successful sync.



\## Questions for PM / Dev



1. Where are the canonical logs for successful/failed sync jobs (StackBuilder UI or Cloud2Code service)?
2. What are the expected cluster names for `clusters` in metadata?
3. Can you share the webhook payload schema and retry rules?





