# Chấm Công Công Trình V2 (starter)

React + Vite frontend, Supabase Postgres/Auth, ready for Vercel deployment.

## Included in this starter
- Email/password login through Supabase Auth
- Dashboard cards and quick daily attendance
- Worker CRUD (worker profile fields, role Cai/Thợ/Phụ, pay/day)
- Project creation/list
- Attendance: full day, half day, absent
- Daily pay preview for selected date
- Responsive desktop/mobile layout
- SQL schema with RLS policies and role scaffold

## Setup
1. Create a Supabase project.
2. Open SQL Editor and execute `supabase/schema.sql`.
3. In Authentication > Users, create an initial user with email/password.
4. Copy that user's UUID. Run the commented insert at the bottom of the SQL, substituting the UUID and display name, with role `admin`.
5. Copy Supabase Project URL and anon/public key (NOT service_role key).
6. Locally: copy `.env.example` to `.env.local`, fill `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
7. `npm install` then `npm run dev`.

## Vercel deploy
- Push this folder to a GitHub repository.
- Import the repository in Vercel; framework preset Vite is detected.
- Build command: `npm run build`; output directory: `dist`.
- Add environment variables `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` in Vercel project settings, then deploy.
- In Supabase Auth > URL Configuration, set Site URL to your deployed Vercel URL and add the URL to Redirect URLs.

## Important security notes
- Do not add the Supabase `service_role` secret to Vite environment variables or the browser bundle.
- RLS is enabled in the SQL schema. The current starter allows staff to read worker/project/attendance data; only admins can manage workers/projects; admins and cai roles can write attendance. Cai role scoping to specific project assignments is not yet implemented in this MVP.
- Because CCCD, phone, address, and bank account data are personal information, use only trusted users. Before production, review policies to restrict access to sensitive worker fields and add an export/backup process.
- The starter attendance UI currently fetches attendance for the selected date; payroll page is a daily preview only. Monthly rollups, advances, payroll locking, worker-project assignment screens, and role-specific project restrictions are planned next.
