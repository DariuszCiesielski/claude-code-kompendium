# Rozdział 8: Debugowanie

## Systematyczne podejście do debugowania

Zamiast zgadywać, podejdź do debugowania metodycznie. Claude Code jest w tym dobry — ale potrzebuje Twojej pomocy w opisaniu problemu.

## Wzorzec zgłaszania błędu

### Słabo:

```
> Nie działa
```

### Dobrze:

```
> Formularz logowania zwraca błąd 500 po kliknięciu "Zaloguj się".
> W konsoli widzę: "TypeError: Cannot read properties of undefined (reading 'email')"
> Ostatnia zmiana: dodałem walidację w auth.ts
> Próbowałem: wyczyścić cache, zrestartować serwer — bez efektu
```

## Szablon opisu błędu

```
1. Co powinno się dziać: [oczekiwane zachowanie]
2. Co się dzieje: [faktyczne zachowanie]
3. Kroki do odtworzenia: [1, 2, 3...]
4. Komunikat błędu: [dokładna treść]
5. Ostatnie zmiany: [co zmieniałem przed wystąpieniem błędu]
6. Co próbowałem: [dotychczasowe próby naprawy]
```

## Strategie debugowania

### 1. Binary search — zawęż problem

Zamiast szukać igły w stogu siana, dziel problem na pół:

```
> Czy błąd jest po stronie frontendu czy backendu?
> Sprawdź: wyślij request z curl — jeśli curl działa, problem w UI.
> Jeśli curl też zwraca 500, problem w API route.
```

### 2. Minimalne odtworzenie

```
> Odtwórz ten błąd na minimalnym przykładzie — nowy plik z samą
> funkcją, która failuje. Bez reszty kodu.
```

### 3. Czytanie logów

```
> Pokaż mi logi serwera z ostatnich 5 minut
> Przefiltruj pod kątem ERROR i WARNING
> Sprawdź też logi Supabase (jeśli problem z bazą)
```

### 4. Git bisect — znajdź commit, który złamał

```
> Użyj git bisect żeby znaleźć commit, który wprowadził ten błąd.
> Ostatni działający: commit abc123 (3 dni temu)
> Pierwszy niedziałający: HEAD
```

### 5. Rubber duck debugging z AI

Opisz problem szczegółowo — sam proces opisywania często ujawnia przyczynę:

```
> Muszę Ci wyjaśnić problem krok po kroku.
> Mam formularz, który wysyła POST do /api/auth/login.
> Route handler pobiera email i password z body.
> Potem wywołuje supabase.auth.signInWithPassword.
> Hmm... czy body jest prawidłowo parsowane? Sprawdźmy.
```

## Typowe kategorie błędów

### Błędy TypeScript

```
> Mam błąd TS: "Type 'string | undefined' is not assignable to type 'string'"
> W pliku: src/components/UserCard.tsx, linia 15
```

Claude doda odpowiedni null check lub typ opcjonalny.

### Błędy runtime (500, undefined, null)

```
> API route /api/users zwraca 500
> Pokaż mi cały request flow: od fetch w komponencie do response w route
```

### Błędy budowania

```
> npm run build failuje z błędem [treść]
> Pokaż mi pełny output builda
```

### Problemy z async/await

```
> Dane nie są załadowane w momencie renderowania
> Podejrzewam brak await — sprawdź wszystkie async operacje w tym flow
```

## Narzędzia debugowania

| Narzędzie | Kiedy użyć |
|-----------|-----------|
| `console.log` / `console.error` | Szybka inspekcja wartości |
| DevTools → Network | Problemy z API (request/response) |
| DevTools → Console | Błędy JS w przeglądarce |
| `curl` / `httpie` | Testowanie API bez UI |
| React DevTools | Stan komponentów, re-rendery |
| Supabase Dashboard | Problemy z bazą, RLS |

## Checklist przed zgłoszeniem

- [ ] Czy zrestartowałem serwer?
- [ ] Czy wyczyściłem cache przeglądarki?
- [ ] Czy `npm install` jest aktualny?
- [ ] Czy zmienne środowiskowe `.env.local` są poprawne?
- [ ] Czy baza danych jest dostępna?
- [ ] Czy błąd jest powtarzalny?

## Następny rozdział

[← Rozdział 7: Multi-agent](07-multi-agent.md) | [Rozdział 9: Integracje →](09-integracje.md)
