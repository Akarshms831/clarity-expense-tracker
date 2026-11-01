# Clarity — safe application rebuild

This rebuild keeps the existing Clarity interface and Supabase data model. It does **not** require a database migration.

## Important: protect your existing data

- Keep using the existing Supabase project and the existing `public.clarity_user_data` table.
- Do **not** run a new schema, drop/recreate the table, delete rows, or create a replacement database.
- The existing SQL schema is included for reference only and is unchanged. It is not an installation step for this update.
- The browser uses only the existing Supabase project URL and publishable key. No service-role key is included.

## What changed

- The dashboard HTML and CSS are retained unchanged.
- The existing dashboard, expense, salary, budget, category editing, export, and profile features remain in `js/app.js`.
- Supabase client creation is now a singleton instead of repeatedly creating clients.
- Authentication errors and cloud-data read errors are reported as separate stages.
- Sign-in reads the existing account row before any cloud write.
- A missing or malformed cloud row is reported without silently replacing it with an empty payload.
- A local recovery snapshot is retained before the cloud payload replaces the active local cache.
- A new account's first row is created with `INSERT`, never an upsert that could replace an existing row.
- Cloud writes continue to use the existing table and `user_id` conflict key.

## Deploy to the existing GitHub repository

1. Download and extract this ZIP.
2. Upload the **contents** of the `clarity-expense-tracker` folder to the root of the existing `Akarshms831/clarity-expense-tracker` repository, preserving `css/`, `js/`, and `supabase/`.
3. Replace the existing application files when GitHub asks. Do not delete or change anything in Supabase.
4. Wait for GitHub Pages to publish the commit.
5. Open the live site and sign in using the existing account.

## Existing database contract

The application continues to read and write only `public.clarity_user_data` using the signed-in user's UUID and the existing JSON `payload` column. Row-level security remains enforced by Supabase. No database migration is part of this release.

## Validation

The JavaScript syntax is checked with Node.js. Live authentication and cloud sync still need to be verified against the user's Supabase project after deployment; a ZIP build cannot prove that the remote service is reachable.
