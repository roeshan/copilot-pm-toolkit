# API Documentation – [API Name]

## Document Information
- **API Name:**
- **Version:** v1.0
- **Last Updated:**
- **Base URL:** `https://api.example.com/v1`
- **Status:** Draft / Published

---

## 1. Overview

### What This API Does
[Brief description of the API's purpose and capabilities]

### Key Features
- **Feature 1:** [e.g., RESTful design]
- **Feature 2:** [e.g., JSON responses]
- **Feature 3:** [e.g., OAuth 2.0 authentication]

### Use Cases
- **Use Case 1:** [Who uses this and why]
- **Use Case 2:** [Common integration scenario]

---

## 2. Getting Started

### Prerequisites
- API Key or OAuth credentials
- HTTPS-capable client
- JSON parser

### Quick Start

```bash
# Example: Get user information
curl -X GET "https://api.example.com/v1/users/123" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Response:**
```json
{
  "id": "123",
  "name": "John Doe",
  "email": "john@example.com",
  "created_at": "2026-01-15T10:30:00Z"
}
```

---

## 3. Authentication

### Authentication Methods

**Bearer Token (Recommended)**
```http
Authorization: Bearer YOUR_API_KEY
```

**API Key (Legacy)**
```http
X-API-Key: YOUR_API_KEY
```

### Getting an API Key

1. Log in to [Developer Portal](https://developer.example.com)
2. Navigate to "API Keys"
3. Click "Generate New Key"
4. Copy and securely store your key

### Token Lifecycle

- **Expiration:** Tokens expire after 24 hours
- **Refresh:** Use refresh token endpoint to get new token
- **Revocation:** Revoke via API or developer portal

---

## 4. Rate Limiting

### Limits

| Plan | Requests per Hour | Requests per Day |
|---|---|---|
| **Free** | 100 | 1,000 |
| **Basic** | 1,000 | 10,000 |
| **Pro** | 10,000 | 100,000 |
| **Enterprise** | Unlimited | Unlimited |

### Rate Limit Headers

```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```

### Handling Rate Limits

When rate limit exceeded:
```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Rate limit exceeded. Retry after 3600 seconds.",
    "retry_after": 3600
  }
}
```

**Recommended:** Implement exponential backoff when retrying.

---

## 5. API Endpoints

### Base URL
```
Production: https://api.example.com/v1
Staging:    https://staging-api.example.com/v1
```

---

### Users

#### Get User by ID
```http
GET /users/{user_id}
```

**Path Parameters:**
- `user_id` (string, required): Unique user identifier

**Headers:**
- `Authorization: Bearer {token}` (required)

**Response (200 OK):**
```json
{
  "id": "123",
  "name": "John Doe",
  "email": "john@example.com",
  "role": "admin",
  "created_at": "2026-01-15T10:30:00Z",
  "updated_at": "2026-01-20T14:45:00Z"
}
```

**Errors:**
- `404 Not Found`: User does not exist
- `401 Unauthorized`: Invalid or missing token

---

#### Create User
```http
POST /users
```

**Headers:**
- `Authorization: Bearer {token}` (required)
- `Content-Type: application/json` (required)

**Request Body:**
```json
{
  "name": "Jane Smith",
  "email": "jane@example.com",
  "role": "user"
}
```

**Response (201 Created):**
```json
{
  "id": "124",
  "name": "Jane Smith",
  "email": "jane@example.com",
  "role": "user",
  "created_at": "2026-04-06T10:00:00Z"
}
```

**Errors:**
- `400 Bad Request`: Invalid input (e.g., email already exists)
- `401 Unauthorized`: Invalid token

---

#### Update User
```http
PATCH /users/{user_id}
```

**Path Parameters:**
- `user_id` (string, required): User identifier

**Request Body:**
```json
{
  "name": "John Updated",
  "role": "admin"
}
```

**Response (200 OK):**
```json
{
  "id": "123",
  "name": "John Updated",
  "email": "john@example.com",
  "role": "admin",
  "updated_at": "2026-04-06T11:00:00Z"
}
```

---

#### Delete User
```http
DELETE /users/{user_id}
```

**Response (204 No Content)**

**Errors:**
- `404 Not Found`: User does not exist
- `403 Forbidden`: Not authorized to delete user

---

### Orders

#### List Orders
```http
GET /orders?user_id={user_id}&status={status}&limit={limit}&offset={offset}
```

**Query Parameters:**
- `user_id` (string, optional): Filter by user
- `status` (string, optional): Filter by status (pending, completed, cancelled)
- `limit` (integer, optional): Number of results (default: 20, max: 100)
- `offset` (integer, optional): Pagination offset (default: 0)

**Response (200 OK):**
```json
{
  "data": [
    {
      "id": "order_001",
      "user_id": "123",
      "status": "completed",
      "total_amount": 99.99,
      "created_at": "2026-04-01T10:00:00Z"
    }
  ],
  "pagination": {
    "total": 150,
    "limit": 20,
    "offset": 0,
    "has_more": true
  }
}
```

---

#### Create Order
```http
POST /orders
```

**Request Body:**
```json
{
  "user_id": "123",
  "items": [
    {
      "product_id": "prod_001",
      "quantity": 2,
      "price": 49.99
    }
  ],
  "shipping_address": {
    "street": "123 Main St",
    "city": "New York",
    "postal_code": "10001",
    "country": "US"
  }
}
```

**Response (201 Created):**
```json
{
  "id": "order_002",
  "user_id": "123",
  "status": "pending",
  "total_amount": 99.98,
  "created_at": "2026-04-06T12:00:00Z"
}
```

---

## 6. Data Schemas

### User Object
```json
{
  "id": "string (UUID)",
  "name": "string",
  "email": "string (email format)",
  "role": "string (enum: user, admin)",
  "created_at": "string (ISO 8601 datetime)",
  "updated_at": "string (ISO 8601 datetime)"
}
```

### Order Object
```json
{
  "id": "string (UUID)",
  "user_id": "string (UUID)",
  "status": "string (enum: pending, completed, cancelled)",
  "items": "array of OrderItem objects",
  "total_amount": "number (decimal)",
  "created_at": "string (ISO 8601 datetime)",
  "updated_at": "string (ISO 8601 datetime)"
}
```

### OrderItem Object
```json
{
  "product_id": "string (UUID)",
  "quantity": "integer (min: 1)",
  "price": "number (decimal)",
  "subtotal": "number (decimal)"
}
```

---

## 7. Error Handling

### Error Response Format

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      "field": "Additional context"
    }
  }
}
```

