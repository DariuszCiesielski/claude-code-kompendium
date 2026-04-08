# Token Optimizer

## Opis

Skill analizuje zużycie tokenów w bieżącej sesji Claude Code i sugeruje konkretne optymalizacje. Pomaga utrzymać niskie koszty przy zachowaniu pełnej funkcjonalności — identyfikuje duże pliki w kontekście, proponuje kompresję i wskazuje wzorce marnotrawiące tokeny.

## Triggery

- "optymalizuj tokeny"
- "za dużo tokenów"
- "oszczędzaj kontekst"
- "zmniejsz zużycie tokenów"
- "sesja się kończy"

## Instrukcje

### Krok 1: Audyt bieżącego kontekstu

Sprawdź co zajmuje najwięcej miejsca w kontekście sesji:

1. Przejrzyj historię narzędzi — które pliki były czytane wielokrotnie
2. Zidentyfikuj duże pliki (>500 linii) załadowane do kontekstu
3. Sprawdź czy są redundantne odczyty (ten sam plik czytany >2 razy)

```bash
# Sprawdź rozmiary plików w projekcie
find . -name "*.ts" -o -name "*.tsx" -o -name "*.js" | xargs wc -l | sort -rn | head -20
```

### Krok 2: Zastosuj techniki redukcji

Dla każdego zidentyfikowanego problemu zastosuj odpowiednią technikę:

**Duże pliki** — czytaj tylko potrzebne fragmenty:
```
Read file_path z offset i limit zamiast całego pliku
```

**Powtarzające się odczyty** — zapisz kluczowe informacje:
```
Zapamiętaj strukturę/typy/interfejsy w kontekście zamiast wracać do pliku
```

**Wyniki wyszukiwania** — ogranicz zakres:
```
Grep z parametrem head_limit zamiast domyślnego
Glob z precyzyjnym wzorcem zamiast **/*
```

### Krok 3: Optymalizuj komendy bash

Zamieniaj rozwlekłe komendy na zwięzłe odpowiedniki:

| Marnotrawne | Zoptymalizowane |
|---|---|
| `cat plik.ts` | `Read` z offset/limit |
| `find . -name "*.ts"` | `Glob "**/*.ts"` |
| `grep -r "pattern" .` | `Grep` z type/glob |
| `git log --all --oneline` | `git log --oneline -10` |
| `ls -laR` | `ls` konkretnego katalogu |

### Krok 4: Zaproponuj zmiany w workflow

Przygotuj listę rekomendacji dla użytkownika:

1. **Podziel duże pliki** — jeśli plik >300 linii, zasugeruj ekstrakcję modułów
2. **Użyj .claudeignore** — wyklucz `node_modules`, `dist`, `.next`, pliki generowane
3. **Kompaktowanie** — jeśli sesja jest długa, zaproponuj kompaktowanie kontekstu
4. **Precyzyjne zapytania** — naucz użytkownika formułować pytania z kontekstem (np. "w pliku X popraw funkcję Y" zamiast "napraw błąd")

## Przykład działania

**Scenariusz**: Użytkownik pisze "za dużo tokenów, sesja się kończy"

**Odpowiedź skilla**:
```
Przeanalizowałem zużycie kontekstu. Oto co znalazłem:

1. Plik `src/components/Dashboard.tsx` (847 linii) — czytany 4 razy w całości
   → Następnym razem czytaj tylko potrzebną funkcję (offset/limit)

2. Wyniki `Grep` bez limitu — 3 wyszukiwania zwróciły 200+ linii każde
   → Używaj head_limit: 20 i zawężaj wzorcem glob

3. Brak .claudeignore — node_modules indeksowany
   → Tworzę .claudeignore z wykluczeniami

Szacowana oszczędność: ~40% tokenów na sesję.
```

## Checklist

- [ ] Zidentyfikowano pliki >500 linii w kontekście
- [ ] Sprawdzono powtarzające się odczyty
- [ ] Zaproponowano .claudeignore (jeśli brak)
- [ ] Przygotowano listę rekomendacji dla użytkownika
- [ ] Oszacowano potencjalną oszczędność tokenów
