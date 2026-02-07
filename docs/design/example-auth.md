---
summary: "User authentication 設計"
read_when:
  - 實作認證功能
  - 修改登入/登出流程
---

# User Authentication

## Goals

- JWT-based 認證
- Refresh token rotation
- OAuth2 整合（Google）

## Non-goals

- 不做 multi-tenant
- 不做 passwordless login

## Decisions (locked)

- **Token storage:** Redis
- **Access token lifetime:** 15 分鐘
- **Password hashing:** bcrypt (cost 12)

## Key concepts

### Access Token
短期 JWT，15 分鐘過期。包含 user id 和 roles。

### Refresh Token
長期 token，存在 Redis。每次使用後 rotate。

## Implementation

1. JWT 生成和驗證
2. Login/Logout endpoints
3. Refresh token flow
4. OAuth integration

## Testing

- JWT 生成/驗證
- 完整 login flow
- Token rotation
