# HeroTerminal Docs

This repository contains the official documentation for **HeroTerminal** and the **Lens** investigator interface.

It is the home for:

- The Case File (scenario) and Lead specification used by Lens
- Author guides for creating and testing new Case Files
- Reference docs for commands, environment behaviour and scoring
- Examples that show how to structure real Leads

If you want to build content for HeroTerminal, this is the place to start.

---

## Who is this for?

- Case authors who want to create new stories and investigation scenarios.
- Power users who want to understand how Lens behaves under the hood.
- Community contributors who want to improve clarity, fix typos or extend guides.

If you only want to play HeroTerminal, go to:

- App: https://app.heroterminal.com  
- Case Files repo: https://github.com/heroterminal/heroterminal-world

---

## Repository structure

The structure may evolve over time, but in general:

- `casefiles/`  
  Core Case File specification documents (scenario manifest, scoring, HeroCert).

- `leads/`  
  Lead specification (lead manifest, command simulation, solutions).

- `architecture/`  
  How Lens renders the filesystem and the Mystery-as-Code model.

- `tools/`  
  Validation helper scripts for packaging and checking Case Files.

Check the individual README files inside those folders for more detail if present.

---

## Contributing

We welcome improvements to the documentation.

Typical contributions include:

- Fixing typos or unclear wording.
- Improving examples.
- Adding small clarifications where behaviour was confusing.

Before opening a Pull Request, please read:

- [`CONTRIBUTING.md`](CONTRIBUTING.md)

---

## License

The documentation in this repository is licensed under:

**Creative Commons Attribution-NoDerivatives 4.0 International (CC BY-ND 4.0)**

You are free to:

- Read and share the documentation.
- Use it to create HeroTerminal Case Files and related content.

You may not:

- Distribute modified versions of this documentation as your own.
- Sell or commercially redistribute this documentation.

For the full legal text, see:  
https://creativecommons.org/licenses/by-nd/4.0/legalcode

© 2025 HeroTerminal.com. All rights reserved.
