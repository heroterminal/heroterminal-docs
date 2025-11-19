# API Overview

HeroTerminal exposes an HTTP+WebSocket API that matches the backend used by the in-browser terminal.

All public clients should talk to `https://api.heroterminal.com`.

All endpoints speak JSON and assume your client stores two cookies:

- `hero_session`: anonymous session cookie minted by `GET /user/init`.
- `hero_user`: signed GitHub identity cookie set after OAuth.

The public surface currently includes:

- `GET /session` (WebSocket): streams terminal output/input.
- `POST /submit`: validates the current mission solution.
- `POST /bootcamp/validate`: optional helper that checks bootcamp archives.

The rest of the API docs dive into `/session` and `/submit`. For completeness, here is the bootcamp validation endpoint that authors use before opening a pull request:

```http
POST /bootcamp/validate HTTP/1.1
Host: api.heroterminal.com
Content-Type: multipart/form-data

file=@detective-hero.tar.gz
```

Successful responses include a list of detected bootcamps and mission counts:

```json
{
  "status": "ok",
  "missions": 5,
  "bootcamps": [
    {
      "bootcamp_key": "detective-hero",
      "title": "Detective Hero",
      "missions": 5
    }
  ]
}
```

This endpoint doesn’t require authentication and is rate-limited per IP. It runs the exact same YAML validation as production.
