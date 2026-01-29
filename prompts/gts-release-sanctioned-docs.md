# Prompt: SAP GTS release sanctioned documents

Generate a manual or automated test case for the SAP GTS Fiori app `Release Sanctioned Documents`.

## Inputs

- System URL:
- Client:
- User role:
- Sample sanctioned document ID:
- Target status:

## Expectations

- Verify list filtering for `Ready for Release`.
- Validate compliance results and document metadata sections.
- Release the document and confirm status change to `Released`.
- Confirm the document is removed from the `Ready for Release` list.
- Capture any release reason or audit trail entry.
