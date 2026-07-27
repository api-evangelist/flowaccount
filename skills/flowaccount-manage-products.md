---
name: Manage products and inventory
description: Create and search FlowAccount products and adjust inventory levels.
api: openapi/flowaccount-openapi-original.json
operations: [Products_Create, Products_Search, Products_GetList, Products_Update, ProductInventory_Adjust]
---

# Manage products and inventory

Use this to maintain the product catalog that document line items reference.

## Auth
- OAuth 2.0 client credentials to `{base}/token` (`scope=flowaccount-api`); send
  `Authorization: Bearer <token>`. Paths are prefixed with `{culture}`.

## Steps
1. **Find existing products** — `Products_Search` or `Products_GetList` (pages with
   `currentPage` + `pageSize`) to avoid duplicates.
2. **Create a product** — `Products_Create` with name, SKU, price, and unit. Keep the id.
3. **Update a product** — `Products_Update` by id when price/details change.
4. **Adjust inventory** — `ProductInventory_Adjust` to set or correct stock quantity.

## Notes
- Product units and categories are managed separately (`ProductUnit_*`, `ProductCategory_*`).
- Retrieve a single product with `Products_GetById` before updating to preserve fields.
