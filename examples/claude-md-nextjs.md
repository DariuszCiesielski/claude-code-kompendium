# Przykład CLAUDE.md — Projekt Next.js + Supabase

```markdown
# Mój Projekt SaaS

## Tech stack
- Next.js 16 (App Router)
- TypeScript (strict mode)
- Supabase (auth, database, realtime, storage)
- Tailwind CSS + shadcn/ui
- Vercel (hosting)

## Struktura projektu
- `src/app/` — App Router (routing, layouty, strony)
- `src/app/api/` — API routes
- `src/components/` — komponenty React
- `src/lib/` — utilities, helpery, konfiguracje
- `src/types/` — typy TypeScript
- `supabase/migrations/` — migracje SQL

## Konwencje kodu
- Nazwy zmiennych/funkcji: camelCase po angielsku
- Nazwy komponentów: PascalCase
- Typy/interfejsy: PascalCase z prefiksem (np. UserProfile, ProjectCard)
- Stringi UI: po polsku z diakrytykami (ą,ć,ę,ł,ń,ó,ś,ź,ż)
- Commit messages: po polsku

## Czcionki
- next/font/google z `subsets: ["latin-ext"]`
- html lang="pl"

## Bezpieczeństwo
- Każdy API route sprawdza auth (getAuthUser())
- RLS na każdej tabeli Supabase
- Zmienne środowiskowe w .env.local (NIGDY w kodzie)
- Error messages nie wyciekają wewnętrznych szczegółów

## Zasady
- Nie używaj `any` — generuj typy Supabase przez CLI
- Nie modyfikuj istniejących migracji — twórz nowe
- Testuj w przeglądarce po zmianach UI
- Po git push sprawdź status deployu na Vercel

## Lessons Learned
- [2026-01-15] Middleware auth: sprawdzaj session w proxy.ts, nie w każdym route
- [2026-02-01] Supabase typy: generuj przez `supabase gen types` po każdej migracji
```
