---
name: Create a contact and issue a quotation
description: Register a customer contact in FlowAccount, then create a quotation document for them.
api: openapi/flowaccount-openapi-original.json
operations: [Contact_Create, Contact_GetContactList, Quotation_Create]
---

# Create a contact and issue a quotation

Use this to onboard a new customer and send them their first quotation.

## Auth
- OAuth 2.0 client credentials. POST `grant_type=client_credentials`, `scope=flowaccount-api`
  with your `client_id`/`client_secret` to `{base}/token` (sandbox base
  `https://openapi.flowaccount.com/sandbox`).
- Send the returned token as `Authorization: Bearer <token>` on every call.
- Every path is prefixed with a `{culture}` segment (e.g. `en` or `th`).

## Steps
1. **Check for an existing contact** — `GET /api/{culture}/contacts` (`Contact_GetContactList`)
   or `GET /api/{culture}/contacts/search` to avoid duplicates.
2. **Create the contact** — `POST /api/{culture}/contacts` (`Contact_Create`) with the
   customer name, tax id, and address. Keep the returned contact id.
3. **Create the quotation** — `POST /{culture}/quotations/simple-document`
   (`Quotation_Create`) referencing the contact and the line items.

## Notes
- List endpoints page with `currentPage` + `pageSize`.
- The spec documents only 200 responses; treat non-200 HTTP status as failure and retry
  auth if the token expired.