### HTTP Status Codes

| Code | Meaning | Usage |
|---|---|---|
| **200** | OK | Successful GET, PATCH, DELETE |
| **201** | Created | Successful POST (resource created) |
| **204** | No Content | Successful DELETE (no body) |
| **400** | Bad Request | Invalid input, validation error |
| **401** | Unauthorized | Missing or invalid authentication |
| **403** | Forbidden | Authenticated but not authorized |
| **404** | Not Found | Resource does not exist |
| **429** | Too Many Requests | Rate limit exceeded |
| **500** | Internal Server Error | Server-side error |
| **503** | Service Unavailable | Temporary outage |

### Common Error Codes

| Error Code | HTTP Status | Description |
|---|---|---|
| `INVALID_REQUEST` | 400 | Request body validation failed |
| `UNAUTHORIZED` | 401 | Invalid or expired token |
| `FORBIDDEN` | 403 | Insufficient permissions |
| `NOT_FOUND` | 404 | Resource not found |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests |
| `INTERNAL_ERROR` | 500 | Unexpected server error |

---

## 8. Pagination

### Standard Pagination

**Request:**
```http
GET /orders?limit=20&offset=0
```

**Response:**
```json
{
  "data": [...],
  "pagination": {
    "total": 150,
    "limit": 20,
    "offset": 0,
    "has_more": true
  }
}
```

### Cursor-Based Pagination (for large datasets)

**Request:**
```http
GET /events?limit=50&cursor=eyJpZCI6MTIzfQ==
```

**Response:**
```json
{
  "data": [...],
  "pagination": {
    "next_cursor": "eyJpZCI6MTczfQ==",
    "has_more": true
  }
}
```

---

## 9. Filtering & Sorting

### Filtering

**Single filter:**
```http
GET /users?role=admin
```

**Multiple filters:**
```http
GET /orders?status=completed&user_id=123
```

**Date range:**
```http
GET /orders?created_after=2026-01-01&created_before=2026-12-31
```

