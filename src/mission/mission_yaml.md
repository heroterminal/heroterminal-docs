# The `mission.yaml` File

Each file in the `missions/` directory defines a single challenge, its environment, and its solution.

| Key | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `key` | String | **Yes** | The unique key (filename) for the mission. |
| `title` | String | **Yes** | The display title for the mission. |
| `score` | Integer | **Yes** | The point value for this mission. See Scoring Rules. |
| `description` | String | **Yes** | The main mission briefing text (Markdown supported). |
| `environment` | Object | No | Defines the initial state of the filesystem. |
| `custom_commands` | Array | No | Simulates custom command behavior. See `custom_commands` spec. |
| `solution` | Object | **Yes** | Defines the conditions required to pass. See `solution` spec. |

## Example `01-containment.yaml`

```yaml
key: "01-containment"
title: "Mission 1: Contain the Threat"
score: 150

description: |
  A virus named 'herovirus' is active in `/bin/`.
  
  YOUR MISSION:
  Analyze the file *without* running it.
  Find the "killswitch" string and write it to `/tmp/answer.txt`

environment:
  initial_filesystem:
    "/bin/herovirus": |
      #!/bin/hsh
      # --- HERPESVIRUS 1.0 ---
      # ... (binary gibberish) ...
      # KILLSWITCH_PHRASE = "disable-alpha-9"
      # ... (more gibberish) ...

custom_commands:
  - command: "/bin/herovirus"
    description: "A dangerous binary file"
    actions:
      - emit:
          stderr: |
            [FATAL] VIRUS TRIGGERED.
            [FATAL] Deleting all files in /...
      - file_content:
          path: "/proc/system_compromised"
          content: "true"
      - set_exit_code:
          value: 1

solution:
  logic:
    all:
      - name: "Correct killswitch was written"
        file_contains:
          path: "/tmp/answer.txt"
          contains: "disable-alpha-9"
          
      - name: "Virus was not triggered"
        file_absent:
          path: "/proc/system_compromised"
```
