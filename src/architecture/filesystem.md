# Lens Filesystem Architecture

Lens builds a virtual filesystem by stacking authored layers. The player only sees a single Workspace, but behind the scenes Investigator, Case, and Lead assets are overlaid with strict precedence.

## Asset Hierarchy (what belongs where?)

- **Investigator Assets (Inventory):** Old Luc personal belongings (e.g., Personal notes, Old emails, shopping lists). Lives in `investigators/<id>/fs/**`.
- **Case Assets (Starting Desk):** Files Claire/Sylvie send at the start (maps, background briefs, manuals). Lives in `cases/<case>/fs/**`.
- **Lead Assets (Evidence):** Items discovered while solving a lead (scent strip, copper flask, chemical vial). Lives in `cases/<case>/fs/<lead-key>/**` and only appear when that lead is active.

## Directory Layout at Runtime

- `/` — Workspace (merged Investigator + Case layers).
- `/desk/` — Active Lead evidence.
- `/desk/drawer/` — Archived evidence from completed leads.

## Authoring Rules

- Put global investigator files in `investigators/<id>/fs/**` → becomes `/...`.
- Put case-wide files in `cases/<case>/fs/**` → becomes `/...` (you can place them under a subfolder like `/desk/` if you want them on the desk from the start of every lead).
- Put lead-specific files in `cases/<case>/fs/<lead-key>/**` → becomes `/desk/...` while that lead is active.
- Do **not** author anything into `/desk/drawer`; rollover is automatic.

## Overlay Precedence (highest wins)

`Lead Layer > Case Layer > Investigator Layer`

If two layers define the same path, the active lead file wins, then case, then investigator.

## Desk Lifecycle

1. Start of a lead: `/desk/` is populated with the active lead’s assets plus any case files you placed under `/desk/`.
2. Complete a lead: everything in `/desk/` is moved to `/desk/drawer/<lead-key>/`.
3. Next lead starts with a fresh `/desk/`, but the drawer keeps history.

## Example: “The Midnight Harvest”

**State:** Investigator `lvernier`; active case `2025-lvernier-the-midnight-harvest`; Lead 1 solved, Lead 2 active.

**Authored sources**
- Investigator: `fs/playlist/blues.m3u`, `fs/personal/elise/2023_incident_galeries.eml`
- Case (global): `fs/desk/map_grasse_valley.svg`, `fs/desk/clipping_lyon_herald.svg`, `fs/desk/doc_lab_codes.md`, `fs/desk/manual_refractometry.md`, `fs/desk/dossier_helene_vasseur.txt`
- Lead 02: `fs/lead-02/tool_refractometer_view.svg`
- Lead 01 (completed, rolled into drawer): `fs/lead-01/evidence_mouillette_strip.svg`, `fs/lead-01/log_visual_inspection.txt`

**What Luc sees**

```text
/ (Workspace)
├── playlist/
│   ├── blues.m3u                      <-- Investigator
├── personal/elise/
│   └── 2023_incident_galeries.eml     <-- Investigator
└── desk/
    ├── map_grasse_valley.svg          <-- Case asset (available every lead)
    ├── clipping_lyon_herald.svg       <-- Case asset
    ├── doc_lab_codes.md               <-- Case asset
    ├── manual_refractometry.md        <-- Case asset
    ├── dossier_helene_vasseur.txt     <-- Case asset
    ├── tool_refractometer_view.svg    <-- Active lead-02 evidence
    └── drawer/
        └── lead-01/
            ├── evidence_mouillette_strip.svg  <-- Archived after lead-01
            └── log_visual_inspection.txt      <-- Archived after lead-01
```

Use this pattern for future cases: keep evergreen gear in the investigator layer, ship onboarding materials in the case layer, and drop clue-by-clue evidence into each lead. The overlay will do the rest.
