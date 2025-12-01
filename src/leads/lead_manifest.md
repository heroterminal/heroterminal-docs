# The `lead.yaml` Manifest

Each file in the `leads/` directory defines a single Lead, its environment, and its solution.

| Key | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `key` | String | **Yes** | The unique key (filename) for the Lead. |
| `title` | String | **Yes** | The display title for the Lead. |
| `reputation` | Integer | **Yes** | Reputation awarded for this Lead. See Scoring Rules. |
| `briefing` | String | **Yes** | The Lead briefing text (Markdown supported). |
| `environment` | Object | No | Defines the initial state of the filesystem (desk overlay). |
| `solution` | Object | **Yes** | Defines the conditions required to pass. See `solution` spec. |

## Example `lead-01.yaml`

```yaml
key: "lead-01"
title: "The Ghost Container"
reputation: 50

briefing: |
  The port registry shows a gap in the container sequence. One container is physically present on the dock, but its manifest entry is missing.

  Your focus:
  - Open the manifest export and registry logs on your desk.
  - Find the container that "should not exist."
  - Submit the container ID and the declared cargo reference.

environment:
  initial_filesystem:
    "/desk/logs/manifest_export.csv": |
      # ...redacted sample data...
    "/desk/logs/registry.log": |
      # ...redacted sample data...

solution:
  logic:
    all:
      - name: "Container ID submitted"
        submission:
          contains: "LXRU-881203-7"
      - name: "Cargo reference submitted"
        submission:
          contains: "V12_ENGINE_BLUEPRINT"
```
