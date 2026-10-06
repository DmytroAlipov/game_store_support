# game_store_support

AI-powered customer support workflows for an online game store, built with
[n8n](https://n8n.io/). The workflows are provided as JSON exports and need to
be imported into an n8n instance before use.

## Workflows

| Location | Purpose |
| --- | --- |
| [`main_workflow/`](./main_workflow/) | Main support assistant: accepts WhatsApp or webhook messages, checks requests for security risks, and uses AI agents and store data to prepare a response. See the [workflow documentation](./main_workflow/README.md). |
| [`utils/`](./utils/) | Standalone customer-request handler: summarizes a request with OpenAI, emails it to support, and appends it to Google Sheets. See the [utility workflow documentation](./utils/README.md). |

## Getting started

1. Import the relevant workflow JSON file into n8n.
2. Configure the credentials, API endpoints, and other environment-specific
   values required by that workflow.
3. Test the workflow in n8n, then activate it and use its production webhook
   URL or configured messaging channel.

Workflow exports may contain placeholder IDs or service settings. Replace
these with values for your own n8n instance before activating a workflow.
