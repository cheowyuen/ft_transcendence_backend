# ft_transcendence_backend

# 🛠️ Backend Implementation Checklist (`ft_transcendence`)

## 1. Environment & Server Setup
- [ ] **.env Configuration:** Securely load secrets (`JWT_SECRET`, `DB_PASSWORD`, `PORT`) via environment variables.
- [ ] **HTTPS / WSS Enforcement:** Configure HTTPS/TLS certificates for encrypted REST endpoints and WebSocket connections.
- [ ] **CORS & Security Headers:** Configure CORS to restrict origin access to the React frontend; configure standard security headers.

## 2. Standard Authentication System
- [ ] `POST /api/auth/register` — Validate payload, hash password safely (Argon2 / bcrypt), and persist user in DB.
- [ ] `POST /api/auth/login` — Verify credentials against stored hash and issue an `httpOnly`, `Secure` JWT cookie/session token.
- [ ] `POST /api/auth/logout` — Invalidate session state and clear authentication cookies.

## 3. User & Profile Management
- [ ] `GET /api/users/me` — Retrieve logged-in user profile details (username, avatar path, global stats).
- [ ] `PUT /api/users/me` — Update editable profile information.
- [ ] `POST /api/users/me/avatar` — Handle image uploads (validate MIME type/file size, store on disk, update DB path).

## 4. Input Validation Middleware
- [ ] **Payload Sanitization:** Enforce strict validation schemas (e.g., using `Zod` or `Joi`) on all REST body payloads, URL params, and WebSocket messages before processing.

## 5. WebSockets & Game Session Management
- [ ] **WebSocket Server Instance:** Initialize real-time connection server (`ws` or `socket.io`).
- [ ] **Handshake Auth:** Authenticate incoming WebSocket connections using the HTTP session token/cookie.
- [ ] **Lobby & Room State:** Maintain active game rooms in server memory (tracking Room IDs, connected socket IDs, turn state).
- [ ] **Real-time Event Bridge:** Receive move events, run game engine validation, and broadcast updated board state to room clients.

## 6. Database Persistence
- [ ] **Match History Storage:** On match completion, persist final scores, winner/loser IDs, and timestamps to PostgreSQL.
- [ ] **User Stats Sync:** Atomically update cumulative player win/loss counts and match records.
