# The `herocert` Spec

Every bootcamp awards a HeroCert when all missions are completed. The `herocert` block in `bootcamp.yaml` controls how that certificate is rendered on app.heroterminal.com and in public share links.

| Key | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `title` | String | **Yes** | Display title for the certificate. Keep it short and inspirational. |
| `subtitle` | String | **Yes** | One sentence describing what the player achieved. |
| `description` | String | **Yes** | Longer blurb that appears on the certificate details page. Markdown allowed. |
| `default_sharing_text` | String | No | Text used when players share the certificate link on social media. |
| `svg` | Path | No | Optional path to a custom SVG badge inside the bootcamp directory (`herocert.svg`). |

## Example

```yaml
herocert:
  title: "Certified Threat Containment Specialist"
  subtitle: "Awarded for securing the HeroBank infrastructure."
  description: |
    You tracked the lateral movement, contained the breach, and restored
    services without losing customer data. HeroBank's SOC owes you a drink.
  default_sharing_text: "I just completed the HeroBank containment bootcamp!"
```

## Tips

- Keep titles under 60 characters.
- Use action verbs in `subtitle`/`description` so the accomplishment feels heroic.
- Provide a custom `herocert.svg` (200x200) if the standard badge does not fit your theme.
