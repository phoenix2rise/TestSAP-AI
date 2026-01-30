# Test: SAP GTS release sanctioned documents

## Preconditions

- `config/gts-release-sanctioned-docs.example.yaml` is copied to `config/gts-release-sanctioned-docs.yaml` with valid credentials.
- A sanctioned document exists in status `Ready for Release`.

## Steps

1. Log in to SAP Fiori Launchpad as the Compliance Officer.
2. Open the `Release Sanctioned Documents` tile.
3. Filter the list by **Status = Ready for Release**.
4. Select the document matching the configured `sample_document_id`.
5. Open the object page and review the compliance results section.
6. Choose **Release** and confirm the action.
7. Return to the list and verify the document status is **Released**.
8. Confirm the document no longer appears in the `Ready for Release` filter results.

## Expected results

- The document status transitions to **Released**.
- A release confirmation message is displayed.
- Audit trail reflects the configured release reason (if applicable).
