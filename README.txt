CLARITY — LIQUID GLASS SALARY & EXPENSE TRACKER
================================================

HOSTING
- This is a static website suitable for GitHub Pages.
- Upload index.html, supabase_schema.sql and this README to your repository.
- Enable GitHub Pages in repository Settings -> Pages.
- Internet access is required for Supabase sync and the Excel, PDF and image export libraries loaded from CDNs.
- Local mode works without a Supabase account and saves to that browser's localStorage.

TAKE-HOME SALARY, BUDGET LIMIT & EXPENSES
- Open Salary & monthly budget.
- Enter the take-home salary you actually received for the selected month.
- Set a separate budget limit that is equal to or lower than take-home salary. The app validates this rule.
- Expenses are NOT capped: you can record any expense, even if total spending exceeds your budget or salary.
- Budget remaining = budget limit - expenses. Salary after expenses = take-home salary - expenses. Either can become negative.
- Different months can have different salary and budget amounts. The month selector and arrows filter every section.

SET UP ONLINE DATABASE (SUPABASE)
1. Create a project at https://supabase.com/.
2. In Project Settings -> API, copy the Project URL and the public anon/publishable key.
   Never use or expose a service_role/secret key in this frontend.
3. Open SQL Editor in Supabase and run the complete supabase_schema.sql file included here.
4. In Authentication settings, configure email confirmation and allowed redirect URLs for your GitHub Pages URL.
5. Open the hosted website -> Settings. Enter the Supabase URL and public anon/publishable key.
6. Choose Save connection, then Create account. Confirm your email if confirmation is enabled, then sign in.
7. The app loads that user's saved record and syncs updates after you save salary/settings/expenses.
8. Sign in with the same account on another device to access the same data.

SECURITY NOTES
- The SQL schema enables Row Level Security (RLS) and restricts each row to the authenticated user.
- The public anon/publishable key is designed to be used in browser apps when RLS is correctly configured.
- Do not disable RLS or use the service_role key.
- The app's cloud model stores one JSON payload per signed-in user. Keep periodic JSON exports from Share & export.
- If Supabase email confirmation is on, sign-up may not create a session until the email is confirmed.
- GitHub Pages only hosts the frontend; Supabase is the database and authentication provider.

SHARE & EXPORT
- Use the Share & export section to generate a designed monthly report for the selected month.
- Excel workbook (.xlsx): includes monthly summary, selected-month metrics/category totals, and all transactions in separate sheets.
- PDF (.pdf) and image (.jpg): export the styled graphical report for the selected month.
- Share report: uses the device share sheet where supported, sharing a JPG and summary where possible.
- CSV exports all expense transactions; JSON exports the full app data for a personal recovery copy.
- Local browser data is kept as a recovery copy. Restoring a JSON export replaces the current local working copy; sync it to cloud after restoring.
