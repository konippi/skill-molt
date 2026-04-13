# Bad Skill Example

This is an example of a poorly written skill with annotations explaining each problem.

## The Skill

```markdown
---
name: database-skill
description: "Helps with database operations including migrations, seeding,
  querying, and managing the PostgreSQL database for the project. Runs
  migrations with Drizzle ORM, seeds test data, and handles connections."
---

# Database Skill

## About Our Database

We use PostgreSQL with Drizzle ORM for our database layer. The database
configuration is stored in `drizzle.config.ts`. Migrations are generated
by Drizzle Kit and stored in the `drizzle/migrations/` directory.

## How to Run Migrations

To run migrations, use the following command:

`npx drizzle-kit migrate`

This will apply all pending migrations to the database.

## How to Seed Data

To seed the database with test data:

`npx drizzle-kit seed`

## Testing

Run `npm test` to run the test suite.

## Notes

- Make sure your database is running before running migrations
- Check the `.env` file for database connection settings
- The database schema is defined in `src/db/schema.ts`
```

## What's Wrong (annotated)

| Line | Problem | Principle Violated |
| --- | --- | --- |
| `description` | Summarizes the workflow ("Runs migrations with Drizzle ORM, seeds test data") — agent will skip the body | Description must be a trigger, not a summary |
| `name: database-skill` | Too generic. "database" matches everything | Name should describe the specific domain |
| "About Our Database" section | Explains what things ARE, not what to DO | Procedures, not documentation |
| "We use PostgreSQL with Drizzle ORM" | Discoverable from `package.json` and `drizzle.config.ts` | Non-inferable information only |
| "Configuration is stored in drizzle.config.ts" | Agent can find this by reading the project | Non-inferable information only |
| "Make sure your database is running" | No specific command to check or start it | Commands need verification steps |
| "Check the .env file" | Vague — which variable? What value? | Be specific, not hand-wavy |
| No conditional logic | What if migration fails? What if DB is not running? | Include error handling |
| No gotchas section | No non-obvious pitfalls captured | The whole point of a skill is non-obvious knowledge |
