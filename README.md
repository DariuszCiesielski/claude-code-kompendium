<div align="center">

# Kompendium Claude Code

**Najobszerniejszy polskojęzyczny przewodnik po Claude Code — od pierwszych kroków po zaawansowane wzorce multi-agentowe.**

[![12 rozdziałów](https://img.shields.io/badge/rozdziałów-12-blue?style=flat-square)](guide/)
[![69 stron PDF](https://img.shields.io/badge/PDF-69%20stron-orange?style=flat-square)](Kompendium-Claude-Code-v260410.pdf?raw=true)
[![Język: polski](https://img.shields.io/badge/język-polski-red?style=flat-square)](#)
[![Licencja: MIT](https://img.shields.io/badge/licencja-MIT-green?style=flat-square)](LICENSE)

[Pobierz PDF](Kompendium-Claude-Code-v260410.pdf?raw=true) · [Ściągawka](cheatsheet/cheatsheet.md) · [Przykłady](examples/)

</div>

---

## Dlaczego to ważne

Claude Code zmienia sposób, w jaki programiści piszą kod. Zamiast kopiować snippety z ChatGPT, dostajesz **agenta AI**, który rozumie cały Twój projekt — czyta pliki, uruchamia komendy, commituje zmiany.

- **78% programistów** używa już narzędzi AI do kodowania (ankieta GitHub 2025)
- **55% szybciej** dostarczają kod zespoły korzystające z AI assistants (badanie McKinsey 2025)
- **Claude Code** to oficjalne CLI Anthropic — działa w terminalu, nie w przeglądarce

Problem? Dokumentacja jest po angielsku, rozproszona, i zakłada, że wiesz od czego zacząć. To kompendium rozwiązuje ten problem — **12 rozdziałów po polsku**, od instalacji po orkiestrację wielu agentów.

---

## Spis treści

| # | Rozdział | Co znajdziesz |
|:-:|---------|---------------|
| 1 | [Wprowadzenie](guide/01-wprowadzenie.md) | Czym jest Claude Code, jak zainstalować, pierwsze komendy |
| 2 | [Podstawowe komendy](guide/02-podstawowe-komendy.md) | Pełna lista komend, skróty klawiszowe, nawigacja |
| 3 | [System skilli](guide/03-system-skilli.md) | Tworzenie własnych skilli — wielokrotne użycie wzorców |
| 4 | [Optymalizacja tokenów](guide/04-optymalizacja-tokenow.md) | Jak zaoszczędzić 60–90% tokenów bez utraty jakości |
| 5 | [Praca z projektami](guide/05-praca-z-projektami.md) | CLAUDE.md, system pamięci, konfiguracja projektu |
| 6 | [Automatyzacje](guide/06-automatyzacje.md) | Hooki, cron, automatyczne workflow bez interwencji |
| 7 | [Wzorce multi-agent](guide/07-multi-agent.md) | Subagenci, delegacja zadań, równoległe wykonywanie |
| 8 | [Debugowanie](guide/08-debugowanie.md) | Systematyczne strategie znajdowania i naprawiania błędów |
| 9 | [Integracje](guide/09-integracje.md) | Serwery MCP, rozszerzenia IDE, narzędzia zewnętrzne |
| 10 | [Najlepsze praktyki](guide/10-najlepsze-praktyki.md) | Kompilacja sprawdzonych wzorców z produkcyjnych projektów |
| 11 | [Frameworki multi-agent](guide/11-multi-agent-frameworks.md) | Porównanie open-multi-agent, claude-swarm, session-driver |
| 12 | [Wzorce promptów agentowych](guide/12-prompt-patterns.md) | Prefix caching, hierarchia pamięci, bezpieczeństwo |

> **Pobierz pełną wersję PDF** — [Kompendium-Claude-Code-v260410.pdf](Kompendium-Claude-Code-v260410.pdf?raw=true) (69 stron ze spisem treści, diagramami i wskazówkami)

---

## Dla kogo

### 👩‍💻 Developer
Chcesz pisać kod szybciej, ale nie wiesz jak zacząć z Claude Code. Rozdział 1–4 da Ci solidny fundament, a 6–7 pokaże jak zautomatyzować powtarzalne zadania.

### 👨‍💼 Tech Lead
Szukasz sposobu na podniesienie produktywności zespołu. Rozdziały 5, 10 i 11 pokażą Ci jak wdrożyć Claude Code w istniejący workflow — z CLAUDE.md, konwencjami i multi-agentami.

### 🚀 Founder / Solopreneur
Budujesz produkt sam lub w małym zespole. Rozdziały 3, 7 i 12 pomogą Ci zbudować system skilli i agentów, który zastąpi brakujące ręce do kodu.

---

## Szybki start

```bash
# 1. Zainstaluj Claude Code
npm install -g @anthropic-ai/claude-code

# 2. Uruchom w katalogu projektu
cd twoj-projekt && claude

# 3. Zacznij od rozdziału 1 tego kompendium
```

---

## Struktura repozytorium

```
claude-code-kompendium/
├── guide/              # 12 rozdziałów (po polsku)
├── examples/           # Przykładowe CLAUDE.md i szablony skilli
│   └── skills/         # Gotowe skille (project-setup, token-optimizer, security-audit)
├── cheatsheet/         # Ściągawka — komendy i skróty
├── CONTRIBUTING.md     # Jak współtworzyć
├── LICENSE             # MIT
└── README.md           # Ten plik
```

---

## Chcesz więcej?

To kompendium to punkt wyjścia. Jeśli chcesz gotowe narzędzia do pracy z Claude Code:

🔧 **[polish-agent-skills](https://github.com/DariuszCiesielski/polish-agent-skills)** — 15 gotowych skilli po polsku (auth, deployment, UI, optymalizacja)

🏗️ **[claude-code-saas-skills](https://github.com/DariuszCiesielski/claude-code-saas-skills)** — skille do budowania SaaS-ów (growth, analytics, Supabase, bezpieczeństwo)

📬 **[Porozmawiajmy](https://aiwbiznesie.online/kontakt/)** — wdrażasz AI w firmie? Napisz, pomożemy dobrać narzędzia.

---

## Licencja

[MIT](LICENSE) — używaj, udostępniaj i adaptuj swobodnie.

---

<div align="center">

**Zbudowane przez [AI w Biznesie](https://aiwbiznesie.online) — automatyzacja i wdrożenia AI dla polskich firm.**

</div>
