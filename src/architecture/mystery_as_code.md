# Mystery-as-Code

HeroTerminal treats every investigation as code. Content lives in git and is layered into Lens at runtime:

- **Investigators** (`investigators/<id>/home/**`): persistent personal files (music, inbox, notes).
- **Case Files** (`cases/<case-key>/case.yaml`): metadata, leads, reputation, briefing, hero cert text.
- **Lead Assets** (`cases/<case-key>/fs/lead-XX/**`): evidence for a single lead. These are mounted onto `~/desk/` for the active lead.

Why this matters:
- **Deterministic**: same repo -> same workstation state; easy to diff and review.
- **Auditable**: everything versioned; no hidden database data.
- **Composable**: investigator home + case + lead overlay -> single sandbox for Lens.

Content authors change YAML and files, then redeploy. No database migrations required for story data.
