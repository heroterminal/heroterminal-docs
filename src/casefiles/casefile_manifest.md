# The `case.yaml` Manifest

The Case File manifest (`case.yaml`) is the entry point for your investigation. It defines the metadata, the author, the case briefing, and the Leads an investigator will work through.

## File Structure

A Case File is a single directory in the Case Files repository.

```
2025-lvernier-the-dockyard-protocol/
├── case.yaml           <-- This file
├── herocert.svg        <-- (Optional) Custom badge
├── fs/                 <-- Filesystem overlay (desk)
└── leads/
    ├── lead-01.yaml
    ├── lead-02.yaml
    └── lead-03.yaml
```

## `case.yaml` Specification

| Key | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `key` | String | **Yes** | A unique, kebab-case key for the Case File. Must match the folder name. |
| `title` | String | **Yes** | The official display title of the Case File. |
| `difficulty` | String | **Yes** | The difficulty: `beginner`, `intermediate`, or `advanced`. |
| `investigator` | String | **Yes** | The investigator persona leading the case (e.g., `lvernier`). |
| `summary` | String | **Yes** | A short, compelling summary for cards and overviews. |
| `author` | Object | **Yes** | See Author block below. |
| `briefing` | String | **Yes** | Narrative briefing shown before Leads begin. Markdown supported. |
| `leads` | Array | **Yes** | Ordered list of Lead objects (see Lead manifest for per-lead fields). |
| `herocert` | Object | **Yes** | The certificate awarded for completion. See `herocert` Spec. |

### Author Block (`author:`)

```yaml
author:
  # (Required) The display name for the creator.
  name: "Hero Terminal"
  # (Required) The creator's GitHub username.
  github: "heroterm"
```

## Example `case.yaml` (from The Dockyard Protocol)

```yaml
key: "2025-lvernier-dockyard-protocol"
title: "The Dockyard Protocol"
difficulty: "beginner"
investigator: "lvernier"
summary: "A ghost shipping container appears in Lyon with no manifest and a suspicious hum. Find out what is inside and who hid it."

author:
  name: "HeroTerminal team"
  github: "heroterminal"

briefing: |
  LOCATION: Port Édouard Herriot, Lyon
  SOURCE: Antoine Besson (Private Security)
  HANDLER: Claire Vernier
  A 40-foot shipping container exists physically but not in the registry. Pull the data dump and find who hid it.

leads:
  - key: "lead-01"
    title: "The Ghost Container"
    reputation: 50
    briefing: "Find the missing container ID and its declared cargo."
    solution:
      logic:
        all:
          - submission:
              contains: "LXRU-881203-7"
          - submission:
              contains: "V12_ENGINE_BLUEPRINT"
  - key: "lead-02"
    title: "The Access Trail"
    reputation: 50
    briefing: "Correlate badge access with RFID reads to find the abused badge."
    solution:
      logic:
        any:
          - submission: { contains: "AC-221" }
          - submission: { contains: "Marc Duret" }

herocert:
  title: "Lyon Docks Investigator"
  subtitle: "Solved: The Dockyard Protocol"
  description: "Identified the ghost container, traced the access trail, and exposed the insider."
```
