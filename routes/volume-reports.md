# Volume Reports

Information regarding trading volume reports for wallet addresses.

## Request

```http
GET /volume-reports HTTP/1.1
Host: **.dexpal.ai
Authorization: Bearer <access_token>
```

## Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "reports": [
    {
      "wallet_address": "0x742d35Cc6634C0532925a3b844Bc9e7595f6E123",
      "date": "2025-07-30",
      "volume_usd": 150000.5,
      "fees_usd": 375.25,
      "transaction_count": 45,
      "metadata": {
        "pairs_traded": ["ETH/USDT", "BTC/USDT"],
        "exchange_user_id": "user123"
      }
    }
  ]
}
```

## Response Type

```ts
interface VolumeReport {
  wallet_address: string;
  date: string;
  volume_usd: number;
  fees_usd: number;
  transaction_count?: number;
  metadata?: Record<string, unknown>;
}

interface VolumeReportsResponse {
  reports: VolumeReport[];
}