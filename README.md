# AI Products Showcase

Architecture notes for the AI-powered software I build and run. The source for these products is private (they hold customer data), so this repo documents what each one is, how it is built, and what I learned.

**Junaid Burke** · AI Application Engineer · [LinkedIn](https://www.linkedin.com/in/junaid-burke/)

## Products

| Product | What it is | Status |
|---|---|---|
| [Tire Manager Pro](https://tiremanagerpro.com) | Multi-tenant platform for tire and auto shops: inventory, point of sale, purchasing and reporting | In daily use across 3 shops and a warehouse |
| [OttoManagerPro](https://ottomanagerpro.com) | SMS AI service advisor for auto repair shops | Twilio A2P 10DLC approved; piloted at a shop, not adopted |
| [Biblio](https://biblioreader.com) | Private English and Urdu digital library with Google Drive sync and AI-assisted organization | Live, 4,000+ books |
| [Tire Tread](https://github.com/JunaidBurke/tire-tread) | Photo-based tire tread estimator (Next.js, Convex, vision model) | Public demo with source |

## Shared architecture

All shop products run on one multi-schema Supabase (PostgreSQL) platform, with one schema per product.

- **Tenant isolation first:** every tenant row carries an `org_id`, and row-level security policies enforce it in the database, not only in application code
- **Location scoping:** organizations can have several shops, and inventory queries are scoped to the active location (see the public [OttoManagerPro-V2-App](https://github.com/JunaidBurke/OttoManagerPro-V2-App) for a code example)
- **Security playbook:** a written checklist for new tables, policies and migrations, applied across projects

## AI design (OttoManagerPro)

- **Tool calling:** the model calls defined tools rather than answering only in free-form text
- **Structured outputs:** responses are validated against schemas before anything is sent or stored
- **SMS delivery:** Twilio messaging, with the 10DLC registration completed after several rejected campaign submissions
- **Evals:** I found that customers often skip the assistant and use a "Get Quote" button. I treat this as a measurement problem, not a build problem, and my next step is eval infrastructure to diagnose it before adding features.

## Stack

TypeScript · Python · Next.js (App Router) · React · Tailwind CSS · PostgreSQL · Supabase · Prisma · Convex · Twilio · OpenAI and Anthropic APIs

## What I would say about the work honestly

- One product is in daily use by real staff; another was piloted and not adopted. I want both stories visible, because the second one is where I learned the most.
- I ship small, test with the people who use the software, and measure before building more.

## Contact

[LinkedIn](https://www.linkedin.com/in/junaid-burke/)
