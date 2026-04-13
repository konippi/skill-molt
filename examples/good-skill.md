# Good Skill Example

This is an example of a well-written skill extracted from a real coding session.

## The Skill

```markdown
---
name: e2e-testing
description: >-
  Use when running end-to-end tests, setting up test environments, or
  debugging test failures in this project. Handles Docker prerequisites,
  database seeding, and test isolation. Do NOT use for unit tests or
  component tests.
---

# E2E Testing

## Workflow

1. Verify Docker is running: `docker info > /dev/null 2>&1`
   - If Docker is not running → start it and wait 10 seconds
2. Start the test database: `docker compose up -d test-db`
3. Set the environment: `export DATABASE_URL=postgresql://test:test@localhost:5433/testdb`
4. Run migrations: `pnpm db:migrate`
5. Seed test data: `pnpm db:seed --env test`
6. Run tests: `pnpm test:e2e`
   - If tests hang for >60 seconds → Docker likely crashed. Run `docker compose logs test-db`
7. Tear down: `docker compose down -v`

## Rules

- Always use port 5433 for test DB (5432 is the dev DB)
- Never run e2e tests against the dev database — seed data will corrupt it
- The `--env test` flag on seed is required — without it, seed uses production fixtures

## Gotchas

- `pnpm test:e2e` silently hangs if Docker is not running. No error message.
- Migrations must run BEFORE seeding. The seed script does not check schema state.
- Port 5433 is hardcoded in `docker-compose.test.yml`, not in `.env`
```

## Why This Is Good

- **Description is a trigger**: tells WHEN to use, not HOW it works
- **Negative trigger**: "Do NOT use for unit tests" prevents over-activation
- **Every line is actionable**: step-by-step commands with verification
- **Conditional logic**: "If Docker is not running → ..." handles edge cases
- **Non-inferable knowledge**: port 5433 hardcoded location, silent hang behavior, seed ordering
- **Under 50 lines**: concise, no filler
