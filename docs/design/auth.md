---
summary: "User authentication 實作規格"
read_when:
  - 實作認證功能
  - 修改登入/登出流程
  - 新增 auth provider
  - 處理 token/session 相關問題
---

# User Authentication

## Goals

- 實作 JWT-based 認證
- 支援 refresh token rotation
- 整合 OAuth2 providers（Google, GitHub）

## Non-goals

- 不支援 multi-tenant（這個版本）
- 不做 passwordless login（之後考慮）
- 不改變現有 API contract

## Decisions (locked)

- **Token storage:** Redis（不用 in-memory）
- **Access token lifetime:** 15 分鐘
- **Refresh token lifetime:** 7 天
- **Password hashing:** bcrypt（cost factor 12）
- **OAuth flow:** Authorization Code + PKCE

## Key concepts

### Access Token

短期 JWT，包含 user id 和 roles。15 分鐘過期。

### Refresh Token

長期 opaque token，存在 Redis。用來換新的 access token。每次使用後 rotate。

### Session

一個 user 可以有多個 session（不同 device）。每個 session 有自己的 refresh token。

## Config surface

### 環境變數

- `JWT_SECRET` — JWT signing key（必須）
- `JWT_ISSUER` — Token issuer（預設：app name）
- `REDIS_URL` — Redis connection string
- `OAUTH_GOOGLE_CLIENT_ID` — Google OAuth client ID
- `OAUTH_GOOGLE_CLIENT_SECRET` — Google OAuth client secret

### 設定檔

```json
{
  "auth": {
    "accessTokenLifetimeMinutes": 15,
    "refreshTokenLifetimeDays": 7,
    "maxSessionsPerUser": 5
  }
}
```

## Implementation phases

### Phase 1: Basic JWT Auth

- [ ] JWT 生成和驗證
- [ ] Login endpoint
- [ ] Logout endpoint
- [ ] Auth middleware

### Phase 2: Refresh Token

- [ ] Refresh token 生成
- [ ] Token refresh endpoint
- [ ] Token rotation
- [ ] Session management

### Phase 3: OAuth Integration

- [ ] Google OAuth
- [ ] GitHub OAuth
- [ ] Account linking

## Data structures

### User

```typescript
interface User {
  id: string;
  email: string;
  passwordHash?: string;  // null for OAuth-only users
  roles: string[];
  createdAt: Date;
  updatedAt: Date;
}
```

### Session (Redis)

```
Key: session:{userId}:{sessionId}
Value: {
  refreshToken: string,
  deviceInfo: string,
  createdAt: number,
  lastUsedAt: number
}
TTL: 7 days
```

## API Endpoints

```
POST /auth/login
POST /auth/logout
POST /auth/refresh
GET  /auth/me
POST /auth/oauth/google
POST /auth/oauth/github
```

## Testing plan

- **Unit tests:**
  - JWT 生成/驗證
  - Password hashing
  - Token rotation logic

- **Integration tests:**
  - 完整 login flow
  - Refresh token flow
  - OAuth flow（mock provider）

- **Security tests:**
  - Expired token rejection
  - Invalid token rejection
  - Rate limiting

## Open risks

- **Redis 掛掉:** 所有 session 會失效。考慮加 fallback 或 circuit breaker。
- **Token 洩漏:** 需要實作 token revocation 機制。

## Related docs

- [API Documentation](/docs/api/auth.md)
- [Security Policy](/SECURITY.md)
