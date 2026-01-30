# Architecture overview

TestSAP-AI keeps configuration, prompts, and templates separate so you can evolve each layer without affecting the others.

## Layers

1. **Configuration** (`config/`)
   - SAP system details
   - Launchpad navigation
   - Application routing hints

2. **Prompts** (`prompts/`)
   - Guidance for AI generation of test cases
   - Review checklists for Fiori UX and SAP-specific behaviors

3. **Templates** (`templates/`)
   - Repeatable test case skeletons
   - Scenario outlines for functional coverage

4. **Automation** (`scripts/`)
   - Validation or test runner wrappers (to be added)
   - CI helpers
