# Abdullah Boshra — NEBU Integration Handoff

This build is integration-ready but does not invent any NEBU API details.

## What we need from NEBU
1. Official API / Web API documentation or integration manual.
2. Authentication method (API key, OAuth, VPN/private endpoint, etc.).
3. Read/write permissions for:
   - products
   - product codes / barcodes
   - karat
   - weight
   - stock quantity
   - sales / invoices
   - reservations (if supported)
   - customers (only where permitted)
   - price lists (if supported)
4. Sandbox/test environment and production endpoint.
5. Rate limits, webhook support, and error/retry rules.

## Proposed mapping
Website product code <-> NEBU product/barcode ID
Website stock <-> NEBU stock
Website order/reservation <-> NEBU order/sales workflow
Website prices <-> approved pricing source / NEBU price list

## Security
NEBU credentials must be stored only as server-side environment variables. Never place service credentials in browser JavaScript.

## Test plan
1. Read-only product sync.
2. Compare counts and a sample of codes/weights/karats.
3. Test stock changes from NEBU to website.
4. Test a website order in sandbox.
5. Verify idempotency (one order cannot create two NEBU sales).
6. Only after reconciliation: enable production write operations.
