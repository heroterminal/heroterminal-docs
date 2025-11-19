# Bootcamp Validation Helper

HeroTerminal does not ship a standalone CLI. Instead, we provide a Python script (`validate.py`) that packages your bootcamp directory and calls the `/bootcamp/validate` API endpoint. This mirrors the exact validation pipeline we run in production.

## Requirements

- Python 3.8+
- `requests` (`pip install requests`)
- Access to the HeroTerminal API (default endpoint: `https://api.heroterminal.com/bootcamp/validate`)

## Usage

```bash
python3 validate.py path/to/detective-hero \
  --endpoint https://api.heroterminal.com/bootcamp/validate
```

The script will:

1. Tar+gzip your bootcamp directory (including `bootcamp.yaml`, `missions/`, etc.).
2. POST the archive to `/bootcamp/validate`.
3. Print a summary of parsed bootcamps and mission counts, or any syntax errors.

Sample output:

```
Validation success:
  - Detective Hero (detective-hero) :: 5 missions
```

If the API detects a problem (missing mission, score outside 10–250, malformed YAML), it returns HTTP 400 with a descriptive message. Fix the reported issue locally, rerun the script, and only open a pull request once the validator passes.

## Manual curl alternative

Prefer not to run the script? You can call the endpoint directly:

```bash
curl -F "file=@detective-hero.tar.gz" https://api.heroterminal.com/bootcamp/validate
```

This is the same request that `validate.py` performs under the hood.
