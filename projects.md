---
layout: page
title: Projects
permalink: /projects/
---

# Projects

A growing collection of production-grade AI systems, automation workflows, and technical experiments built at the intersection of agentic architecture and practical business application.

---

## Project 01 — Basic Content Agentic AI

**Status:** Production-ready · **License:** MIT · [View on GitHub](https://github.com/faisalmrasul/Inquiro-Basic_Content_Agentic-AI)

### What It Does

A sophisticated agentic AI workflow built with n8n that autonomously researches, drafts, critiques, and delivers professional content reports via email — without manual intervention at any step. It accepts a user message and optional content via webhook, routes intelligently through a planning layer, retrieves live web data when needed, self-critiques the output for quality, and delivers a formatted HTML email with scoring metadata.

### The Problem It Solves

Content operations typically fragment across multiple tools — research, writing, review, and delivery all require separate human touchpoints. This system collapses that entire pipeline into a single webhook call, reducing content turnaround time by an estimated **87%** compared to manual workflows.

### Architecture & Key Design Decisions

The system is built around five interconnected layers:

**1. Memory Layer (Supabase)**
Persistent user profile and conversation history stored in Supabase. The agent recalls prior context across sessions, enabling personalised and coherent multi-turn interactions rather than stateless one-shot responses.

**2. Planning & Routing Layer (Groq / Llama-3.3-70b)**
An LLM-powered planner evaluates each incoming request and decides whether it requires live web search or can be answered from existing context and provided content. This conditional routing prevents unnecessary API calls and keeps latency low.

**3. Tool Use Layer (SerpAPI)**
When the planner determines a query needs current information, the agent queries SerpAPI for live web results and incorporates them into the response. When the user provides content directly (article text, PDF summary), the search step is bypassed entirely.

**4. Self-Critique Layer (Critic Agent)**
Before delivery, a dedicated Critic Agent reviews the generated output and assigns a quality score with specific improvement suggestions. If quality falls below threshold, the response is revised. This governance step is what elevates the system from a basic chatbot to a production-grade content pipeline.

**5. Delivery Layer (Gmail OAuth2)**
The final output is formatted as a professional HTML email with quality badges, metadata, and structured sections — delivered directly to the configured recipient. No copy-paste step required.

### Tech Stack

| Component | Technology |
|---|---|
| Orchestration | n8n (self-hosted) |
| LLM | Groq — Llama-3.3-70b-versatile |
| Memory | Supabase (PostgreSQL) |
| Web Search | SerpAPI |
| Email Delivery | Gmail (OAuth2) |
| Trigger | Webhook (POST) |

### Key Capabilities

- Persistent memory across sessions — user profile + conversation history
- Intelligent routing — decides live search vs. content-only processing
- Self-critique system — quality scoring before delivery
- Professional HTML email output with embedded metadata
- Robust error handling and partial retry logic
- Fully importable via single `workflow.json` file

### Use Cases

- Summarising articles, PDFs, and reports on demand
- Researching current events and delivering structured briefings
- Automated client or team reporting pipelines
- Personal knowledge assistant with persistent context

### What I Learned

This project marked the shift from building individual automations to designing systems with feedback loops. The Critic Agent pattern — treating output quality as a first-class concern rather than an afterthought — is the insight I carry into every subsequent build. It demonstrated that production-readiness isn't about adding more features; it's about adding the right governance layer.

### Getting Started

1. Import `workflow.json` into your n8n instance
2. Configure credentials: Groq API, Supabase, Gmail OAuth2, SerpAPI
3. Activate the workflow
4. POST to the webhook with `userMessage` and optional `userContent`

See the [setup guide](https://github.com/faisalmrasul/Inquiro-Basic_Content_Agentic-AI/blob/main/setup-guide.md) for full instructions.

---

*More projects coming as the roadmap progresses — Q3 2026 targets enterprise observability tooling and expanded multi-agent deployments.*
