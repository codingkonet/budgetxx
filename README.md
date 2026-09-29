# Personal Budget Manager
Production-oriented multi-currency personal finance platform built with Next.js, TypeScript, Prisma/PostgreSQL, Auth.js, Zod and Recharts.

## Architecture
- Next.js App Router / Server Components
- PostgreSQL + Prisma with Decimal money fields
- Auth.js-compatible authentication layer
- Currency-aware ledger preserving original amounts and transaction-time exchange rates
- Responsive fintech UI, RTL-ready for Arabic
- API health endpoint and test foundation

## Setup
1. Install Node.js 20.9+ and PostgreSQL 15+.
2. `cp .env.example .env.local` and configure `DATABASE_URL` and `AUTH_SECRET`.
3. `npm install`
4. `npx prisma migrate dev --name init`
5. `npm run db:seed`
6. `npm run dev`

## Verification
`npm run typecheck`, `npm run lint`, `npm test`, `npm run build`.

## Financial rules
Never store money as JS floating-point values. PostgreSQL Decimal is the source of truth. Transactions retain original currency/amount and transaction-time exchange rate; reporting conversion is never retroactively changed by later rates. Transfers store both legs, currencies, rate and fees.

## Production checklist
Configure a managed PostgreSQL instance, Auth.js secret, email provider for password reset, object storage for receipts, rate limiting/WAF, exchange-rate provider, observability, backups and HTTPS. Run migrations in CI/CD before deploying the application.
