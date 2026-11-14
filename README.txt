QOOPZA FOOD — SECURE ADMIN PANEL STARTER

Files
- admin.html: browser-based admin login and order dashboard
- supabase-setup.sql: database tables, admin check function and Row Level Security policies

IMPORTANT
This is a secure starter panel, not yet connected to your live shop. Your existing GitHub Pages page currently uses browser localStorage/demo orders. Those orders do not automatically appear here. The customer checkout must also be connected to the same Supabase orders table before this becomes a real shared order system.

SETUP
1. Create a Supabase project at https://supabase.com/ (free tier availability/limits can change).
2. In Supabase Dashboard > SQL Editor, review and run supabase-setup.sql.
   If your project already has an orders table, compare columns first and adapt the SQL; do not overwrite existing data.
3. In Authentication > Users, create the admin account using an email and a strong unique password. Disable public sign-ups in Authentication settings if customers do not need account registration.
4. Copy the admin user's UUID from Authentication > Users.
5. In SQL Editor run:
   insert into public.admin_users (user_id) values ('PASTE-AUTH-USER-UUID-HERE');
6. In Project Settings > API, copy the Project URL and anon/public key. In admin.html replace:
   YOUR_SUPABASE_PROJECT_URL
   YOUR_SUPABASE_ANON_KEY
   Never use the service_role/secret key in HTML, JavaScript, GitHub, or any browser app.
7. Upload admin.html to the same GitHub Pages repository as a separate file, e.g. admin.html. Open:
   https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPOSITORY/admin.html
8. Sign in with the admin email/password created in step 3.

SECURITY NOTES
- Admin identity is checked with the server-side is_admin() function and protected by Supabase Row Level Security.
- Only UUIDs added to public.admin_users are admins.
- Do not share admin passwords or commit them to GitHub.
- UPI PINs, card numbers, CVVs, and banking passwords must never be collected or stored. For UPI, use a trusted payment provider checkout; otherwise treat UPI as a payment method/reference only.
- If you expose customer order lookup without customer login, use a separate secure Edge Function with an unguessable order lookup token; do not make the whole orders table public.

EXPECTED ORDERS COLUMNS
id, user_id, customer_name, phone, address, items (JSON array), total, payment_method ('UPI' or 'Cash on Delivery'), status, created_at.
