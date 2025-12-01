# Defining the Solution (`solution`)

The `solution` block defines what constitutes a "win". In Lens, submissions are validated directly against the text the investigator sends with the `submit` command.

```yaml
solution:
  logic:
    all:  # Can be 'all' (AND) or 'any' (OR)
      - name: "Container ID submitted"
        submission:
          contains: "LXRU-881203-7"
      - name: "Cargo reference submitted"
        submission:
          contains: "V12_ENGINE_BLUEPRINT"
```

## Check Types

- **`submission`**: Checks the investigator’s submitted text.
  - `equals`: optional exact match
  - `contains`: required substring
  - `regex`: optional regular expression

Combine `all`/`any` blocks to express complex requirements. Keep checks descriptive so Lead failure messages help investigators understand what remains.
