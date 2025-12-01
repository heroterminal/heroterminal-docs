# The `herocert` Spec

Every Case File awards a HeroCert when all Leads are completed. The `herocert` block in `case.yaml` controls how that certificate is rendered on app.heroterminal.com and in public share links.

| Key | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `title` | String | **Yes** | Display title for the certificate. Keep it short and inspirational. |
| `subtitle` | String | **Yes** | One sentence describing what the player achieved. |
| `description` | String | **Yes** | Longer blurb that appears on the certificate details page. Markdown allowed. |
| `default_sharing_text` | String | No | Text used when players share the certificate link on social media. |
| `svg` | Path | No | Optional path to a custom SVG badge inside the Case File directory (`herocert.svg`). |

## Example (The Dockyard Protocol)

```yaml
herocert:
  title: "Lyon Docks Investigator"
  subtitle: "Solved: The Dockyard Protocol"
  description: |
    Identified the ghost container, reconstructed the tampered manifests,
    uncovered fraudulent internal access, and attributed the manipulation
    to the responsible party.
  default_sharing_text: "I just closed The Dockyard Protocol in Lens."
```

## Tips

- Keep titles under 60 characters.
- Use action verbs in `subtitle`/`description` so the accomplishment feels heroic.
- Provide a custom `herocert.svg` (200x200) if the standard badge does not fit your theme.
