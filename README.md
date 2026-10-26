# Clarity — Multi-user expense tracker

This folder contains the Clarity website and Supabase backend files. The interface and application logic are separated into HTML, CSS, and JavaScript files.

## Files
- `index.html` — page markup and CDN dependencies
- `css/styles.css` — responsive Liquid Glass styling
- `js/app.js` — dashboard, authentication, cloud sync, profile, exports, and account UI
- `supabase_schema.sql` — database table and row-level security policies
- `supabase/functions/delete-account/index.ts` — server-side account deletion endpoint

## Publish on GitHub Pages
Upload the **contents** of this folder into the root of the existing repository, preserving the `css/`, `js/`, and `supabase/` folder structure. Configure Pages to publish from `main` and `/(root)`.

## Supabase setup
1. Confirm the Project URL and browser-safe publishable key in `js/app.js` / application defaults are correct for your project. A publishable key is expected to be public; never put a service-role or secret key in browser files or GitHub.
2. Run `supabase_schema.sql` in the Supabase SQL Editor if the table/policies are not already installed.
3. In Supabase Authentication, configure allowed redirect URLs for the deployed GitHub Pages URL. Set email confirmation according to your preference.
4. Deploy the account deletion Edge Function using the Supabase CLI and configure the required server-side environment. Never put admin secrets in frontend code.

## Privacy checks before using real financial data
- Create two test accounts and confirm each begins with its own empty dataset.
- Add a dummy expense to account A; sign out and sign in as account B; verify the expense is not visible.
- Test refresh, sign-out, and sign-in from a second device/browser.
- Verify the `clarity_user_data` table has RLS enabled and the policies restrict rows to `auth.uid() = user_id`.
- Test account deletion only with a test account after the Edge Function is deployed.

## Notes
This is a static website with Supabase as its backend; GitHub Pages does not run server-side PHP, Java, or Python. Server-side actions are handled by Supabase Edge Functions. Validate all auth, RLS, and deletion behavior in the live project before entering real financial data.
