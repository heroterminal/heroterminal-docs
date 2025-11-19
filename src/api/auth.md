# Authentication

HeroOS uses the same GitHub OAuth flow for the app and the marketing site. You always start by creating an anonymous session and then optionally linking a GitHub account.

1. `GET /user/init`
   - Response sets `hero_session`.
   - Reuse this cookie for every API call and the WebSocket upgrade.
2. `GET /auth/github/login`
   - Redirects you to GitHub. Accepts an optional `return_url` so marketing pages can bounce back after login.
3. `GET /auth/github/callback`
   - Exchanges the OAuth code and sets `hero_user` (signed user ID).
4. `GET /auth/logout`
   - Clears both cookies.

Requests that modify state (starring bootcamps, submitting missions) only work when `hero_user` is present. Anonymous users can still open `/session`, but HeroCerts and points do not persist until they link GitHub.
