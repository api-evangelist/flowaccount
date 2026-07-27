---
name: Record a cash sale and receive payment
description: Create a FlowAccount cash invoice (sales receipt) and record the payment against it.
api: openapi/flowaccount-openapi-original.json
operations: [CashInvoice_Create, CashInvoice_ReceivePayment, CashInvoice_ChangeStatusByKey]
---

# Record a cash sale and receive payment

Use this to capture an over-the-counter / POS cash sale and mark it paid.

## Auth
- OAuth 2.0 client credentials to `{base}/token` (`scope=flowaccount-api`); send
  `Authorization: Bearer <token>`. Paths are prefixed with `{culture}`.

## Steps
1. **Create the cash invoice** — `POST /{culture}/cash-invoices/simple-document`
   (`CashInvoice_Create`) with buyer, items, and totals. Keep the returned document id.
2. **Receive the payment** — `POST /{culture}/cash-invoices/{id}/payments`
   (`CashInvoice_ReceivePayment`) with the amount and payment method.
3. **(Optional) Update status** — `POST /{culture}/cash-invoices/{documentId}/status-key/{statusKey}`
   (`CashInvoice_ChangeStatusByKey`) to move the document through its lifecycle.

## Notes
- Verify amounts against the created document before posting payment.
- The same create/payment/status pattern applies to quotations, receipts, tax invoices,
  and receivable invoices (`*_Create`, `*_ReceivePayment`, `*_ChangeStatusByKey`).
