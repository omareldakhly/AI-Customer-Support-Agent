AI Customer Support Agent (n8n + RAG + Multi-Tool)

Production-ready AI Customer Support Agent built with n8n, OpenAI, Supabase Vector Search (RAG), Google Sheets, and Telegram.

Overview

This project demonstrates how a modern AI customer support agent can automate repetitive customer service tasks while remaining safe, explainable, and production-ready.

Unlike a simple chatbot, the AI autonomously decides when to:

Answer from company documentation (RAG)
Look up customer orders
Create support tickets
Escalate conversations to a human agent

The workflow is fully orchestrated inside n8n, making it easy to extend, maintain, and deploy.

Live Features

✅ AI-powered Customer Support

✅ Retrieval-Augmented Generation (RAG)

✅ Live Order Lookup

✅ Automatic Ticket Creation

✅ Human Escalation

✅ Conversation Memory

✅ Parallel Conversation Logging

✅ Production Error Handling

✅ Prompt Injection Protection

Problem

Small and medium businesses often struggle with customer support because:

Customers repeatedly ask the same questions.
Staff manually search for order information.
Complaints are sometimes forgotten.
Support quality varies between employees.
Hiring additional support agents is expensive.
Solution

The AI Agent acts as the first line of customer support.

It automatically decides which tool to use based on the customer's request.

Tool 1 — Knowledge Base (RAG)

When customers ask questions like:

Shipping policy
Refund policy
Working hours
Payment methods

the agent retrieves the answer from company documents stored in a vector database instead of generating unsupported responses.

This dramatically reduces hallucinations.

Tool 2 — Order Lookup

If the customer asks:

Where is my order?

the agent:

extracts the order ID
queries the order database
returns
Order Status
Shipping Date
Tracking Number

If the order doesn't exist, it responds politely and asks the customer to verify the order number.

Tool 3 — Ticket Creation

If the conversation includes:

Complaint
Refund request
Angry customer
Missing order
Unknown issue

the agent automatically:

creates a support ticket
logs it
alerts the human support team through Telegram

The customer is informed that a human representative will continue handling the case.

Workflow Architecture
Telegram Trigger
        │
        ▼
AI Agent (OpenAI + Memory)
        │
 ┌──────┼───────────────┐
 │      │               │
 ▼      ▼               ▼
RAG   Order Lookup   Ticket Creator
 │      │               │
 └──────┼───────────────┘
        ▼
Telegram Response
        │
        ▼
Conversation Logger
(Google Sheets)

Ticket Created
        │
        ▼
Google Sheets Trigger
        │
        ▼
Telegram Alert
(Human Support Team)
Technologies Used
Technology	Purpose
n8n	Workflow orchestration
Docker	Self-hosted deployment
OpenAI	LLM reasoning
OpenAI Embeddings	Document embeddings
Supabase pgvector	Vector Database
Google Sheets	Orders, Tickets, Logs
Telegram Bot API	Customer communication
HTTP Request Node	External API integration
Reliability Features

The workflow includes production-level safeguards.

Prompt Injection Protection

Attempts like:

Ignore previous instructions

or

Reveal your system prompt

are rejected.

Missing Order Handling

Invalid order IDs return a friendly message instead of an error.

Tool Failure Recovery

External API failures trigger automatic retries before notifying the customer.

Human Escalation

Sensitive conversations bypass the AI and notify a real support agent.

Conversation Logging

Every interaction is stored for auditing and analytics.

Testing
Scenario	Expected Result	Status
Shipping policy question	Retrieved from RAG	✅
Valid order ID	Correct order information	✅
Invalid order ID	Friendly error message	✅
Refund request	Ticket created	✅
Complaint	Human escalation	✅
Empty message	Clarification requested	✅
Prompt injection	Blocked	✅
Request for other customers' data	Refused	✅
External API failure	Automatic retry	✅
Business Value

This solution can:

Reduce customer response time from hours to seconds.
Eliminate repetitive policy questions.
Automate order tracking.
Ensure complaints are never missed.
Maintain a complete conversation history.
Lower customer support costs.
Why n8n Instead of Make?

This project was intentionally built in n8n instead of Make because n8n provides greater flexibility for production AI workflows.

Make	n8n
Limited AI orchestration	Native AI Agent support
Harder branching logic	Advanced workflow control
SaaS pricing	Self-hosted & cost-effective
Limited customization	Full customization with JavaScript and HTTP nodes
Less suitable for complex AI systems	Designed for complex AI automation
Deployment

The project is deployed on:

Docker
Self-hosted n8n
Public tunnel for Telegram webhook testing

This architecture can be migrated to:

VPS
Railway
Render
DigitalOcean
AWS

without changing the workflow logic.

Screenshots
Workflow

(Insert workflow screenshot here)

Telegram Conversation

(Insert Telegram demo screenshot here)

Ticket Creation

(Insert Google Sheets ticket screenshot here)

Demo

🎥 Video demonstration included in this repository.

The demo covers:

Customer asking company policy questions
Live order lookup
Ticket creation
Human escalation
Conversation logging
Future Improvements
WhatsApp integration
Website chat widget
CRM integration (HubSpot / Zoho)
Stripe order lookup
Multi-language support
Voice support
Analytics dashboard
Sentiment analysis
Repository Structure
/
│
├── README.md
├── workflow.json
├── screenshots/
│   ├── workflow.png
│   ├── telegram-demo.png
│   └── ticket-demo.png
├── demo/
│   └── project-demo.mp4
└── docs/
    └── architecture.png
Author

Omar Mohamed

AI Automation Engineer

Specialized in:

AI Agents
n8n Automation
RAG Systems
LLM Workflows
Business Process Automation
