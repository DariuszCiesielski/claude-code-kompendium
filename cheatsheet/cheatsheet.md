# Claude Code — Ściągawka

## Uruchamianie

```bash
claude                           # Sesja interaktywna
claude "polecenie"               # Jednorazowe polecenie
cat plik | claude "analizuj"     # Tryb pipe
claude --resume                  # Wznów ostatnią sesję
```

## Komendy /slash

| Komenda | Opis |
|---------|------|
| `/help` | Pomoc |
| `/clear` | Wyczyść kontekst |
| `/compact` | Skompaktuj kontekst (oszczędność tokenów) |
| `/status` | Status sesji i zużycie tokenów |
| `/commit` | Utwórz git commit |
| `/review` | Code review ostatnich zmian |

## Skróty klawiszowe

| Skrót | Akcja |
|-------|-------|
| `Ctrl+C` | Przerwij operację |
| `Ctrl+D` | Zakończ sesję |
| `Tab` | Autouzupełnianie |
| `↑ / ↓` | Historia poleceń |
| `Esc` | Tryb wieloliniowy |

## Kluczowe pliki

```
~/.claude/CLAUDE.md              # Globalne instrukcje
~/.claude/settings.json          # Hooki, MCP, uprawnienia
~/.claude/skills/                # Globalne skille
./CLAUDE.md                      # Instrukcje projektu
./MEMORY.md                      # Pamięć projektu
./.ai/handoffs/                  # Handoffy sesji
```

## Wzorce poleceń

```
# Analiza
> Przeanalizuj ten projekt i opisz architekturę
> Znajdź wszystkie pliki używające [wzorzec]
> Pokaż zależności między modułami

# Tworzenie
> Utwórz komponent [nazwa] z [wymagania]
> Dodaj endpoint API [metoda] [ścieżka] z [logika]
> Wygeneruj typy TypeScript dla [struktury danych]

# Naprawianie
> Napraw błąd: [treść błędu] w [plik]
> Dlaczego [komponent] re-renderuje się w nieskończoność?
> Ten test failuje — pokaż dlaczego i napraw

# Git
> Scommituj z opisem "[opis]"
> Utwórz brancha [nazwa]
> Pokaż diff z main
```

## Optymalizacja tokenów

```
1. RTK (60-90% oszczędności CLI)    rtk gain
2. /compact co ~30 min
3. Grupuj operacje (1 polecenie > 5)
4. CLAUDE.md zamiast powtarzania
5. Skille zamiast długich promptów
6. Tryb jednorazowy dla prostych zadań
```

## Debugowanie — szablon

```
1. Co powinno się dziać: [oczekiwane]
2. Co się dzieje: [faktyczne]
3. Komunikat błędu: [treść]
4. Ostatnie zmiany: [co zmieniałem]
5. Co próbowałem: [dotychczasowe próby]
```

## MCP — konfiguracja

```json
// ~/.claude/settings.json
{
  "mcpServers": {
    "nazwa": {
      "command": "npx",
      "args": ["pakiet-mcp"],
      "env": { "API_KEY": "..." }
    }
  }
}
```

## Hooki — konfiguracja

```json
// ~/.claude/settings.json
{
  "hooks": {
    "SessionStart": [{ "matcher": "", "hooks": [{ "type": "command", "command": "..." }] }],
    "PreToolUse": [{ "matcher": "Write", "hooks": [{ "type": "command", "command": "..." }] }]
  }
}
```

## Skille — struktura

```
~/.claude/skills/nazwa-skilla/SKILL.md

# W SKILL.md:
- Opis: co robi
- Triggery: frazy aktywujące
- Instrukcje: krok po kroku
- Przykłady kodu
- Zależności
```

## Codzienne nawyki

| Kiedy | Co |
|-------|----|
| Start | Claude czyta handoffy |
| Praca | /compact co 30 min |
| Po bloku | Testy + linter |
| Koniec | Handoff + MEMORY.md |
