# Szablon skilla — do skopiowania i dostosowania

Utwórz folder w `~/.claude/skills/nazwa-skilla/` i wklej poniższy szablon do pliku `SKILL.md`:

```markdown
# Nazwa skilla

## Opis

[1-3 zdania opisujące co skill robi i w jakim kontekście go używać.]

## Triggery

Frazy aktywujące ten skill:
- "[fraza 1]"
- "[fraza 2]"
- "[fraza 3]"

## Instrukcje

### Krok 1: [Nazwa kroku]

[Opis co zrobić. Bądź konkretny — Claude potrzebuje jasnych instrukcji.]

### Krok 2: [Nazwa kroku]

[Opis co zrobić.]

### Krok 3: [Nazwa kroku]

[Opis co zrobić.]

## Przykład kodu

\```typescript
// Przykładowy kod do wygenerowania/użycia
// Zamień placeholdery na konkretne wartości
\```

## Zależności

- **[pakiet]**: wersja (do czego służy)
- **[pakiet]**: wersja (do czego służy)

## Checklist

- [ ] [Krok weryfikacji 1]
- [ ] [Krok weryfikacji 2]
- [ ] [Krok weryfikacji 3]
```

## Zasady tworzenia skilli

1. **Uniwersalność** — skill musi działać w różnych projektach (bez hardcoded wartości)
2. **Konkretność** — instrukcje krok po kroku, nie ogólniki
3. **Przykłady** — dodaj snippety kodu do skopiowania
4. **Triggery** — 3-5 naturalnych fraz aktywujących
5. **Testowanie** — sprawdź skill na nowym, pustym projekcie
