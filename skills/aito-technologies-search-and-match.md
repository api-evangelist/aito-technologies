---
name: Search and pattern-match rows with Aito
description: Filter rows with a where clause and find similar or matching records using Aito's search, similarity, and match operations.
api: openapi/aito-technologies-openapi-original.yml
operations: [search, similarity, match]
---

# Search and pattern-match rows with Aito

## Auth
- `x-api-key` header (read-only key works). Base URL `https://{instance}.aito.app/api/v1`.

## Steps
1. **Filter** with `search` (`POST /api/v1/_search`): supply `from` (table) and `where` (filter); page with `offset`/`limit`.
2. **Find similar** with `similarity` (`POST /api/v1/_similarity`): rank rows by distance to a reference proposition.
3. **Pattern-match** with `match` (`POST /api/v1/_match`): match rows against a partial proposition to fill or link records.

## Example
```json
POST /api/v1/_search
{ "from": "products", "where": { "id": "6411300000494" } }
```

## Rules
- All operations are POST + `application/json`; results paginate via `offset`/`limit` (default 10) in the body.
- 10MB payload cap; 30s query timeout; `400 Invalid request body` signals a malformed clause or bad table/column reference.
