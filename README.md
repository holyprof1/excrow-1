Excrow

Fast, developer-friendly escrow service for safer payments between buyers and sellers. Excrow holds funds in a neutral account until both sides meet agreed conditions, then releases or refunds automatically.






Key Features

Multi-party escrow: buyer, seller, optional arbitrator

Funding flows: card, bank transfer, wallet/top-up (provider-agnostic)

Release & refund with programmable conditions and timeouts

Dispute handling with role-based resolution

Webhooks for real-time status updates

Idempotent APIs and signed callbacks

Audit trail for every action

Table of Contents

Architecture

Tech Stack

Getting Started

Environment Variables

Running Locally

Docker

Database & Migrations

API Overview

Webhook Events

Security

Testing

Deployment

Troubleshooting

Roadmap

Contributing

License

Architecture

API service (REST/JSON) – stateless business logic

DB – transactional store for escrows, ledgers, users

Queue/Worker – async tasks (webhooks, retries, settlements)

Payment provider(s) – pluggable (e.g., Paystack, Flutterwave, Stripe)

Webhook relay – signed event delivery to client apps

Client ↔ API ↔ Queue/Worker ↔ Payment Provider
                 ↘ DB ↙

Tech Stack

Replace with your actual stack.

Backend: Django + DRF / Laravel / Node (Express/Fastify)

DB: PostgreSQL / MySQL

Cache/Queue: Redis

Container: Docker

CI/CD: GitHub Actions

Observability: Sentry, OpenTelemetry

Getting Started
Prerequisites

Git, Docker (optional), Python 3.11+ or PHP 8.2+ or Node 20+ (pick your stack)

PostgreSQL 14+ (or MySQL 8+)

Redis 6+

Quick Start (non-Docker)
# 1) Clone
git clone https://github.com/YOUR_ORG/excrow.git
cd excrow

# 2) Create environment
cp .env.example .env
# Fill values (see below)

# 3) Install deps (pick your stack)

# If Django:
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver 0.0.0.0:8000

# If Laravel:
composer install
php artisan key:generate
php artisan migrate
php artisan serve --host=0.0.0.0 --port=8000

# If Node:
npm install
npm run db:migrate
npm run dev

Environment Variables

Create .env from the example and set the values.

# App
APP_ENV=development
APP_URL=http://localhost:8000
APP_SECRET=CHANGE_ME

# Database (Postgres)
DB_ENGINE=postgres
DB_HOST=127.0.0.1
DB_PORT=5432
DB_NAME=excrow
DB_USER=excrow
DB_PASS=YOUR_DB_PASSWORD

# Redis / Queue
REDIS_URL=redis://127.0.0.1:6379/0

# Payments (example: Paystack + Stripe)
PAYSTACK_SECRET_KEY=sk_test_xxx
PAYSTACK_PUBLIC_KEY=pk_test_xxx
STRIPE_SECRET_KEY=sk_test_xxx
STRIPE_WEBHOOK_SECRET=whsec_xxx

# Webhooks (sign outgoing)
WEBHOOK_SIGNING_SECRET=whs_change_me

# Email (optional)
SMTP_HOST=smtp.mailtrap.io
SMTP_PORT=2525
SMTP_USER=YOUR_USER
SMTP_PASS=YOUR_PASS

Running Locally
Start services (DB/Redis) quickly
# Postgres
docker run --name excrow-db -e POSTGRES_PASSWORD=pass \
  -e POSTGRES_USER=excrow -e POSTGRES_DB=excrow \
  -p 5432:5432 -d postgres:14

# Redis
docker run --name excrow-redis -p 6379:6379 -d redis:6

Run the app

Follow the stack setup you chose in Getting Started.
Visit http://localhost:8000/health (or /api/health) to verify.

Docker
# Build & run
docker compose up --build

# First-time DB migrate (Django example)
docker compose exec api python manage.py migrate

# Logs
docker compose logs -f api


Provide a docker-compose.yml including api, db, redis, and optionally a worker.

Database & Migrations
Core Tables (conceptual)

users – accounts, roles (buyer, seller, admin, arbitrator)

escrows – lifecycle: created → funded → released/refunded/canceled → closed

escrow_parties – references buyer/seller per escrow

transactions – funding, fees, payouts; provider refs; idempotency keys

disputes – state & resolution notes

webhook_endpoints / webhook_deliveries – targets & delivery attempts

