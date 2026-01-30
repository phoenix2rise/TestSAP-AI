# SAP Fiori prerequisites

Before running automation against a SAP Fiori app, confirm the following:

- The SAP system is reachable from the test environment.
- A test user exists with the required roles and catalogs assigned.
- The Fiori Launchpad tile is visible to the test user.
- The app works in the target browser(s) without manual interventions.

## Recommended data setup

- Create stable master data sets for your key flows.
- Use dedicated test clients to avoid collisions with production.
- Document any nightly refresh or data cleanup jobs.
