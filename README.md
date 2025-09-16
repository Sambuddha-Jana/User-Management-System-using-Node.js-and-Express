# User-Management-System-using-Node.js-and-Express
A RESTful project management backend built with Node.js, Express and MongoDB. Includes JWT access/refresh token auth, email verification, password reset, and role-based user management.


Quick features

Register / login / logout
JWT access + refresh token flow (cookies & Authorization header)
Email verification and password reset (tested with Mailtrap)
Profile management and simple admin user management
Input validation and centralized error handling
Prerequisites (what a developer needs)

Node.js (recent LTS)
npm
MongoDB connection (Atlas or local)
Mailtrap account for email testing (optional)
Postman for API testing (optional but recommended)
Setup (high-level)

Install dependencies with npm
Copy .env.example → .env and fill values (do not commit .env)
Start server in dev mode (auto-reload) or run production start
Important environment variables (placeholders only)

MONGO_URI — MongoDB connection string
PORT — server port (e.g. 8000)
CORS_ORIGIN — allowed origins
ACCESS_TOKEN_SECRET, ACCESS_TOKEN_EXPIRY
REFRESH_TOKEN_SECRET, REFRESH_TOKEN_EXPIRY
MAIL SMTP credentials for Mailtrap (or other SMTP provider)
Testing notes

Use Postman to exercise endpoints; import your Postman collection if available
Mailtrap captures verification and reset emails — configure SMTP creds in .env
Use MongoDB Atlas UI / Compass to inspect data
Main API endpoints (short)

POST /api/v1/auth/register — register user
POST /api/v1/auth/login — login (returns tokens; sets cookies)
POST /api/v1/auth/logout — logout (revokes refresh)
GET /api/v1/auth/current-user — protected: returns logged-in user
POST /api/v1/auth/refresh-token — refresh access token
POST /api/v1/auth/forgot-password — request reset
POST /api/v1/auth/reset-password — reset with token
GET /api/v1/auth/verify-email/:token — verify email
Admin/testing: DELETE /api/v1/auth/delete-user, DELETE /api/v1/auth/delete-all (remove when shipping)
Common troubleshooting

Server won’t start → check .env and MONGO_URI
401 on current-user → ensure a valid access token (header or cookie) and that ACCESS_TOKEN_SECRET matches
No emails in Mailtrap → check SMTP creds in .env and Mailtrap inbox
Security reminders

Never commit .env. Add .env to .gitignore.
Rotate secrets immediately if a secret is accidentally published.
Use HTTPS in production; set cookie secure and sameSite appropriately.
Keep access tokens short-lived; refresh tokens revocable server-side.
Contributor & workflow notes

Fork → branch → PR
Run lint/format before PR (Prettier is configured)
Add tests for new features (Jest + Supertest recommended)
