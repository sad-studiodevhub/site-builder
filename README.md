# AiSiteBuilder

An AI-powered website builder. Users describe a website in plain text, and the app generates a complete, responsive single-page site (HTML + Tailwind CSS) that can be previewed, iterated on with follow-up prompts, versioned, rolled back, and published to a public gallery.

## Monorepo Structure

```
.
├── client/   React + TypeScript + Vite frontend
└── server/   Express + TypeScript API
```

## Features

- **Prompt-to-website generation** — an initial prompt is enhanced by an LLM and turned into a complete, responsive, Tailwind-styled HTML page.
- **Iterative revisions** — follow-up prompts patch the existing site's code rather than regenerating from scratch.
- **Version history & rollback** — every generation/revision is stored as a `Version`, so a project can be rolled back to any prior version.
- **Credits system** — project creation and revisions cost credits; additional credits are purchased via Stripe checkout.
- **Publishing & community gallery** — projects can be toggled public and browsed by other users.
- **Authentication** — email/session-based auth via `better-auth`.

## Tech Stack

**Client**
- React 19, TypeScript, Vite
- React Router
- Tailwind CSS
- `better-auth` (client), `axios`

**Server**
- Node.js, Express 5, TypeScript
- Prisma ORM + PostgreSQL
- `better-auth` (server) for auth/sessions
- OpenAI SDK against OpenRouter for LLM code generation
- Stripe for payments/webhooks

## Getting Started

### Prerequisites
- Node.js
- A PostgreSQL database

### Server setup

```bash
cd server
npm install
npx prisma migrate deploy   # or `npx prisma migrate dev` locally
npm run server              # dev, with nodemon
```

Create `server/.env` with:

| Variable | Description |
|---|---|
| `DATABASE_URL` | PostgreSQL connection string |
| `TRUSTED_ORIGINS` | Comma-separated list of allowed CORS origins |
| `BETTER_AUTH_SECRET` | Secret used by `better-auth` |
| `BETTER_AUTH_URL` | Base URL of the auth server |
| `AI_API_KEY` | OpenRouter API key used for code generation |
| `STRIPE_SECRET_KEY` | Stripe secret key |
| `STRIPE_WEBHOOK_SECRET` | Stripe webhook signing secret |

### Client setup

```bash
cd client
npm install
npm run dev
```

Create `client/.env` with:

| Variable | Description |
|---|---|
| `VITE_BASEURL` | Base URL of the running API server |

See `How to Run Project.pdf` for a more detailed walkthrough.
