---
name: Recommend items that optimize a goal with Aito
description: Rank items (products, actions, options) by how likely they are to achieve a defined goal for a given context.
api: openapi/aito-technologies-openapi-original.yml
operations: [recommend, search]
---

# Recommend items that optimize a goal with Aito

## Auth
- `x-api-key` header (read-only key works). Base URL `https://{instance}.aito.app/api/v1`.

## Steps
1. Identify the candidate field to recommend (e.g. `product`) and the goal you are optimizing (e.g. `{ "purchase": true }`).
2. Call `recommend` (`POST /api/v1/_recommend`) with:
   - `from`: the table of interactions/impressions
   - `where`: the context you are recommending for (e.g. the user)
   - `recommend`: the field to rank
   - `goal`: the outcome to optimize toward
   - optional `limit`: number of ranked recommendations
3. Return the ranked list; each item carries a score reflecting goal likelihood.

## Example
```json
POST /api/v1/_recommend
{ "from": "impressions",
  "where": { "context.user": "veronica" },
  "recommend": "product",
  "goal": { "purchase": true },
  "limit": 5 }
```

## Rules
- POST + `application/json`; 10MB payload cap; 30s timeout.
- Pagination is `offset`/`limit` inside the request body (default limit 10).
