# MFootball Stage 26 — Remote Sandbox Integration

Stage 26 connects the Android client to the Stage 25 Node.js/PostgreSQL sandbox contract.

## Safety

- `REAL_MONEY_BETTING_ENABLED` is hard-coded to `false` in both client and server.
- Currency is `TEST_CREDITS`.
- No real deposits, withdrawals, cash wagers or cash redemption are implemented.
- Production deployments should use HTTPS, a production secret manager, a managed PostgreSQL instance, and the required gambling/KYC/AML controls before any regulated-money functionality is considered.

## Run the sandbox backend

From `backend/`:

```bash
cp .env.example .env
npm install
npm start
```

Or use Docker Compose:

```bash
docker compose up --build
```

The API listens on port `3000` by default.

## Connect an Android phone

For a physical Android phone, change `Stage26Config.API_BASE_URL` to the reachable HTTPS/HTTP sandbox address, for example:

```text
http://192.168.1.20:3000
```

The phone and server must be reachable on the same network when using a local LAN address. `10.0.2.2` is for an Android emulator and normally does not point to your phone's host when running on a physical device.

## Cloud deployment

Deploy the `backend/` directory to a Node.js-compatible service and attach PostgreSQL. Set:

- `DATABASE_URL`
- `JWT_SECRET`
- `PORT`
- `TEST_CREDITS_START`

Use the resulting HTTPS URL as `Stage26Config.API_BASE_URL`.

## API integration

The Android client uses:

- `GET /health`
- `GET /api/v1/config`
- `POST /api/v1/auth/register`
- `POST /api/v1/auth/login`
- `GET /api/v1/wallet`
- `GET /api/v1/risk/profile`
- `GET /api/v1/bets`
- `POST /api/v1/bets`

Bet placement requires `Authorization: Bearer <JWT>` and an `Idempotency-Key` header.
