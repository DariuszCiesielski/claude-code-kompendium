---
name: security-audit
description: Audyt bezpieczeństwa konfiguracji Claude Code w projekcie
---

## Opis
Skanuje konfigurację `.claude/`, hooks, skille i pliki projektu pod kątem wycieków sekretów, błędnych uprawnień i niebezpiecznych hooków.

## Triggery
- "audyt bezpieczeństwa"
- "sprawdź sekrety"
- "security scan"
- "czy mam wycieki"

## Instrukcje

### 1. Skanuj sekrety w konfiguracji
```bash
# Szukaj kluczy API w plikach Claude Code
grep -r "sk_\|SERVICE_ROLE\|API_KEY\|SUPABASE_\|GITHUB_TOKEN" \
  .claude/ settings.json CLAUDE.md --include="*.md" --include="*.json"
```

### 2. Sprawdź hooks
```bash
# Czy hooks nie wyciekają sekretów do stdout?
cat .claude/settings.json | jq '.hooks'
# Każdy hook z "echo" lub "cat" + zmienną env = ryzyko
```

### 3. Sprawdź .gitignore
```bash
# Czy .env jest ignorowane?
grep -q ".env" .gitignore && echo "OK" || echo "BRAK .env w .gitignore!"
# Czy credentials są ignorowane?
grep -q "credentials" .gitignore && echo "OK" || echo "BRAK credentials w .gitignore!"
```

### 4. Sprawdź uprawnienia skilli
```bash
# Czy skille mają dostęp do plików poza projektem?
grep -r "rm \|sudo \|chmod \|/etc/" ~/.claude/skills/ --include="*.md"
```

### 5. Raport
Wygeneruj raport:
```
🔒 Audyt bezpieczeństwa — [projekt]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ .gitignore zawiera .env
❌ Znaleziono API_KEY w .claude/settings.json linia 42
⚠️  Hook "pre-commit" wywołuje echo $GITHUB_TOKEN
✅ Skille nie mają dostępu poza projektem

Rekomendacje:
1. Usuń API_KEY z settings.json → przenieś do credentials vault
2. Hook pre-commit: zamień echo na zapis do pliku
```

## Zależności
- grep, jq (standardowe CLI)
- Opcjonalnie: [agentshield](https://github.com/affaan-m/agentshield) — rozszerzony scanner

## Źródło
Na podstawie researchu [agentshield](https://github.com/affaan-m/agentshield) (299★, TS, MIT).
