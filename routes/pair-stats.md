# Pair Stats

Information regarding trading pairs across supported DEXes with filtering options.

## Request

```http
GET /pair-stats HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

## Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "pairs": [
    {
      "id": "12345",
      "dex_id": "aevo",
      "dex_name": "Aevo",
      "chain_id": "ethereum",
      "chain_name": "Ethereum",
      "base": "BTC",
      "target": "USD",
      "symbol": "BTC-USD",
      "canonical_base": "BTC",
      "canonical_target": "USD",
      "asset_type": "crypto", (e.g. 'crypto', 'commodities', 'rwa', 'equities', 'indices', 'forex', and 'other')
      "trading_volume_24h": 1234567890,
      "open_interest": 987654321,
      "funding_rate": 0.0001,
      "max_leverage": 100,
      "percentage_change_24h": 2.5,
      "index_price": 63000,
      "trade_url": "https://app.aevo.xyz/BTC-USD",
      "last_updated": "2025-08-27T12:00:00Z"
    }
  ]
}
```

## Response Type

```ts
interface PairStat {
  id: string;
  dex_id: string;
  dex_name: string;
  chain_id?: string;
  chain_name?: string;
  base: string; // 1000PEPE
  target: string; // USDT(ARB)
  symbol: string;
  canonical_base: string; //PEPE
  canonical_target: string; //USDT
  asset_type:
    | "crypto"
    | "commodities"
    | "rwa"
    | "equities"
    | "indices"
    | "forex"
    | "other";
  trading_volume_24h: number;
  open_interest: number;
  funding_rate?: number; // Hourly
  max_leverage?: number;
  percentage_change_24h?: number;
  index_price?: number;
  trade_url?: string;
  last_updated: string;
}

interface PairStatsResponse {
  pairs: PairStat[];
}
```
