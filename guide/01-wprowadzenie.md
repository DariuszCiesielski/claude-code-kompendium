# Rozdział 1: Wprowadzenie do Claude Code

## Czym jest Claude Code?

Claude Code to oficjalne narzędzie CLI (Command Line Interface) od Anthropic, które pozwala programować z pomocą Claude — zaawansowanego modelu AI. W odróżnieniu od chatbotów webowych, Claude Code:

- **Działa bezpośrednio w terminalu** — ma dostęp do systemu plików, gita, narzędzi deweloperskich
- **Rozumie kontekst projektu** — czyta pliki, analizuje strukturę kodu, rozumie zależności
- **Wykonuje polecenia** — tworzy pliki, uruchamia testy, commituje zmiany, debuguje błędy
- **Pamięta kontekst** — system pamięci przechowuje decyzje i preferencje między sesjami

## Instalacja

### Wymagania

- **Node.js** 18+ (zalecane: 20 LTS)
- **npm** lub **pnpm**
- **Konto Anthropic** z kluczem API lub subskrypcją Claude

### Krok 1: Zainstaluj globalnie

```bash
npm install -g @anthropic-ai/claude-code
```

### Krok 2: Zweryfikuj instalację

```bash
claude --version
```

### Krok 3: Pierwsza sesja

Przejdź do katalogu projektu i uruchom:

```bash
cd ~/moj-projekt
claude
```

Claude Code przeanalizuje strukturę projektu i będzie gotowy do pracy.

## Pierwszy kontakt

Po uruchomieniu zobaczysz interaktywny prompt. Możesz po prostu pisać po polsku:

```
> Przeanalizuj ten projekt i powiedz mi co robi

> Dodaj nowy komponent Button z wariantami primary i secondary

> Napraw błąd w pliku src/utils.ts — funkcja parsuje datę niepoprawnie
```

Claude Code sam zdecyduje jakie pliki przeczytać, jakie narzędzia użyć i jakie zmiany wprowadzić.

## Tryby pracy

### Tryb interaktywny (domyślny)

```bash
claude
```

Otwiera sesję konwersacji. Piszesz polecenia, Claude wykonuje, pytasz dalej.

### Tryb jednorazowy

```bash
claude "dodaj .gitignore do projektu"
```

Wykonuje jedno polecenie i kończy sesję.

### Tryb pipe

```bash
cat error.log | claude "przeanalizuj ten log i zaproponuj fix"
```

Przekazuje dane przez stdin — przydatne w skryptach.

## Struktura katalogów Claude Code

Po pierwszym uruchomieniu Claude Code tworzy:

```
~/.claude/
├── CLAUDE.md           # Globalne instrukcje (dla wszystkich projektów)
├── settings.json       # Konfiguracja (hooki, uprawnienia)
├── memory/             # System pamięci
├── skills/             # Globalne skille
└── projects/           # Konfiguracje per projekt
    └── -path-to-project/
        ├── CLAUDE.md   # Instrukcje specyficzne dla projektu
        └── memory/     # Pamięć projektu
```

## Kluczowe pojęcia

| Pojęcie | Opis |
|---------|------|
| **Sesja** | Jedna rozmowa z Claude Code (od uruchomienia do zamknięcia) |
| **Kontekst** | Ilość tekstu, którą Claude „pamięta" w ramach sesji (~200K tokenów) |
| **Token** | Jednostka tekstu (~4 znaki). Im więcej tokenów, tym wyższy koszt |
| **Skill** | Zestaw instrukcji dla powtarzalnych zadań (np. „utwórz komponent React") |
| **Hook** | Automatyczna akcja uruchamiana przy określonym zdarzeniu |
| **MCP** | Model Context Protocol — standard integracji z zewnętrznymi narzędziami |

## Wskazówki na start

1. **Pisz po polsku** — Claude doskonale rozumie polski
2. **Bądź konkretny** — „Dodaj walidację email w formularzu rejestracji" > „Popraw formularz"
3. **Iteruj** — zacznij od prostego polecenia, doprecyzuj w kolejnych krokach
4. **Czytaj co Claude robi** — ucz się z jego podejścia do problemów

## Następny rozdział

[Rozdział 2: Podstawowe komendy →](02-podstawowe-komendy.md)
