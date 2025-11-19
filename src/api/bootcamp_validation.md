# Bootcamp Validation (`POST /bootcamp/validate`)

Use this endpoint when you want to sanity-check a bootcamp archive before opening a pull request. It runs the same YAML parsing and scoring rules that production uses.

## Request

- **Method:** `POST`
- **URL:** `https://api.heroterminal.com/bootcamp/validate`
- **Auth:** none (rate-limited per IP)
- **Body:** `multipart/form-data` with one file input named `file`
  - Accepts `.tar.gz` / `.tgz` or `.zip` archives.
  - The archive root must contain the bootcamp directory (with `bootcamp.yaml`, `missions/`, etc.).

Example curl call:

```bash
curl -F "file=@detective-hero.tgz" \
  https://api.heroterminal.com/bootcamp/validate
```

## Response

On success the API returns HTTP 200 with a JSON summary:

```json
{
  "status": "ok",
  "bootcamps": [
    {
      "bootcamp_key": "detective-hero",
      "title": "Detective Hero",
      "missions": 5
    }
  ],
  "warnings": []
}
```

If the validator finds issues (missing missions, invalid YAML, scores outside 10–250, etc.) it responds with HTTP 400 and a descriptive error payload:

```json
{
  "status": "error",
  "message": "Mission 03-track-movement is referenced in mission_order but missing from missions/"
}
```

Fix the reported problems, regenerate the archive, and resubmit until you receive `status: ok`. This endpoint never mutates data; it only analyzes the uploaded archive.
