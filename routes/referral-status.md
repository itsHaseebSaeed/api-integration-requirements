# Referral Status

Information regarding the referral status of a user.

## Request

```http
GET /referral-status HTTP/1.1
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
  "is_active": true
}
```

## Response Type

```ts
interface ReferralStatusResponse {
  is_active: boolean;
}
```
