# Lens Filesystem Architecture

Lens operates as a strict, proprietary sandbox environment. It defines its own structure and does not adhere to standard OS conventions.

## Directory Structure

The file system is a unified view constructed dynamically at runtime by merging layers directly into the **Workspace**.
The file system mounts everything into the top level (`/`).

* **/** (THE WORKSPACE) -> Contains investigator tools, personal files, and general case context.
* **/desk** -> Contains **Active Evidence** for the current lead.
* **/desk/drawer** -> Contains **Archived Evidence** from completed leads.

---

## Authoring Cheatsheet

**Put global investigator files here:**
`investigators/<id>/fs/**`
➡️ Ends up in `/` (Workspace)

**Put case-wide files here:**
`cases/<case>/fs/**`
➡️ Ends up in `/` (Workspace)

**Put lead-specific evidence here:**
`cases/<case>/fs/<lead-key>/**`
➡️ Ends up in `/desk/`

**Do NOT author anything into `/desk/drawer`**
➡️ Drawer is populated automatically when a lead completes.

**Overlay Precedence (highest wins):**
Lead Layer > Case Layer > Investigator Layer

---

## The 4-Layer Construction Logic

The virtual filesystem is built by stacking these layers in this specific order:

### 1. Investigator Layer (Base)
* **Source:** `investigators/<id>/fs/**`
* **Mount Point:** `/`
* **Purpose:** The investigator's personal tools and persistent files. These exist across all cases.
* **Usage Guidelines:**
    * Avoid referencing specific cases or dates in these files unless you are certain they won’t conflict with future cases (e.g., generic tools or evergreen personal notes).

### 2. Case Layer (Context)
* **Source:** `cases/<case_key>/fs/**` (Global files only)
* **Mount Point:** `/` (Merges into Workspace)
* **Purpose:** Files relevant to the active case timeline but not specific to a single lead.
* **Usage Guidelines:**
    * Use for case-specific background that should be visible during **every** lead of this case.
    * **Context:** A case represents a specific point in time for an investigator. Personal banter, emails, or recent events are highly encouraged here to add depth.
    * Ideal for:
        * Case briefings (PDFs/Text).
        * News articles (e.g., *Lyon Herald*) about the incident.
        * Personal notes written specifically during this investigation.
        * Personal emails or corporate correspondence.
        * Ephemeral items: Recent shopping lists, gym invoices, or calendar events relevant to that timeframe.

### 3. Lead Layer (The Desk)
* **Source:** `cases/<case_key>/fs/<lead_key>/**`
* **Mount Point:** `/desk/`
* **Purpose:** The immediate files and evidence required to solve the *current* objective.
* **Usage Guidelines:**
    * Use for evidence that must appear on the desk strictly when that lead is active.
    * **Note:** Assume the desk is empty at the start of a lead (except for what you explicitly place here).

### 4. Drawer Rollover (History)
* **Trigger:** When a lead is completed.
* **Action:** Everything currently in `/desk/` is moved to `/desk/drawer/<lead_key>/`.
* **Result:** The Desk is cleared for the next lead, but the player retains access to previous evidence in the drawer.
* **Usage Guidelines:**
    * **Do not author drawer content directly.**
    * The system handles the migration automatically upon lead completion.

---

## Comprehensive Merge Example: "The Dockyard Protocol"

**Current State:**
* **Investigator:** Luc Vernier (`lvernier`)
* **Active Case:** The Dockyard Protocol (`dockyard`)
* **Current Status:** Lead 1 ("Ghost Container") is **Complete**. Lead 2 ("Encrypted Signal") is **Active**.

### 1. The Source Layers (Backend Data)

* **Layer 1: Investigator (lvernier)**
    * `fs/tools/network_scanner.exe`
    * `fs/notes/luc_journal.md`

* **Layer 2: Case Overlay (dockyard)**
    * `fs/briefing/mission_brief.txt`
    * `fs/dossier/port_authority_map.img`

* **Layer 3: Active Lead (lead-02)**
    * `fs/signal_dump_raw.hex`
    * `fs/decryption_key.txt`

* **Layer 4: Drawer History (lead-01 completed)**
    * *Previous Desk Contents:* `shipping_manifest.csv`, `container_log.txt`

### 2. The Resulting Filesystem (What Luc Sees)

When the terminal loads, these layers merge into this exact structure:

```text
/ (THE WORKSPACE)
├── tools/
│   └── network_scanner.exe       <-- From Investigator Layer
├── notes/
│   └── luc_journal.md            <-- From Investigator Layer
├── briefing/
│   └── mission_brief.txt         <-- From Case Layer (Merged into Workspace)
├── dossier/
│   └── port_authority_map.img    <-- From Case Layer (Merged into Workspace)
└── desk/
    ├── signal_dump_raw.hex       <-- From Active Lead (Layer 3)
    ├── decryption_key.txt        <-- From Active Lead (Layer 3)
    └── drawer/
        └── lead-01/
            ├── shipping_manifest.csv  <-- From Drawer Rollover (Layer 4)
            ── container_log.txt      <-- From Drawer Rollover (Layer 4)

