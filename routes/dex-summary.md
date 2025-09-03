## Dex Summary

Retrieve aggregated statistics across all pairs.

### Request

```http
GET /dex/summary HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "total_pairs": 1250,
  "total_volume_24h": 25000000000,
  "total_open_interest": 15000000000,
  "volume_by_asset": [
    {
      "asset": "BTC",
      "volume_24h": 8000000000
    }
  ]
}
```

### Response Type

```ts
interface AssetVolume {
  asset: string;
  volume_24h: number;
}

interface PairStatsSummaryResponse {
  total_pairs: number;
  total_volume_24h: number;
  total_open_interest: number;
  volume_by_asset: AssetVolume[];
}
```
