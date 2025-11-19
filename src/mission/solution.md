# Defining the Solution (`solution`)

The `solution` block defines what constitutes a "win". It is driven by logical checks.

```yaml
solution:
  logic:
    all:  # Can be 'all' (AND) or 'any' (OR)
      # Check 1
      - name: "A descriptive name for the check"
        file_contains:
          path: "/tmp/answer.txt"
          contains: "disable-alpha-9"
          
      # Check 2
      - name: "Virus was not triggered"
        file_absent:
          path: "/proc/system_compromised"

      # Check 3 (Nested logic)
      - any:
          - file_exists:
              path: "/tmp/fixed-a"
          - file_exists:
              path: "/tmp/fixed-b"
```

## Check Types

- **`file_contains`**: Checks if a file's content contains a string.
  - `path`, `contains`
- **`file_absent`**: Checks if a file or directory does not exist.
  - `path`
- **`file_exists`**: Checks if a file or directory does exist.
  - `path`
- **`command_exit`**: Checks if a specific command was run and returned a specific code.
  - `command`, `exit_code`

Combine `all`/`any` blocks to express complex requirements. Keep checks descriptive so mission failure messages help players understand what remains.
