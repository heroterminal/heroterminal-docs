# Introduction

Welcome to the HeroTerminal developer docs. HeroTerminal is **Mystery-as-Code**: noir investigations defined as text + assets in git, layered into the Lens filesystem at runtime.

Core terminology:
- **Case File** — the full investigation dossier (root directory, manifest, HeroCert).
- **Lead** — a chapter inside the case with its own brief, evidence, and completion checks.
- **Finding / File Report** — what the investigator submits to close a Lead.
- **Reputation** — the scoring unit awarded for clearing Leads.

What you’ll find here:
- How to author Case/Lead YAML.
- How the layered filesystem works (Investigator Home → Lead overlay on `~/desk` with drawer rollover).
- How validation and the APIs behave so you can keep the “forensic workstation” illusion intact.
