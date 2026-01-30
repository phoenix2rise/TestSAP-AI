# Playwright Automation Repository Improvements

This document is a practical checklist for strengthening a Playwright-based automation repo. It focuses on reliability, maintainability, and CI ergonomics with concrete, actionable recommendations.

## Repository Structure
- **Organize by feature and journey** (e.g., `tests/auth/`, `tests/billing/`) so tests map to product areas.
- **Keep helper code close** under `tests/helpers/` and `tests/fixtures/` to avoid a large, shared “utils” bucket.
- **Split fast vs. slow suites** (`tests/smoke/`, `tests/regression/`) so CI can run the right subset quickly.

Example layout:
```
tests/
  auth/
  billing/
  sap-fiori/
  smoke/
  fixtures/
  helpers/
```

## Fixtures & Test Data
- **Prefer Playwright fixtures** for user/session setup and API seeding to keep tests isolated.
- **Seed data via API** where possible and clean up on teardown to avoid cross-test coupling.
- **Tag tests that mutate data** to keep them off shared environments or run them in dedicated pipelines.

## Locator Strategy
- **Standardize on `data-testid` or ARIA roles** and avoid brittle CSS/XPath selectors.
- **Document selector patterns** in the README so every contributor follows the same approach.
- **Fail on ambiguous locators** by using strict mode and `getByRole` with `name`.

## SAP Fiori & Environment Notes (test.abc.com)
- **Treat `test.abc.com` as a shared SAP Fiori environment**: isolate tests that mutate data and run them in a dedicated pipeline or time window.
- **Prefer role-based selectors** in Fiori UIs (e.g., `getByRole("button", { name: "Save" })`) and add `data-testid` for custom controls when feasible.
- **Stabilize navigation** by waiting for shell and app readiness (e.g., wait for launchpad tile visibility and main content region).
- **Keep environment-specific config** (base URL, credentials, tenant/client) in `playwright.config` via env vars.

Example (launchpad navigation against `test.abc.com`):
```ts
import { test, expect } from "@playwright/test";

test("open Fiori app from launchpad", async ({ page }) => {
  await page.goto(process.env.BASE_URL ?? "https://test.abc.com");

  await expect(page.getByRole("region", { name: /launchpad/i })).toBeVisible();
  await page.getByRole("link", { name: "Manage Sales Orders" }).click();

  await expect(page.getByRole("main")).toBeVisible();
  await expect(page.getByRole("heading", { name: /sales orders/i })).toBeVisible();
});
```

## Reliability & Flake Reduction
- **Wait on expectations, not timeouts** (e.g., `await expect(locator).toBeVisible()`).
- **Use `expect.poll` for async backends** instead of fixed sleeps.
- **Enable retries only for flaky suites** and track recurring failures to fix root causes.
- **Gate on determinism**: keep a policy that prohibits `waitForTimeout` unless explicitly justified.

## Reporting & Debuggability
- **Collect trace/video/screenshot on failure** to speed up debugging in CI.
- **Use dual reporters** (HTML + JUnit) for local debugging and CI dashboards.
- **Upload artifacts** as build outputs for rapid triage.

Suggested config defaults (adapt to your repo):
```
use: {
  trace: "retain-on-failure",
  video: "retain-on-failure",
  screenshot: "only-on-failure",
}
```

## Configuration & Environments
- **Centralize env config** in `playwright.config` and validate required env vars early.
- **Use multiple projects** for browsers and devices; keep a minimal “smoke” project for speed.
- **Document local run commands** and required env vars in README.
- **Separate credentials per environment** (local/staging/prod) with least-privilege access.

## CI & Performance
- **Shard test suites** in CI to reduce wall-clock time.
- **Cache Playwright browsers** in CI to avoid repeated downloads.
- **Pin Playwright version** and update intentionally with a changelog review.
- **Enable parallelism** but keep workers within your environment’s stability limits.

## Code Quality
- **Lint TypeScript/JS** and enforce formatting for consistent reviews.
- **Keep helpers small and pure**; avoid cross-test state and global caches.
- **Add a test data strategy** (seeded data or API setup/teardown) and document ownership.
- **Prefer page objects for complex flows** while keeping simple tests inline to reduce indirection.

## Security & Secrets
- **Use CI secret stores** rather than committing credentials.
- **Avoid printing secrets** in test logs; scrub output where needed.

## Next Steps (Quick Wins)
1. Add a `README` section with local run instructions and debugging tips.
2. Add test tagging and a smoke suite with `@smoke` annotations.
3. Configure trace/video/screenshot capture on failure in `playwright.config`.
4. Review selectors and replace brittle ones with `data-testid` or role selectors.
