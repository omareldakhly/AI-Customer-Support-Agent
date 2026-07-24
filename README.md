AI Customer Support Agent (n8n + RAG + Multi-Tool)

An AI-powered customer support agent built with n8n that answers from real company knowledge, checks order status, creates support tickets, and escalates sensitive conversations to a human — deployed live on Telegram.

The Problem

Small e-commerce businesses lose time and customers to slow, inconsistent support: repetitive policy questions, manual order lookups, and complaints that fall through the cracks without a proper escalation path.

The Solution

An AI Agent that acts as a first line of customer support, with three specialized tools it decides between autonomously:

Knowledge Base (RAG) — Answers policy questions (shipping, returns, payment, hours) from real company documents via vector search, never inventing information.
Order Lookup — Retrieves real order status, shipping date, and tracking number from a live orders database, using dynamic filtering based on what the customer asks.
Ticket Creation + Human Handoff — Automatically opens a support ticket and alerts a human team member when a customer has a genuine complaint, a refund request, or an issue outside the bot's knowledge — with the customer notified their case is being handled.

Every conversation is logged for auditability, and the agent includes production-level safeguards: prompt injection protection, retry logic on external tool failures, and tested edge-case handling (missing orders, malformed input, off-topic questions, and attempts to manipulate the system prompt).

Architecture

The agent runs on a self-hosted n8n instance, using an OpenAI-powered AI Agent node with conversational memory, connected to three tools and two logging/alerting pipelines.

(insert architecture screenshot here)

Flow: Telegram Trigger → AI Agent (OpenAI + Memory) → [Knowledge Base / Order Lookup / Ticket Creation] → Telegram Reply → Conversation Logging (Google Sheets, parallel) New Ticket → Google Sheets Trigger → Telegram Alert (to support team)

Tools Used
n8n (self-hosted via Docker) — orchestration
OpenAI — LLM reasoning + embeddings
Supabase (pgvector) — vector database for RAG
Google Sheets — orders data, ticket tracking, conversation logs
Telegram — customer-facing channel + internal alerts
Quality & Reliability Testing
Test	Expected	Result
Policy question (RAG)	Answers from real source	✅
Order lookup (valid ID)	Returns correct order data	✅
Order lookup (invalid ID)	Clearly states not found	✅
Malformed order number	Asks for clarification	✅
Complaint + refund request	Ticket created + escalated	✅
Off-topic question	Politely declines, stays on scope	✅
Vague/empty message	Asks for clarification	✅
Prompt injection attempt	Refused, instructions not revealed	✅
Request for all customers' data	Refused, per-customer isolation explained	✅
External tool failure	Automatic retry (3 attempts)	✅
Business Value
Reduces response time for common questions from hours to seconds
Cuts manual order-status lookups for the support team
Ensures no complaint goes unnoticed via automatic ticket creation and instant alerts
Full conversation audit trail for quality review and analytics
Built on a self-hosted, cost-transparent stack — no per-seat SaaS fees
Status

Fully functional, tested, and deployed live on Telegram. Ready to be adapted to WhatsApp or a website widget for a real business.
