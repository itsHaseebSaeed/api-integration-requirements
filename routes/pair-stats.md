# Pair Stats

Information regarding trading pairs across supported DEXes with filtering options.

## Request

```http
GET /pair-stats HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

## Parameters

- `dex` (optional): Filter by DEX profile route (e.g. 'aevo', 'hyperliquid')
- `chain` (optional): Filter by chain name
- `base` (optional): Filter by base asset symbol
- `target` (optional): Filter by target/quote asset symbol
- `asset_type` (optional): Filter by asset type (e.g. 'crypto', 'commodities', 'rwa', 'equities', 'indices', 'forex', and 'other')
- `page` (optional, default=1): Pagination page number
- `limit` (optional, default=50): Number of results per page
- `sort_by` (optional, default='trading_volume_24h'): Field to sort by
- `sort_dir` (optional, default='desc'): Sort direction ('asc' or 'desc')

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
  ],
  "pagination": {
    "total": 150,
    "page": 1,
    "limit": 50,
    "pages": 3
  }
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

interface Pagination {
  total: number;
  page: number;
  limit: number;
  pages: number;
}

interface PairStatsResponse {
  pairs: PairStat[];
  pagination: Pagination;
}
```

## Get Single Pair Stats

Retrieve detailed information for a specific trading pair.

### Request

```http
GET /pair-stats/:id HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

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
  "asset_type": "perpetual",
  "trading_volume_24h": 1234567890,
  "open_interest": 987654321,
  "funding_rate": 0.0001,
  "max_leverage": 100,
  "percentage_change_24h": 2.5,
  "index_price": 63000,
  "trade_url": "https://app.aevo.xyz/BTC-USD",
  "last_updated": "2025-08-27T12:00:00Z",
  "historical_data": [
    {
      "timestamp": "2025-08-26T12:00:00Z",
      "trading_volume_24h": 1134567890,
      "open_interest": 887654321,
      "funding_rate": 0.00012
    }
  ]
}
```

### Response Type

```ts
interface HistoricalPairData {
  timestamp: string;
  trading_volume_24h: number;
  open_interest: number;
  funding_rate?: number;
}

interface SinglePairStatResponse extends PairStat {
  historical_data?: HistoricalPairData[];
}
```

## Get DEX Pairs

Retrieve pairs for a specific DEX.

### Request

```http
GET /dexes/:profileRoute/pairs HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

### Parameters

- `page` (optional, default=1): Pagination page number
- `limit` (optional, default=50): Number of results per page
- `sort_by` (optional, default='trading_volume_24h'): Field to sort by
- `sort_dir` (optional, default='desc'): Sort direction ('asc' or 'desc')

### Response

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
      "asset_type": "perpetual",
      "trading_volume_24h": 1234567890,
      "open_interest": 987654321,
      "funding_rate": 0.0001,
      "max_leverage": 100,
      "percentage_change_24h": 2.5,
      "index_price": 63000,
      "trade_url": "https://app.aevo.xyz/BTC-USD",
      "last_updated": "2025-08-27T12:00:00Z"
    }
  ],
  "pagination": {
    "total": 50,
    "page": 1,
    "limit": 50,
    "pages": 1
  }
}
```

### Response Type

```ts
interface DexPairsResponse {
  pairs: PairStat[];
  pagination: Pagination;
}
```

## Get Dex Summary

Retrieve aggregated statistics across all pairs.

### Request

```http
GET /dex/summary HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

### Parameters

- `dex` (optional): Filter by DEX profile route
- `chain` (optional): Filter by chain name
- `asset_type` (optional): Filter by asset type

### Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "total_pairs": 1250,
  "total_volume_24h": 25000000000,
  "total_open_interest": 15000000000,
  "volume_by_dex": [
    {
      "dex_id": "aevo",
      "dex_name": "Aevo",
      "volume_24h": 5000000000
    }
  ],
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
interface DexVolume {
  dex_id: string;
  dex_name: string;
  volume_24h: number;
}

interface AssetVolume {
  asset: string;
  volume_24h: number;
}

interface PairStatsSummaryResponse {
  total_pairs: number;
  total_volume_24h: number;
  total_open_interest: number;
  volume_by_dex: DexVolume[];
  volume_by_asset: AssetVolume[];
}
```
