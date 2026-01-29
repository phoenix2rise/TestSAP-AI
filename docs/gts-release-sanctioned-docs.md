# SAP GTS release of sanctioned documents flow

This walkthrough provides a concrete, plug-and-play scenario for validating the SAP GTS flow that releases sanctioned documents. It is designed to serve as the baseline functional test for this repository.

## Business context

Organizations running SAP GTS need to release sanctioned trade documents once compliance checks are satisfied. The flow typically includes:

- Reviewing sanctioned document queues.
- Inspecting blocked items and compliance status.
- Releasing the sanctioned document once the business decision is made.

## Actors and roles

- **Compliance Officer**: reviews sanctioned documents and releases them.
- **Trade Compliance Supervisor** (optional): performs final approval.

## Prerequisites

- SAP GTS system accessible via Fiori Launchpad.
- Role/authorization for the `Release Sanctioned Documents` app.
- At least one sanctioned document in the queue with releasable status.

## Test flow summary

1. Log in to SAP Fiori Launchpad as the Compliance Officer.
2. Open `Release Sanctioned Documents` tile.
3. Filter the list by status = `Ready for Release`.
4. Open a sanctioned document detail page.
5. Review compliance results and document metadata.
6. Release the document and confirm status changes.
7. Validate the document no longer appears in the `Ready for Release` list.

## Data requirements

- Sample sanctioned document ID (e.g., `SDOC-100045`).
- Status transitions: `Ready for Release` -> `Released`.
- Optional: reason codes for audit trail validation.
