# Mission Submission (`submit` command)

All mission validations eventually call the `submit` handler. The command is sent through the WebSocket connection and mirrors the semantics of `POST /submit`.

Your client must provide:

- `hero_session` and `hero_user` cookies (cookies ride along with the WebSocket upgrade).
- The latest session token from `session_token` messages.
- The mission code as part of the `submit` command text.

Example payload sent to the server:

```json
{
  "type": "command",
  "data": "submit disable-alpha-9",
  "token": "6e9f9b19f2f34b87..."
}
```

Example terminal output on success:

```
HeroOS :: Mission accepted. 150 hero points awarded.
HeroOS :: Promotion unlocked. Loading next mission...
```

### Rate limiting

To discourage brute-force guessing we limit failed submissions per mission (per user and per IP). When the limit is exceeded the server responds with a rate-limit warning and ignores further submissions until the rolling window expires.

### HeroCerts

When the backend detects that you have completed every mission in a bootcamp it mints a HeroCert and prints the URL inside the terminal stream. You do not need an extra API call; the certificate endpoint is `/herocerts/:uuid` if you want to fetch it later.
