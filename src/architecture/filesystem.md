# Lens Filesystem (Layered)

Lens always sandboxes the player to the active investigator’s home (e.g., `/home/lvernier`). Three layers are merged, in order:

1) **Investigator Home** — long-lived personal files  
   - Source: `investigators/<id>/home/**`  
   - Mount: `~/`  
   - Example: `~/personal/elise/2023_incident_galeries.eml`

2) **Lead Overlay** — evidence for the current lead  
   - Source: `cases/<case>/fs/<lead-key>/**`  
   - Mount: `~/desk/` (files appear on the desk)  
   - Example: `~/desk/dock_manifest_export.csv`

3) **Drawer Rollover** — previous lead artifacts  
   - When a lead completes, everything on `~/desk/` is moved to `~/desk/drawer/<lead-key>/`.  
   - New lead assets are then placed on a clean `~/desk/`.

Path rules:
- `~` and `$HOME` both point to `/home/<investigator-id>`.
- Lens never allows navigation above the investigator home.
- Default tabs: `Desk → ~/desk`, `Home → ~/`.

Example progression (investigator `lvernier`, case `dockyard`):
- **Lead 1**: desk has `dock_manifest_export.csv`, `container_registry.log`.
- **Lead 2**: those files roll into `~/desk/drawer/lead-01/`; desk now has `cctv_index_A3.txt`, `dockyard_badge_access.log`, `rfid_reader_A3_dump.txt`.
- **Lead 3**: drawer holds all prior leads; desk has `shift_schedule.json`, `employee_roster.csv`, `maintenance_requests.log`.
