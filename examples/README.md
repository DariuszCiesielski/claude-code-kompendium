# Przykłady — Claude Code Kompendium

Gotowe do użycia szablony, skille i konfiguracje hooków dla Claude Code.

## Szablony CLAUDE.md

Pliki CLAUDE.md dopasowane do konkretnych stacków technologicznych. Skopiuj odpowiedni szablon do katalogu głównego swojego projektu i dostosuj.

| Plik | Opis |
|------|------|
| [claude-md-nextjs.md](claude-md-nextjs.md) | Szablon dla projektów Next.js (App Router, TypeScript, Tailwind) |
| [claude-md-react-vite.md](claude-md-react-vite.md) | Szablon dla projektów React + Vite |
| [claude-md-python.md](claude-md-python.md) | Szablon dla projektów Python |
| [skill-template.md](skill-template.md) | Uniwersalny szablon skilla do skopiowania |

## Skille

Kompletne skille do zainstalowania w `~/.claude/skills/`. Każdy skill to folder z plikiem `SKILL.md` zawierającym triggery, instrukcje krok po kroku i przykłady kodu.

### Instalacja

```bash
# Skopiuj folder skilla do katalogu skilli Claude Code
cp -r examples/skills/nazwa-skilla ~/.claude/skills/
```

### Dostępne skille

| Skill | Opis | Triggery |
|-------|------|----------|
| [token-optimizer](skills/token-optimizer/SKILL.md) | Analiza i optymalizacja zużycia tokenów w sesji — identyfikuje marnotrawstwo, sugeruje kompresję kontekstu i uczy oszczędnych wzorców pracy | "optymalizuj tokeny", "za dużo tokenów", "oszczędzaj kontekst" |
| [project-setup](skills/project-setup/SKILL.md) | Inicjalizacja nowych projektów z kompletną strukturą folderów, CLAUDE.md, .gitignore, TypeScript i ESLint | "nowy projekt", "zainicjalizuj projekt", "scaffolding projektu" |

## Hooki

Konfiguracje hooków Claude Code w formacie `settings.json`. Hooki automatyzują powtarzalne zadania — uruchamiają się przed/po operacjach agenta.

### Instalacja

Skopiuj zawartość wybranego pliku JSON do swojego `.claude/settings.json` (globalnie) lub `.claude/settings.json` w katalogu projektu (lokalnie).

```bash
# Podgląd konfiguracji
cat examples/hooks/pre-commit-check.json

# Edytuj settings.json i wklej sekcję "hooks"
code ~/.claude/settings.json
```

### Dostępne hooki

| Plik | Zdarzenie | Opis |
|------|-----------|------|
| [pre-commit-check.json](hooks/pre-commit-check.json) | `PreCommit` | Sprawdzenie typów TypeScript, lint zmienionych plików i blokada commitowania sekretów — uruchamia się automatycznie przed każdym commitem |
| [auto-test.json](hooks/auto-test.json) | `PostToolUse` | Automatyczne uruchamianie testów powiązanych z edytowanym plikiem (Vitest) oraz przypomnienie o testach po zmianie zależności npm |

## Jak używać tych przykładów

1. **Szablony CLAUDE.md** — skopiuj do katalogu projektu, dostosuj sekcje do swoich potrzeb
2. **Skille** — skopiuj folder do `~/.claude/skills/`, Claude Code automatycznie je wykryje
3. **Hooki** — wklej konfigurację do `settings.json`, zrestartuj Claude Code

## Tworzenie własnych

- Szablon skilla: [skill-template.md](skill-template.md)
- Przewodnik po skillach: [Rozdział 3 — System skilli](../guide/03-system-skilli.md)
- Przewodnik po hookach: [Rozdział 6 — Automatyzacje](../guide/06-automatyzacje.md)
