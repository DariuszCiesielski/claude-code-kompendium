# Rozdział 7: Wzorce multi-agent

## Czym jest multi-agent?

Multi-agent to wzorzec, w którym Claude Code deleguje zadania do osobnych agentów (subagentów). Każdy agent ma własny kontekst, specjalizację i może pracować równolegle.

## Subagenci

Subagent to osobna instancja Claude uruchomiona z konkretnym zadaniem. Główny agent (orkiestrator) deleguje i zbiera wyniki.

### Kiedy używać subagentów?

- **Zadania niezależne** — np. testowanie 3 komponentów jednocześnie
- **Różne specjalizacje** — jeden agent pisze kod, drugi robi review
- **Duże zadania** — podziel na mniejsze, niezależne części

### Wzorzec: Dispatch parallel agents

```
> Uruchom równolegle:
> 1. Agent 1: Napisz testy dla modułu auth
> 2. Agent 2: Napisz testy dla modułu payments
> 3. Agent 3: Zaktualizuj dokumentację API
```

Claude Code automatycznie uruchamia 3 subagentów i zbiera wyniki.

## Delegacja do Codex (GPT)

Claude Code może delegować proste zadania do GPT Codex (jeśli dostępny). Komunikacja przez katalog `.codex/`:

```
.codex/
├── tasks/          # Zadania do wykonania
│   ├── 001-fix-typos.md
│   └── 002-add-tests.md
├── reports/        # Raporty z wykonania
│   └── 001-fix-typos.done.md
└── archived/       # Zakończone zadania
```

### Tworzenie zadania dla Codex

```markdown
# 001-fix-typos.md

## Zadanie
Napraw literówki w plikach src/components/*.tsx

## Kontekst
- Projekt React + TypeScript
- Polskie znaki muszą być poprawne (ą,ć,ę,ł,ń,ó,ś,ź,ż)

## Kryteria akceptacji
- [ ] Brak literówek w stringach user-facing
- [ ] Build przechodzi bez błędów
- [ ] Commit z opisem "fix: popraw literówki w komponentach"
```

## AI Crew — pipeline ról

Dla złożonych zadań (4+ plików, nowa funkcjonalność) możesz uruchomić pipeline z wieloma rolami:

| Rola | Zadanie |
|------|---------|
| Designer | Makieta/wireframe UI |
| Planner | Plan implementacji |
| Architect | Decyzje architektoniczne |
| Coder | Implementacja kodu |
| Reviewer | Code review |
| Auditor | Audyt bezpieczeństwa |

### Uruchomienie AI Crew

```
crew run "Dodaj system płatności Stripe z formularzem, webhookami i panelem admina"
```

### Tryb autopilot (bez bramek zatwierdzenia)

```
crew autopilot "Zrefaktoryzuj moduł auth na wzorzec repository"
```

## Wzorce orkiestracji

### Wzorzec 1: Fan-out / Fan-in

```
Orkiestrator → [Agent A, Agent B, Agent C] → Orkiestrator zbiera wyniki
```

Użyj gdy: zadania są niezależne i mogą być wykonywane równolegle.

### Wzorzec 2: Pipeline

```
Agent A → Agent B → Agent C → Wynik
```

Użyj gdy: każdy krok zależy od wyniku poprzedniego (np. design → kod → testy).

### Wzorzec 3: Supervisor

```
Supervisor monitoruje → [Worker 1, Worker 2]
                     → Interweniuje gdy worker się blokuje
```

Użyj gdy: zadania są długie i mogą wymagać korekt w trakcie.

## Wskazówki

1. **Nie nadużywaj multi-agent** — dla prostych zadań jeden agent jest szybszy
2. **Definiuj jasne granice** — każdy agent musi wiedzieć co jest jego zakresem
3. **Sprawdzaj wyniki subagentów** — agent-orkiestrator powinien walidować
4. **Unikaj współdzielonego stanu** — agenci nie powinni edytować tych samych plików

## Następny rozdział

[← Rozdział 6: Automatyzacje](06-automatyzacje.md) | [Rozdział 8: Debugowanie →](08-debugowanie.md)
