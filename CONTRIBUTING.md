# Contributing

Thank you for helping improve this project.

## Before making a change

- Open an issue for substantial hardware, wiring, or register-map changes.
- Never commit Wi-Fi credentials, API keys, passwords, or private site details.
- Base technical claims on the manufacturer manuals or clearly label field-test
  observations.

## Workflow

1. Create a branch from `main`.
2. Make a focused change.
3. Validate `veris-8100.yaml` with a current ESPHome installation.
4. Check Markdown links and review changed images or PDFs.
5. Update `CHANGELOG.md` under `Unreleased`.
6. Open a pull request describing the hardware and meter variant tested.

## Documentation conventions

- Put component guidance in `docs/hardware/`.
- Put ESPHome and protocol guidance in `docs/software/`.
- Put editable CAD in `hardware/<part>/cad/`, printable exports in `exports/`,
  and drawings in `drawings/`.
- Put general images in `images/`.
- Use lowercase kebab-case names for new files.

## Safety

Do not present unverified mains wiring as tested guidance. Include the applicable
meter model, service type, and test conditions with field results.
