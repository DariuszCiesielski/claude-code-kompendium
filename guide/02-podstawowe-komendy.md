# Rozdział 2: Podstawowe komendy i skróty

## Komendy wbudowane (slash commands)

Komendy zaczynające się od `/` to wbudowane akcje Claude Code:

| Komenda | Opis | Przykład |
|---------|------|---------|
| `/help` | Pomoc i lista komend | `/help` |
| `/clear` | Wyczyść kontekst sesji | `/clear` |
| `/compact` | Skompaktuj kontekst (oszczędność tokenów) | `/compact` |
| `/status` | Status projektu i sesji | `/status` |
| `/commit` | Utwórz commit z opisem zmian | `/commit` |
| `/review` | Code review ostatnich zmian | `/review` |
| `/bug` | Zgłoś błąd w Claude Code | `/bug` |

## Skróty klawiszowe

| Skrót | Akcja |
|-------|-------|
| `Ctrl+C` | Przerwij bieżącą operację |
| `Ctrl+D` | Zakończ sesję |
| `Tab` | Autouzupełnianie |
| `↑ / ↓` | Historia poleceń |
| `Esc` | Tryb wieloliniowy (wpisz tekst, `Esc` ponownie by wysłać) |

## Praca z plikami

### Czytanie plików

Claude Code automatycznie czyta pliki, gdy ich potrzebujesz:

```
> Pokaż mi zawartość pliku src/App.tsx

> Co robi funkcja calculateTotal w utils.ts?
```

### Tworzenie i edycja plików

```
> Utwórz nowy plik src/components/Header.tsx z komponentem React

> W pliku src/styles.css dodaj style dla dark mode

> Zamień wszystkie console.log na proper logging w src/api/
```

### Wyszukiwanie w kodzie

```
> Znajdź wszystkie pliki używające useEffect

> Gdzie jest zdefiniowany typ UserProfile?

> Pokaż mi wszystkie API routes
```

## Praca z gitem

Claude Code natywnie wspiera operacje gitowe:

```
> Pokaż status gita

> Scommituj zmiany z opisem "Dodaj komponent Header"

> Utwórz brancha feature/dark-mode i przełącz się na niego

> Pokaż diff między main a bieżącym branchem
```

## Uruchamianie poleceń

Claude Code może uruchamiać polecenia w terminalu:

```
> Zainstaluj pakiet @tanstack/react-query

> Uruchom testy

> Zbuduj projekt i pokaż błędy

> Sprawdź jakie porty są zajęte
```

## Kontekst i pamięć w sesji

### Dodawanie kontekstu

```
> Przeczytaj README.md i ARCHITECTURE.md — potrzebujesz tego kontekstu

> @plik.ts  (szybkie dodanie pliku do kontekstu)
```

### Zarządzanie kontekstem

```
/compact          # Skompaktuj — Claude zachowa ważne informacje, usunie szczegóły
/clear            # Wyczyść całkowicie — nowa sesja
```

## Efektywne polecenia — wzorce

### Wzorzec: Opisz problem, nie rozwiązanie

```
# Źle (mówisz JAK):
> Dodaj try-catch do funkcji fetchData i w catch wyświetl console.error

# Dobrze (mówisz CO):
> Funkcja fetchData nie obsługuje błędów — dodaj obsługę z informowaniem użytkownika
```

### Wzorzec: Podaj kontekst biznesowy

```
# Słabo:
> Dodaj walidację do formularza

# Lepiej:
> Formularz rejestracji musi walidować: email (format), hasło (min 8 znaków,
> cyfra + duża litera), NIP (10 cyfr, checksum). Komunikaty błędów po polsku.
```

### Wzorzec: Iteracja

```
> Utwórz komponent tabeli z sortowaniem
[Claude tworzy tabelę]

> Dodaj paginację — 10 wierszy na stronę
[Claude rozszerza]

> Dodaj filtrowanie po kolumnie "status"
[Claude dodaje]
```

## Następny rozdział

[← Rozdział 1: Wprowadzenie](01-wprowadzenie.md) | [Rozdział 3: System skilli →](03-system-skilli.md)
