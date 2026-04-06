# Rozdział 6: Automatyzacje

## Hooki — automatyczne akcje

Hooki to skrypty uruchamiane automatycznie przy określonych zdarzeniach w Claude Code. Konfiguracja w `~/.claude/settings.json`.

## Rodzaje hooków

| Hook | Kiedy się uruchamia | Przykład użycia |
|------|-------------------|-----------------|
| `SessionStart` | Na początku sesji | Sprawdź handoffy, załaduj kontekst |
| `PreToolUse` | Przed użyciem narzędzia | Walidacja, logging |
| `PostToolUse` | Po użyciu narzędzia | Audit, notyfikacje |
| `Notification` | Przy powiadomieniu | Alerty Telegram/Slack |

## Konfiguracja hooków

W pliku `~/.claude/settings.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'Sesja rozpoczęta: '$(date)"
          }
        ]
      }
    ],
    "PreToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'Zapisuję plik: $TOOL_INPUT'"
          }
        ]
      }
    ]
  }
}
```

## Praktyczne przykłady hooków

### Hook: Automatyczne sprawdzanie handoffów

```json
{
  "SessionStart": [
    {
      "matcher": "",
      "hooks": [
        {
          "type": "command",
          "command": "ls -la .ai/handoffs/ 2>/dev/null || echo 'Brak handoffów'"
        }
      ]
    }
  ]
}
```

### Hook: Tworzenie katalogu .codex

```json
{
  "SessionStart": [
    {
      "matcher": "",
      "hooks": [
        {
          "type": "command",
          "command": "mkdir -p .codex/{tasks,reports,archived}"
        }
      ]
    }
  ]
}
```

### Hook: Optymalizacja tokenów z RTK

RTK automatycznie rejestruje się jako hook i przepisuje polecenia CLI, oszczędzając tokeny:

```json
{
  "PreToolUse": [
    {
      "matcher": "Bash",
      "hooks": [
        {
          "type": "command",
          "command": "rtk proxy $TOOL_INPUT"
        }
      ]
    }
  ]
}
```

## Zdalne agenty (Remote Triggers)

Claude Code umożliwia uruchamianie agentów zdalnie — na przykład przez cron:

```bash
# Uruchom agenta z konkretnym zadaniem
claude --remote "Sprawdź status deployów i wyślij raport na Telegram"
```

### Harmonogramowanie (Schedule)

```
/schedule create "Codzienny raport" --cron "0 6 * * *" --prompt "Sprawdź logi z ostatnich 24h"
```

## Automatyzacja z GitHub Actions

Możesz uruchomić Claude Code w CI/CD:

```yaml
# .github/workflows/claude-review.yml
name: AI Code Review
on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Claude Code Review
        run: |
          npx @anthropic-ai/claude-code "Zrób code review zmian w tym PR"
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
```

## Wskazówki

1. **Testuj hooki na małych operacjach** zanim wdrożysz globalnie
2. **Nie blokuj workflow** — hooki powinny być szybkie (<5 sekund)
3. **Loguj działanie hooków** — ułatwia debugowanie
4. **Unikaj pętli** — hook wywołujący narzędzie, które wywołuje hook...

## Następny rozdział

[← Rozdział 5: Praca z projektami](05-praca-z-projektami.md) | [Rozdział 7: Multi-agent →](07-multi-agent.md)
