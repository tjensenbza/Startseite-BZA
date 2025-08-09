# Weiterleitungs-Seite mit Supabase

Eine kleine HTML-Seite, die automatisch Buttons aus einer Supabase-Datenbank lädt und zu deinen Projekten weiterleitet.

## 🚀 Funktionen
- Buttons werden dynamisch aus einer Supabase-Tabelle (`links`) geladen
- Keine Codeänderung nötig, um neue Links hinzuzufügen – einfach in Supabase eintragen
- Mobile- und Desktop-kompatibel

---

## 📦 Installation & Einrichtung

### 1. Supabase-Tabelle erstellen
Falls noch nicht vorhanden, erstelle die Tabelle in Supabase:

```sql
create table if not exists public.links (
  id        bigint generated always as identity primary key,
  title     text    not null,
  url       text    not null check (url ~ '^https?://'),
  order_nr  integer,
  created_at timestamptz not null default now()
);

alter table public.links enable row level security;

create policy "links: public read"
on public.links
for select
using (true);

insert into public.links (title, url, order_nr) values
  ('Problems', 'https://tjensenbza.github.io/Problems/', 1),
  ('Bestellmeldung-Tool', 'https://bestellmeldung-tool-git-main-tjensenbzas-projects.vercel.app', 2),
  ('KVP', 'https://tjensenbza.github.io/KVP/', 3),
  ('Urlaubsantrag-Tool', 'https://urlaubsantrag-tool.vercel.app/', 4);
