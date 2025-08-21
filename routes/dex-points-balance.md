# DEX Points Balance (Optional)

Information regarding points balances for DEXs that have their own points system.

## Request

```http
GET /dex-points-balance HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

## Parameters

- `user_address` (required): The user's wallet address.

## Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "points": 100
}
```

## Response Type

```ts
interface DEXPointsBalanceResponse {
  points: number;
}
```
