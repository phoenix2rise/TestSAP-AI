# TestSAP-AI

TestSAP-AI is a starter repository for building AI-assisted test automation tailored to SAP Fiori applications. It mirrors the structure of TestAuto-AI with SAP-specific configuration, prompts, and documentation so teams can bootstrap Fiori test suites quickly and consistently.

## Goals

- Provide a predictable repository layout for SAP Fiori test automation.
- Separate configuration, prompts, and scripts so they can evolve independently.
- Offer templates and documentation for launchpad and app setup.

## Quick start

1. Copy `config/gts-release-sanctioned-docs.example.yaml` to `config/gts-release-sanctioned-docs.yaml` and fill in your SAP GTS system details.
2. Run the baseline test case in `tests/gts-release-sanctioned-docs.md` for the Release of sanctioned documents flow.
3. Review the prompts under `prompts/` to align with your testing standards.
4. Use the templates under `templates/` as a starting point for new test cases.

## Repository structure

- `config/` — SAP system, launchpad, and app configuration.
- `docs/` — SAP Fiori prerequisites, architecture notes, and contributing guidance.
- `prompts/` — AI prompt templates for test generation and reviews.
- `scripts/` — helper scripts for validation and automation.
- `templates/` — test case templates and checklists.
- `tests/` — place generated or handcrafted test cases here.

## Next steps

- Expand the SAP GTS flow details in `docs/gts-release-sanctioned-docs.md` as your process evolves.
- Add your test runner of choice (e.g., UI5, WebdriverIO, Playwright) to `scripts/`.
- Wire CI using your preferred pipeline configuration.
- Expand prompts and templates as you learn.
