# The `bootcamp.yaml` File

The `bootcamp.yaml` file is the entry point for your entire bootcamp. It defines the metadata, the author, the certificate, and the order of the missions.

## File Structure

A bootcamp is a single directory in the `heroterminal-bootcamps` repo.

```
web-forensics/
├── bootcamp.yaml      <-- This file
├── herocert.svg       <-- (Optional) Custom badge
├── missions/
│   ├── 01-find-entrypoint.yaml
│   └── 02-analyze-payload.yaml
└── commands/
    └── (Optional) custom_command_files...
```

## `bootcamp.yaml` Specification

| Key | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `key` | String | **Yes** | A unique, kebab-case key for the bootcamp. Must match the folder name. |
| `title` | String | **Yes** | The official display title of the bootcamp. |
| `category` | String | **Yes** | The category (e.g., "Digital Forensics", "Incident Response"). |
| `description` | String | **Yes** | A short, compelling description for the bootcamp card. |
| `level` | String | **Yes** | The difficulty: `beginner`, `intermediate`, or `advanced`. |
| `author` | Object | **Yes** | See Author block below. |
| `mission_order` | Array | **Yes** | An ordered list of mission keys (the filenames in `missions/`). |
| `herocert` | Object | **Yes** | The certificate awarded for completion. See `herocert` Spec. |

### Author Block (`author:`)

```yaml
author:
  # (Required) The display name for the creator.
  name: "Hero Terminal"
  # (Required) The creator's GitHub username.
  github: "heroterm"
```

## Example `bootcamp.yaml`

```yaml
key: "webserver-forensics"
title: "Forensics: The Compromised Web Server"
category: "Digital Forensics"
description: "ALERT: Our main website has been defaced. Investigate the breach..."
level: "intermediate"

author:
  name: "Hero Terminal"
  github: "heroterm"

mission_order:
  - "01-find-entrypoint"
  - "02-analyze-payload"
  - "03-track-movement"

herocert:
  title: "Certified Web Forensics Investigator"
  subtitle: "Awarded for completing the Web Forensics Incident bootcamp."
  description: "Awarded for successfully analyzing a web server compromise..."
  default_sharing_text: "I just earned the 'Certified Web Forensics Investigator' cert..."
```
