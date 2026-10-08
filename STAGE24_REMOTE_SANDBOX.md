# MFootball Stage 24 — Remote Betting Sandbox

Stage 24 establishes a client/server contract for regulated betting infrastructure while keeping cash betting disabled.

## Added
- Authenticated versioned API client (`/api/v1/...`)
- Idempotency key on bet placement to prevent duplicate submissions
- Server-authoritative wallet and risk-profile reads
- Structured bet selections and receipts
- Explicit production safety gate: `REAL_MONEY_BETTING_ENABLED = false`
- Separation of sandbox credits from any future cash wallet

## Expected sandbox endpoints
- `POST /api/v1/bets`
- `GET /api/v1/bets/{betId}`
- `GET /api/v1/wallet`
- `GET /api/v1/risk/profile`
- `POST /api/v1/bets/{betId}/cancel` (where legally/operationally permitted)
- `GET /api/v1/audit/events`
- `POST /api/v1/reconciliation/run`

## Server requirements
The server must validate authentication, KYC/age status, jurisdiction, self-exclusion, limits, available sandbox credits, fixture/market state and idempotency before accepting a bet. Settlement must remain server-authoritative.

## Production gate
Do not enable cash deposits, withdrawals, cash wagering or redemption merely by changing this flag. Production requires the applicable licence, approved payment flow, KYC/AML controls, responsible-gambling controls, security review, auditability and regulator/payment-provider requirements.
