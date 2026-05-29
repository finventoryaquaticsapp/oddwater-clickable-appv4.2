create table if not exists public.profiles (
  id uuid primary key references auth.users(id) on delete cascade,
  email text,
  display_name text,
  created_at timestamptz default now()
);

create table if not exists public.tanks (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  name text not null,
  type text not null default 'Freshwater community',
  gallons numeric default 0,
  temp numeric default 0,
  ph numeric default 7.0,
  ammonia numeric default 0,
  nitrite numeric default 0,
  nitrate numeric default 0,
  stocking_level text default 'moderate',
  maintenance_overdue boolean default false,
  disease_alert boolean default false,
  notes text default '',
  created_at timestamptz default now()
);

create table if not exists public.water_logs (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  tank_id uuid references public.tanks(id) on delete cascade,
  ammonia numeric default 0,
  nitrite numeric default 0,
  nitrate numeric default 0,
  ph numeric default 7.0,
  temp numeric default 0,
  notes text default '',
  created_at timestamptz default now()
);

alter table public.profiles enable row level security;
alter table public.tanks enable row level security;
alter table public.water_logs enable row level security;

create policy "profiles select own" on public.profiles for select using (auth.uid() = id);
create policy "profiles insert own" on public.profiles for insert with check (auth.uid() = id);
create policy "profiles update own" on public.profiles for update using (auth.uid() = id);
create policy "tanks select own" on public.tanks for select using (auth.uid() = user_id);
create policy "tanks insert own" on public.tanks for insert with check (auth.uid() = user_id);
create policy "tanks update own" on public.tanks for update using (auth.uid() = user_id);
create policy "tanks delete own" on public.tanks for delete using (auth.uid() = user_id);
create policy "water logs select own" on public.water_logs for select using (auth.uid() = user_id);
create policy "water logs insert own" on public.water_logs for insert with check (auth.uid() = user_id);
create policy "water logs update own" on public.water_logs for update using (auth.uid() = user_id);
create policy "water logs delete own" on public.water_logs for delete using (auth.uid() = user_id);
