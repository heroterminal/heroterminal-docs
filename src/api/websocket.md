# WebSocket Session (`/session`)

Every HeroOS mission lives inside a WebSocket. Clients connect, send terminal text, and receive output lines, mission metadata, and session tokens.

## Connecting

```
GET /session?mission_key=detective-hero-01 HTTP/1.1
Host: api.heroterminal.com
Upgrade: websocket
Cookie: hero_session=...; hero_user=...
```

Query parameters:
- `mission_key` or `task_key`: optional explicit mission slug. If omitted we pick a random bootcamp.
- `nickname`: optional alias used in the terminal greeting.

## Messages from the server

- `output` / `output_block` / `output_inline`: terminal text.
- `mission_info`: JSON snapshot describing the current mission.
- `score_update`: new total score after a mission completes.
- `session_token`: the challenge token required for the next `submit` command.

Example `session_token` payload:

```json
{
  "type": "session_token",
  "token": "6e9f9b19f2f34b87..."
}
```

Tokens expire quickly. Store the most recent value and send it with the next mission submission.

## Messages to the server

The terminal sends JSON objects with a `type` field. For example:

```json
{ "type": "command", "data": "ls -lha" }
```

To submit a mission the client sends:

```json
{
  "type": "command",
  "data": "submit disable-alpha-9",
  "token": "6e9f9b19f2f34b87..."
}
```

If the token is missing or expired the server responds with an error and immediately emits a fresh `session_token` message. When the token is valid the `/submit` handler executes and, if successful, the terminal prints the promotion text and (when applicable) the HeroCert link.