events – append-only audit/event store

Run migrations via your framework (Django/Laravel/Node ORM).

API Overview

Base URL: https://api.yourdomain.com/v1

Auth: Bearer token (Authorization: Bearer <token>)

Create escrow

POST /escrows

{
  "title": "Logo Design",
  "amount": 250000,
  "currency": "NGN",
  "buyer_id": "usr_123",
  "seller_id": "usr_456",
  "expires_at": "2025-12-31T23:59:59Z",
  "metadata": { "order_id": "ORD-98765" }
}


201 Created

{
  "id": "esc_abc123",
  "status": "created",
  "amount": 250000,
  "currency": "NGN",
  "funding": { "payment_intent_id": "pi_..." },
  "conditions": { "release_after_accept": true }
}

Fund escrow

POST /escrows/{id}/fund

{ "source": "card", "provider": "paystack" }


200 OK

{ "status": "funding_pending", "checkout_url": "https://pay..." }

Mark deliverables accepted (buyer)

POST /escrows/{id}/accept

{ "note": "Files received, looks good." }

Release funds

POST /escrows/{id}/release

{ "to": "seller" }

Cancel (pre-fund or by timeout)

POST /escrows/{id}/cancel

{ "reason": "No longer needed" }

Open dispute

POST /escrows/{id}/disputes

{ "reason": "Work not as described", "evidence": ["https://.../screenshot.png"] }

Retrieve escrow

GET /escrows/{id}

List escrows (filters)

GET /escrows?status=funded&party=buyer&limit=20

Include Idempotency-Key header on write endpoints to ensure safe retries:

Idempotency-Key: 1d8a0c7e-2c2b-4a44-9a2a-xxxx

Webhook Events

Set your endpoint(s) in dashboard or via API. We sign webhook payloads using WEBHOOK_SIGNING_SECRET.

Event types

escrow.created

escrow.funded

escrow.released

escrow.refunded

escrow.canceled

escrow.dispute.opened

escrow.dispute.resolved

payment.failed

webhook.delivery.attempted

Sample payload

{
  "id": "evt_123",
  "type": "escrow.funded",
  "created": 1731240000,
  "data": {
    "escrow_id": "esc_abc123",
    "amount": 250000,
    "currency": "NGN",
    "provider": "paystack",
    "tx_ref": "PSK_..._123"
  },
  "signature": "t=1731240000,v1=HEX_DIGEST"
}


Verify signature

Compute HMAC SHA-256 over the raw body using WEBHOOK_SIGNING_SECRET.

Compare to v1 in the header (constant-time compare).

Return 2xx on success; >=400 triggers retries with backoff.

Security

Enforce HTTPS everywhere; HSTS on the edge.

Store secrets in a vault; never commit .env.

Role-based access control (buyer/seller/admin/arbitrator).

Validate all inputs (length, type, enums).

Use idempotency and optimistic locking on balance/ledger writes.

Rotate API keys & webhook secrets regularly.

Keep dependencies patched; run SAST/DAST in CI.

Testing
# Django
pytest -q

# Laravel
php artisan test

# Node
npm test


Include unit tests for state transitions, webhooks, and provider callbacks.

Add integration tests for full “create → fund → release/refund” flows.

Deployment

Staging: auto-deploy from develop

Production: protected main branch, required checks

Migrations run automatically with zero-downtime strategy

Scale api and worker separately; enable horizontal autoscaling

Observability: traces + metrics; alert on webhook failure rates

Troubleshooting

Funding stuck at pending: check provider dashboard + webhook logs

Duplicate events: ensure idempotent processing on webhooks

Clock skew: verify server time sync (NTP) to validate signatures

Payment mismatch: reconcile with transactions and provider reference

Roadmap

 Milestone rules (partial release, milestones)

 Multi-currency FX support

 Payout batching

 Buyer protection scoring

 GraphQL API

Contributing

PRs welcome! Please open an issue to discuss big changes.
Follow the code style and include tests.

Fork the repo

Create feature branch: git checkout -b feat/awesome

Commit: git commit -m "feat: add awesome"

Push: git push origin feat/awesome

Open PR

License

MIT © YOUR_NAME. See LICENSE
 for details.

Quick Badges & Files to Add

LICENSE (MIT)

.env.example

docker-compose.yml

CONTRIBUTING.md

SECURITY.md

OPENAPI.yaml (optional for API docs)
