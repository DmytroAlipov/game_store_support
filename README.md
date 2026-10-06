# AI Game Store Support — n8n Workflow

<img width="1714" height="655" alt="Game Store Support" src="https://github.com/user-attachments/assets/e837af97-8e57-469d-be4a-28d342837118" />

An AI-powered customer support workflow for an online video game store, built with **n8n**, **OpenAI**, and **Elasticsearch**.

## What it does

The workflow receives customer messages from **WhatsApp or a webhook**, checks them for security risks, identifies the relevant game, and generates a support response based on the store's actual data.

### Main flow

1. **Receive message** — via WhatsApp or HTTP webhook.
2. **Security Guard** — detects prompt injection, jailbreaks, malicious payloads, data-exfiltration attempts, and other unsafe requests.
3. **Game catalog lookup** — loads the current game catalog and uses Elasticsearch for fuzzy game search when needed.
4. **AI Orchestrator** — determines what the customer needs and delegates the task to specialized agents.
5. **Game Specialist** — retrieves game details, known issues, fixes, and knowledge-base articles.
6. **Policy Agent** — handles refunds, delivery, payments, region restrictions, and warranty questions.
7. **Final response** — returns a concise answer based only on information provided by the connected APIs and tools.
8. **Send response** — returns the result to the webhook or sends it back through WhatsApp.

## Architecture

```text
WhatsApp / Webhook
        │
        ▼
  Normalize Input
        │
        ▼
  Security Guard
        │
   ┌────┴────┐
 Blocked    Safe
   │          │
   │          ▼
   │    Game Catalog
   │          │
   │          ▼
   │   AI Orchestrator
   │      ┌───┴────┐
   │      ▼        ▼
   │ Game Specialist  Policy Agent
   │      │        │
   │      └───┬────┘
   │          ▼
   │     Final Reply
   └──────────┤
              ▼
       Webhook / WhatsApp
```

## Key features

* Multi-channel support: **WhatsApp + HTTP API**
* AI-based security filtering
* Multi-agent architecture
* Elasticsearch fuzzy search
* Game-specific technical support
* Store policy lookup
* Conversation memory
* Fallback handling for API/agent errors
* Responses grounded in external store data rather than model knowledge

## Requirements

* n8n
* OpenAI API
* WhatsApp Business API
* Game Store API
* Elasticsearch
* Configured n8n credentials for the required services

> The API URLs and credentials in the workflow are placeholders and must be configured for the target environment.
