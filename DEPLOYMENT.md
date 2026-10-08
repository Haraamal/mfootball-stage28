# MFootball Deployment Package

Merged Android source through Stage 16.

## Build
Open this folder in Android Studio, sync Gradle, then use Build > Generate Signed App Bundle / APK.

## Before production
1. Configure the production API URL in ApiConfig.kt.
2. Deploy the Node.js/PostgreSQL backend and apply database migrations in order.
3. Configure HTTPS, authentication, logging, backups and monitoring.
4. Configure Play App Signing.
5. Complete privacy policy, terms, age restrictions and required regulatory compliance.
6. Keep real-money wagering, deposits, withdrawals and cash redemption disabled until all required licensing and payment-provider approvals are in place.
