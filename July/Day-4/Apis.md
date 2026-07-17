# Auth API Reference — for Frontend

Base URL: `http://localhost:3000`

## 1. Register
**POST** `/auth/register`

Request body:
```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}
```

Response (200):
```json
{
  "user": {
    "id": "uuid-string",
    "email": "user@example.com",
    "role": "USER"
  },
  "accessToken": "eyJhbGc...",
  "refreshToken": "eyJhbGc..."
}
```

---

## 2. Login

**POST** `/auth/login`

Request body:
```json
{
  "email": "user@example.com",
  "password": "yourpassword"
}
```

Response: same shape as register (`user`, `accessToken`, `refreshToken`)

Error case: wrong email/password → `401 Unauthorized`

---

## 3. Get current user (protected route example)

**GET** `/auth/me`

Headers required:

Authorization : Bearer **< acessToken>**

Response (200):
```json
{
  "userId": "uuid-string",
  "email": "user@example.com",
  "role": "USER"
}
```

No token / invalid token → `401 Unauthorized`

---

## 4. Refresh access token
**POST** `/auth/refresh`

Headers required:
````

Authorization : Bearer **< refreshToken>**

```
(note: this uses the **refresh** token, not the access token)

Response (200): fresh `accessToken` + `refreshToken` — replace both in storage

---

## 5. Logout
**POST** `/auth/logout`

Headers required:
```

Authorization : Bearer **< acessToken>**

Response (200):
```json
{ "message": "Logged out successfully" }
```

Frontend should also clear the stored tokens on logout.

---

## Frontend flow summary
1. Register/Login → save `accessToken` + `refreshToken` (localStorage is fine for now)
2. Every protected request → attach `Authorization: Bearer <accessToken>` header
3. If a request fails with `401` (token expired) → call `/refresh` with the refresh token to get a new access token, then retry
4. On logout → call `/auth/logout`, then clear both tokens from storage

## CORS note

Backend needs to know your frontend's dev server port to allow requests — let me know what port your React app runs on (Vite default: `5173`, CRA default: `3000`) so I can whitelist it.
