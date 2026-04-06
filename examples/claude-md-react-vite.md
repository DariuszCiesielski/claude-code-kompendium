# Przykład CLAUDE.md — Projekt React + Vite

```markdown
# Aplikacja React + Vite

## Tech stack
- React 19
- Vite 6
- TypeScript (strict)
- Tailwind CSS v4
- React Router v7
- TanStack Query (React Query)

## Struktura
- `src/pages/` — strony (routing)
- `src/components/` — komponenty UI
- `src/hooks/` — custom hooki
- `src/api/` — klient API i typy
- `src/utils/` — helpery
- `src/assets/` — statyczne zasoby

## Konwencje
- Komponenty: PascalCase, jeden komponent na plik
- Hooki: useNazwa.ts
- Testy: obok pliku (Component.test.tsx)
- CSS: Tailwind utility classes, brak plików CSS
- Polskie znaki we wszystkich stringach UI

## Routing
- React Router v7 z createBrowserRouter
- Chronione route przez komponent ProtectedRoute
- Layout z Sidebar + Header

## Stan
- TanStack Query do danych z serwera
- useState/useReducer do stanu lokalnego
- Context tylko dla globalnych ustawień (auth, theme)

## Build
- `npm run dev` — development
- `npm run build` — production build
- `npm run preview` — podgląd builda
```
