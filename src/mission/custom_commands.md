# Simulating Commands (`custom_commands`)

The `custom_commands` array lets you simulate bespoke binaries or scripts without writing real code. Each entry describes how the command behaves when the player runs it inside HeroOS.

```yaml
custom_commands:
  - command: "/opt/tools/heroscan"
    description: "Scans directories for IOC markers"
    actions:
      - emit:
          stdout: |
            [+] Scanning /srv
            [!] IOC matched: c2-beacon
      - set_exit_code:
          value: 0
```

## Supported Actions

| Action | Description |
| :--- | :--- |
| `emit` | Prints to `stdout` or `stderr`. |
| `set_exit_code` | Overrides the command's exit code. |
| `file_content` | Writes content to a file. Useful for dropping clues. |
| `file_exists` / `file_absent` | Can be set via environment block; combine with actions to simulate artifacts. |

Actions run in the order listed. Pair them to build rich behavior—emit output, mutate files, then set the exit code.

## Tips

- Use descriptive `command` paths (e.g., `/usr/bin/heroscan`).
- Keep output terse; players can always rerun the command.
- Record state changes with `file_content` so later solution checks can validate the mission.
