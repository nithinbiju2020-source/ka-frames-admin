KA FRAMES — SUPABASE-CONNECTED ADMIN UI

FILES
- index.html: admin interface + Supabase email/password authentication + database integration
- config.js: enter your Supabase Project URL and publishable/anon key here

SETUP
1. In Supabase, open Project Settings → API (or API Keys). Copy the Project URL and the publishable key (or legacy anon key).
2. Edit config.js and replace YOUR_SUPABASE_PROJECT_URL and YOUR_SUPABASE_PUBLISHABLE_KEY. Keep the quotes. Do NOT use a service_role/secret key.
3. In Supabase Authentication → URL Configuration, add your eventual GitHub Pages URL to Site URL and Redirect URLs. For example: https://YOUR-GITHUB-USERNAME.github.io/ka-frames-admin/
4. Ensure the Supabase Auth user is registered in public.admin_users using that user's Auth UID. The app checks this allow-list at sign-in.
5. Upload index.html and config.js to the root of a GitHub repository. Enable Settings → Pages → Deploy from a branch → main → /(root).
6. Open the Pages URL, sign in with the Supabase Auth email/password, create a test key, and verify it appears in Supabase Table Editor → memory_keys.

DATABASE EXPECTATIONS
This UI expects public.memory_keys columns created by the provided schema: id, order_id, customer_name, secret_key, destination_url, destination_type, notes, expires_at, is_active, is_archived, created_at, updated_at. It reads unlock_events for activity counts.

SECURITY NOTES
- Only publishable/anon key belongs in config.js. Never publish service_role or secret keys.
- RLS must remain enabled. Admin access should be restricted to users listed in public.admin_users.
- This page is for admin management only. Do not let the customer-facing unlock page read the whole memory_keys table. Use a narrowly scoped Supabase Edge Function/server endpoint for customer key validation and redirects.
- Do not commit real customer data or private URLs to a public repository. A public repo is fine for source code because config.js contains only the frontend publishable key, but a private repo is an extra precaution.
