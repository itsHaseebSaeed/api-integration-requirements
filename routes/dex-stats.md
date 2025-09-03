# DEX Stats

General information about your DEX for display on your profile page.

## Request

```http
GET /dex-stats HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

## Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "stats": {
    "trades": {
        "total": 900,
        "90d": 600,
        "30d": 200,
        "7d": 10,
        "24h": 4
    },
    "liquidations": {
        "total": 900,
        "90d": 600,
        "30d": 200,
        "7d": 10,
        "24h": 4
    },
    "active_wallets": {
        "total": 900,
        "90d": 600,
        "30d": 200,
        "7d": 10,
        "24h": 4
    },
  }
}
```

## Response Type

```ts
interface DEXStatsRange {
    total: number;
    "90d": number;
    "30d": number;
    "7d": number;
    "24h": number;
}

interface DEXStatsResponse {
  stats: {
    trades: DEXStatsRange;
    liquidations: DEXStatsRange;
    active_wallets: DEXStatsRange;
  };
}
```