### Sorting

**Single field:**
```http
GET /users?sort=created_at
```

**Descending:**
```http
GET /users?sort=-created_at
```

**Multiple fields:**
```http
GET /orders?sort=created_at,-total_amount
```

---

## 10. Webhooks

### Registering Webhooks

```http
POST /webhooks
```

**Request Body:**
```json
{
  "url": "https://your-app.com/webhook",
  "events": ["order.created", "order.completed"],
  "secret": "your_webhook_secret"
}
```

### Webhook Events

| Event | Description |
|---|---|
| `order.created` | New order placed |
| `order.completed` | Order fulfilled |
| `order.cancelled` | Order cancelled |
| `user.created` | New user registered |
| `payment.successful` | Payment processed |

### Webhook Payload

```json
{
  "event": "order.created",
  "timestamp": "2026-04-06T12:00:00Z",
  "data": {
    "id": "order_002",
    "user_id": "123",
    "status": "pending",
    "total_amount": 99.98
  }
}
```

### Webhook Signature Verification

```python
import hmac
import hashlib

def verify_signature(payload, signature, secret):
    expected = hmac.new(
        secret.encode(),
        payload.encode(),
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(signature, expected)
```

---

## 11. SDKs & Client Libraries

### Official SDKs

**JavaScript/TypeScript:**
```bash
npm install @example/api-client
```

```javascript
import { ExampleAPI } from '@example/api-client';

const api = new ExampleAPI({ apiKey: 'YOUR_KEY' });
const user = await api.users.get('123');
```

**Python:**
```bash
pip install example-api-client
```

```python
from example_api import ExampleAPI

api = ExampleAPI(api_key='YOUR_KEY')
user = api.users.get('123')
```

**Community Libraries:**
- Ruby: [gem install example-api]
- PHP: [composer require example/api-client]
- Go: [go get github.com/example/api-go]

---

## 12. SLA & Service Guarantees

### Availability

| Metric | Target | Measurement |
|---|---|---|
| **Uptime** | 99.9% | Monthly uptime percentage |
| **Latency p95** | < 200ms | API response time |
| **Error Rate** | < 0.1% | Failed requests / total |

### Support SLA

| Plan | Response Time | Support Channels |
|---|---|---|
| **Free** | Best effort | Community forum |
| **Basic** | < 24 hours | Email |
| **Pro** | < 4 hours | Email, Chat |
| **Enterprise** | < 1 hour | Email, Chat, Phone |

---

## 13. Versioning

### Current Version: v1

**Base URL:** `https://api.example.com/v1`

### Deprecated Versions

- **v0 (Legacy):** Deprecated as of 2025-12-31, sunset on 2026-06-30
- Migration guide: [Link to migration docs]

### Breaking Changes Policy

- Major version changes for breaking changes
- 6-month deprecation notice
- Backwards compatibility within major version

---

## 14. Testing

### Sandbox Environment

**Base URL:** `https://sandbox-api.example.com/v1`

**Test Credentials:**
- API Key: `test_sk_1234567890abcdef`

**Test Data:**
- User ID: `test_user_001`
- Order ID: `test_order_001`

### Postman Collection

Import our Postman collection: [Download Link]

---

## 15. Best Practices

### Idempotency

Use idempotency keys for POST requests:
```http
POST /orders
Idempotency-Key: unique_key_123
```

### Caching

Respect cache headers:
```http
Cache-Control: max-age=3600
ETag: "abc123"
```

### Retry Logic

Implement exponential backoff:
```
1st retry: wait 1 second
2nd retry: wait 2 seconds
3rd retry: wait 4 seconds
Max retries: 3
```

### Security

- Always use HTTPS
- Never expose API keys in client-side code
- Rotate keys regularly
- Validate webhook signatures

---

## 16. Changelog

See [Release Notes](./release-notes-template.md) for API version history.

---

## 17. Support & Resources

- **Developer Portal:** [https://developer.example.com](https://developer.example.com)
- **API Status:** [https://status.example.com](https://status.example.com)
- **Support Email:** api-support@example.com
- **Community Forum:** [Link to forum]
- **GitHub Issues:** [Link to repo]

---

**Document Version:** 1.0  
**API Version:** v1  
**Last Updated:** [YYYY-MM-DD]
