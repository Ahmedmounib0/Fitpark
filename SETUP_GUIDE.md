# Fit Park Fouchana — Setup Guide

## Step 1 — Supabase (Real Database)

1. Go to https://supabase.com → Sign up → New Project
2. Name it "fitpark-fouchana" → Create
3. Go to **SQL Editor** → Run this SQL:

```sql
create table registrations (
  id bigserial primary key,
  created_at timestamptz default now(),
  type text,
  prenom text,
  nom text,
  telephone text,
  email text,
  objectif text,
  message text
);

create table newsletter (
  id bigserial primary key,
  created_at timestamptz default now(),
  email text unique
);

-- Allow public inserts
alter table registrations enable row level security;
alter table newsletter enable row level security;
create policy "Allow inserts" on registrations for insert with check (true);
create policy "Allow inserts" on newsletter for insert with check (true);
create policy "Allow reads for auth" on registrations for select using (auth.role() = 'authenticated');
create policy "Allow reads for auth" on newsletter for select using (auth.role() = 'authenticated');
```

4. Go to **Settings → API**
5. Copy **Project URL** and **anon public key**
6. In `index.html`, replace:
   - `YOUR_PROJECT` → your real project URL
   - `YOUR_ANON_KEY` → your real anon key

---

## Step 2 — GitHub

1. Go to https://github.com → New repository
2. Name it `fitpark-fouchana` → Public → Create
3. Upload ALL files from this folder
4. Commit

---

## Step 3 — Netlify

1. Go to https://netlify.com → New site from Git
2. Connect GitHub → Select `fitpark-fouchana`
3. Build settings: leave empty (static site)
4. Deploy!

---

## Step 4 — Netlify Identity (Secure Admin Login)

1. In Netlify → your site → **Identity** tab
2. Click **Enable Identity**
3. **Invite users** → enter `douissafitness@gmail.com`
4. Client clicks the email link → sets their password
5. Done! Admin login is now secure ✅

---

## Step 5 — Netlify CMS (Client can edit content)

1. After deploying, go to `yoursite.netlify.app/admin`
2. Log in with Netlify Identity
3. Client can now edit: prices, schedules, coaches, testimonials

---

## Admin Panel Access

- **Triple-click** footer FITPARK logo
- OR `Ctrl + Shift + A`
- Password (before Netlify Identity): `F!tP@rk#S4if_2026`
