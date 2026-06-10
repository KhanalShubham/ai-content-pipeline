# AI Content Automation Pipeline — Live Demo

A fully automated, end-to-end content publishing system. One topic in, one published article out — with a human approval gate in between.

**Live demo:** type a topic, watch a self-hosted n8n pipeline write the article in real time.

## What the production pipeline does

New Google Sheets row (Status = Pending) → IF gate → Gemini Writer Agent → SEO Analysis Agent → Sheet updated → Markdown to HTML → Approval email (Gmail send-and-wait with Approve/Decline) → if approved: WordPress REST API publish → live URL written back to the sheet.

## What this repo contains

| File | Purpose |
|---|---|
| index.html | The demo site (static, deployed on Vercel). Sends the topic to the n8n webhook and renders the returned article. |
| n8n-demo-workflow.json | The importable n8n workflow powering the public demo (Webhook → Gemini agent → JSON response). |

## Engineering highlights

- **Self-hosted n8n** in Docker on Render (Singapore), tuned to run inside a 512 MB free instance (NODE_OPTIONS=--max-old-space-size=384).
- **Custom OAuth 2.0**: own Google Cloud OAuth client for Sheets + Gmail (consent screen, test users, redirect URIs), and a manual WordPress.com OAuth token exchange for publishing.
- **Human-in-the-loop**: the workflow pauses on a real email and resumes on the recipient's decision — nothing publishes itself.
- **State tracking**: every article's lifecycle (Pending → Written → Published), SEO report and live URL synced back to one Google Sheet by unique row ID.
- **CORS-enabled webhook** so a static Vercel site can talk to the pipeline directly from the browser.

## Built by

**Shubham Khanal** — BSc (Hons) Computing, Kathmandu, Nepal.
Automation · AI/ML · Full-stack.
