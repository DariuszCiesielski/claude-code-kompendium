# Project Setup

## Opis

Skill inicjalizujący nowe projekty z kompletną strukturą folderów, plikiem CLAUDE.md, .gitignore oraz podstawową konfiguracją TypeScript i ESLint. Zapewnia spójny punkt startowy dla każdego nowego projektu, eliminując powtarzalne czynności konfiguracyjne.

## Triggery

- "nowy projekt"
- "zainicjalizuj projekt"
- "utwórz projekt"
- "project setup"
- "scaffolding projektu"

## Instrukcje

### Krok 1: Zbierz wymagania

Zapytaj użytkownika o:

1. **Nazwę projektu** (kebab-case, np. `moja-aplikacja`)
2. **Typ projektu** — wybierz jeden:
   - `nextjs` — Next.js App Router + TypeScript
   - `react-vite` — React + Vite + TypeScript
   - `node-api` — Node.js API + TypeScript
   - `library` — biblioteka npm + TypeScript
3. **Opis** — 1 zdanie do CLAUDE.md i package.json

### Krok 2: Utwórz strukturę folderów

Bazowa struktura (wspólna dla wszystkich typów):

```
nazwa-projektu/
├── src/
├── docs/
│   ├── PRODUCT.md
│   └── ARCHITECTURE.md
├── .claude/
│   └── rules/
├── CLAUDE.md
├── .gitignore
├── .claudeignore
├── package.json
├── tsconfig.json
└── README.md
```

Dodatkowe foldery zależne od typu:

**nextjs**:
```
src/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── globals.css
├── components/
├── lib/
└── types/
```

**react-vite**:
```
src/
├── components/
├── hooks/
├── lib/
├── types/
├── App.tsx
├── main.tsx
└── index.css
```

**node-api**:
```
src/
├── routes/
├── middleware/
├── services/
├── types/
└── index.ts
```

**library**:
```
src/
├── index.ts
└── lib/
```

### Krok 3: Wygeneruj CLAUDE.md

Użyj poniższego szablonu i wypełnij placeholdery:

```markdown
# {{NAZWA_PROJEKTU}}

## Opis
{{OPIS_PROJEKTU}}

## Stack technologiczny
- **Język**: TypeScript 5.x
- **Framework**: {{FRAMEWORK}}
- **Testy**: Vitest
- **Linter**: ESLint + Prettier

## Struktura projektu
- `src/` — kod źródłowy
- `docs/` — dokumentacja produktowa
- `.claude/rules/` — reguły kontekstowe

## Konwencje
- Używaj polskich znaków (ą,ć,ę,ł,ń,ó,ś,ź,ż) w tekstach widocznych dla użytkownika
- Nazwy zmiennych i funkcji w języku angielskim (camelCase)
- Komponenty React w PascalCase
- Typy i interfejsy z prefiksem (np. `UserProps`, `ApiResponse`)

## Komendy
- `npm run dev` — serwer deweloperski
- `npm run build` — build produkcyjny
- `npm run lint` — sprawdzenie kodu
- `npm run test` — uruchomienie testów
```

### Krok 4: Wygeneruj .gitignore

```gitignore
# Zależności
node_modules/

# Build
dist/
.next/
out/

# Środowisko
.env
.env.*
!.env.example

# System
.DS_Store
*.log

# IDE
.vscode/
.idea/

# Testy
coverage/
```

### Krok 5: Wygeneruj .claudeignore

```
node_modules/
dist/
.next/
out/
coverage/
*.lock
package-lock.json
pnpm-lock.yaml
```

### Krok 6: Skonfiguruj TypeScript

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### Krok 7: Skonfiguruj ESLint

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "@typescript-eslint/no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
    "@typescript-eslint/no-explicit-any": "warn",
    "no-console": ["warn", { "allow": ["warn", "error"] }]
  }
}
```

### Krok 8: Zainicjalizuj repozytorium

```bash
cd nazwa-projektu
git init
npm install
git add .
git commit -m "chore: initial project setup"
```

## Zależności

- **typescript**: ^5.x (kompilator TypeScript)
- **eslint**: ^9.x (linter kodu)
- **@typescript-eslint/parser**: ^8.x (parser TS dla ESLint)
- **@typescript-eslint/eslint-plugin**: ^8.x (reguły TS dla ESLint)
- **vitest**: ^3.x (framework testowy — opcjonalnie)

## Checklist

- [ ] Utworzono strukturę folderów zgodną z typem projektu
- [ ] Wygenerowano CLAUDE.md z opisem i konwencjami
- [ ] Utworzono .gitignore i .claudeignore
- [ ] Skonfigurowano tsconfig.json
- [ ] Skonfigurowano ESLint
- [ ] Zainicjalizowano repozytorium git
- [ ] Uruchomiono `npm install` bez błędów
- [ ] Pierwszy commit wykonany
