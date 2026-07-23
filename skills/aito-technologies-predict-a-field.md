---
name: Predict a field value with Aito
description: Use the Aito predictive database to predict the most likely value of a field given known context.
api: openapi/aito-technologies-openapi-original.yml
operations: [predict, search]
---

# Predict a field value with Aito

Aito returns calibrated probabilities for a target field given whatever context you know, without any model training.

## Auth
- Send the `x-api-key` header on every request (read-only key is sufficient for `_predict`).
- Base URL is your instance: `https://{instance}.aito.app/api/v1` (public demo: `https://shared.aito.ai/db/aito-demo/api/v1`).

## Steps
1. (Optional) Confirm the table and fields exist by running `search` (`POST /api/v1/_search`) with a small `where` and `limit`.
2. Call `predict` (`POST /api/v1/_predict`) with:
   - `from`: the table to learn from
   - `where`: the known context (feature values you have)
   - `predict`: the field whose value you want
   - optional `limit`: number of ranked hypotheses to return (default 10)
3. Read the ranked results — each hypothesis carries a probability (`$p`) score; pick the top hypothesis, or route low-confidence results (below your threshold) to a human.

## Example
```json
POST /api/v1/_predict
{ "from": "impressions",
  "where": { "context.user": "larry", "product.id": "6410405216120" },
  "predict": "purchase" }
```

## Rules
- POST + `application/json`; payload cap 10MB; query timeout 30s (see conventions/aito-technologies-conventions.yml).
- On a `400 Invalid request body`, check the table/column names and clause shape (errors/aito-technologies-problem-types.yml).
