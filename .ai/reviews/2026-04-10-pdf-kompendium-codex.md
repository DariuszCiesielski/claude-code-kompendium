# Recenzja planu: „PDF Claude Code Kompendium — Orange Book Style”
Data: 2026-04-10  
Zakres: ocena podejścia do generowania PDF z treści Markdown oraz braków/ryzyk w przedstawionym planie.

## 1) Czy Markdown → HTML → PDF (Puppeteer) to najlepsze podejście?
Nie, jeśli celem jest „książkowy”, przewidywalny skład (Orange Book / podręcznik techniczny), a nie tylko „ładny PDF”.

Chromium (Puppeteer/Playwright, md-to-pdf) wygrywa szybkością prototypu i łatwością CSS, ale przegrywa tam, gdzie zaczyna się skład publikacyjny: stabilne łamanie stron, reguły typograficzne, przypisy, spisy treści z zakładkami PDF, nagłówki/stopki zależne od rozdziału, wdowy/sieroty, dzielenie wyrazów (zwłaszcza PL), kontrola nad tabelami/rysunkami i ich umieszczaniem.

Największy błąd w argumentacji planu: „brak ligatur/kerningu w HTML” — w nowoczesnych silnikach renderujących tekst ligatury i kerning działają; problemem jest raczej *paged media* i zachowanie na granicach stron, nie samo kształtowanie glifów.

**Kiedy Puppeteer ma sens**
- PDF ma wyglądać nowocześnie, „webowo”, a nie jak skład DTP.
- Treść to głównie nagłówki + listy + krótkie bloki kodu + proste grafiki.
- Akceptujesz iteracyjne „dostrajanie CSS do tego jednego dokumentu” i drobne artefakty łamania.

**Kiedy to jest zły wybór (a w Twoim planie brzmi jak wymagania)**
- Chcesz stabilnej paginacji i powtarzalnego składu na CI i na różnych maszynach.
- Chcesz przypisów, cross-referencji, numeracji rysunków/tabel, spisu treści jak w książce.
- Chcesz typografii PL (dzielenie wyrazów, interpunkcja, niełamanie w skrótach).

**Alternatywy (w kontekście Twoich celów)**
- **Pandoc + LaTeX (LuaLaTeX)**: najlepsza jakość składu, hyphenation PL, przypisy, bibliografia, spójna numeracja, stabilność. „2GB install” to chochoł: da się to zorganizować lżej (TinyTeX/Tectonic), ale nadal jest to ekosystem, który trzeba oswoić.
- **Typst**: bardzo dobry kompromis nowoczesności i składu. Minusem jest migracja (Markdown → Typst bywa „prawie”, ale w praktyce i tak kończy się poprawkami) i mniejsza dojrzałość niż LaTeX w niektórych niszach.
- **Asciidoctor PDF**: świetny, jeśli *przechodzisz na AsciiDoc* (admonitions, xrefy, atrybuty, reuse). Jeśli zostajesz przy Markdown, to narzut migracji może zabić „prostotę”.
- **Prince XML**: najbliżej „HTML/CSS jak DTP” (paged media, przypisy, running headers) — ale to narzędzie komercyjne. Jeśli budżet jest, to często jest to *najmniej bolesna* droga do książkowego PDF z HTML.
- **WeasyPrint**: lepsze „paged CSS” niż Chromium i świetne font shaping (Pango), ale bez JS. U Ciebie to oznacza konieczność *pre-renderingu* Mermaid i wszystkich dynamicznych elementów do SVG/PNG. Dla książki bywa OK, ale CSS support nie jest pełny i też ma swoje ostre krawędzie.

Wniosek: jeśli naprawdę chcesz „Orange Book” (książkowy look + przewidywalność), to **albo** idź w „HTML, ale paged-media engine” (Prince / Vivliostyle / ewentualnie WeasyPrint), **albo** w Typst/LaTeX. Chromium+Puppeteer to ryzykowny środek.

## 2) Największe ryzyka (page breaks, fonty PL, encoding)
### Łamanie stron / skład
- **Brak kontroli nad wdowami/sierotami**: CSS ma właściwości typu `widows/orphans`, ale realne wsparcie w silniku PDF z Chromium jest ograniczone i często nieskuteczne.
- **Nagłówki na dole strony**: typowy problem (H2/H3 zostaje jako ostatnia linia). `break-after/avoid` pomaga, ale potrafi generować duże „dziury”.
- **Bloki kodu**: długie linie w PDF *muszą* się łamać albo ucinać. Łamanie „gdziekolwiek” psuje czytelność i copy/paste. To jest największy praktyczny ból w dokumentacji technicznej.
- **Obrazy/diagramy**: `break-inside: avoid` potrafi „wypchnąć” całe SVG na następną stronę zostawiając pół strony pustej. Przy 8 diagramach to będzie widoczne.
- **Header/footer**: Puppeteer oferuje `headerTemplate/footerTemplate`, ale to jest osobny system niż CSS paged media. Trudno zrobić: różne nagłówki w zależności od rozdziału, parzyste/nieparzyste strony, running title itp.

### Fonty i polskie znaki
- **Brak/niepełne osadzanie fontów w PDF**: jeśli polegasz na fontach systemowych, wynik różni się między maszynami i CI. Jeśli używasz `@font-face`, musisz dopilnować, że font *naprawdę* jest użyty i osadzony (inaczej dostaniesz zamiany glifów lub „tofu” na części znaków).
- **Kursywa/pogrubienie**: w webowym świecie często lądujesz na „faux bold/italic”, jeśli nie podasz kompletnego zestawu (regular/bold/italic/bold italic). W PDF to wygląda tanio.
- **Dzielenie wyrazów po polsku**: w Chromium bywa słabe lub zerowe nawet przy `hyphens: auto` i poprawnym `lang="pl"`. Efekt: wąskie kolumny/duże odstępy albo brzydkie łamanie.

### Encoding / pipeline
- **Normalizacja znaków** (cudzysłowy, dywizy, spacje nierozdzielające): w publikacji technicznej to wychodzi natychmiast. Plan nie mówi nic o pre-processing (np. NBSP w „np.”, „r.”, „itd.”, spacje przed jednostkami, itp.).
- **Deterministyczność builda**: „Puppeteer już zainstalowany na maszynie” to anty-cecha. Jeśli nie przypniesz wersji Chromium i fontów, paginacja i łamanie wierszy będą „pływać”.

## 3) Co pominięto?
Najważniejsze luki planu (rzeczy, które zwykle wywracają takie projekty):
- **Reprodukowalność i pinning**: wersje Node, Puppeteer/Chromium, mermaid-cli, markdown-it pluginów + fonty jako zasoby repo. Bez tego każdy build to inny PDF.
- **Zakładki PDF / outline**: „spis treści HTML” to nie to samo co prawdziwe zakładki w PDF. Dla kompendium to jest kluczowe UX, a Chromium zwykle nie tworzy sensownego outline automatycznie.
- **Cross-referencje i numeracja** (rysunki/tabele/callouty/sekcje): plan mówi „trudniejsze”, ale nie proponuje mechanizmu. Bez tego „książkowość” odpada.
- **Reguły łamania kodu**: musisz zdecydować: (a) wrap zawsze, (b) zmniejszaj font, (c) ręcznie wstawiaj łamania, (d) generuj „code callouts” z łamaniem po tokenach. Bez polityki, PDF będzie pełen ucięć.
- **Długi content bez grafik → nagle „okładka + 8 diagramów + 5–8 screenshotów”**: to jest nowy, spory zakres redakcyjny. Brakuje procesu utrzymania (źródła diagramów, aktualizacja screenshotów, wykrywanie zmian w CLI output).
- **Preflight jakości**: brak automatycznych kontroli typu: brakujące glify, zbyt mały kontrast, przepełnione bloki, „puste” strony, niedziałające linki, obrazy poza marginesem.
- **Dwa profile**: PDF do druku vs PDF do ekranu (marginesy, kolory, linki, tło). „Orange Book” często zakłada druk/papier.
- **Metadane PDF**: tytuł, autor, wersja, data, licencja, language, słowa kluczowe. W publikacji technicznej to robi różnicę.

## 4) Screenshoty: Playwright vs symulowane HTML — co lepsze?
Jeśli to mają być „screenshoty terminala” w książce: oba podejścia są podejrzane, ale z różnych powodów.

**Playwright (prawdziwy rendering terminala/UI)**
- Plus: najwyższa wierność „tak to wygląda”.
- Minus: *kruchość i niedeterministyczność* (fonty, hinting, antyaliasing, różnice OS/CI, rozmiary okna, DPI). W praktyce screenshoty zaczynają „gnić” i trzeba je odświeżać częściej niż treść.

**Symulowane HTML (terminal w CSS + tekst)**
- Plus: deterministyczne, lekkie, łatwe do dopasowania do stylu książki; często można zachować selekcję tekstu (a przynajmniej copy/paste z PDF jest sensowniejszy, jeśli to nie obraz).
- Minus: to *nie jest screenshot* — jeśli czytelnik ma odtworzyć UI 1:1, możesz go wprowadzić w błąd.

Moja rekomendacja: **unikaj obrazków, gdy da się to pokazać jako tekst**. Dla kompendium CLI lepiej:
- renderować output jako blok kodu z dobrą typografią i tłem,
- a jeśli koniecznie „terminal look”: generować SVG/HTML z ANSI (deterministycznie) zamiast „fotografować” terminal.

## 5) Czy jest prostsze narzędzie dające ten sam efekt?
Jeżeli „ten sam efekt” oznacza: book-like PDF, callouty, spis treści, kontrola paged media — to **Chromium+Puppeteer nie jest najprostsze**, tylko „najbardziej znajome”.

Najprostsze ścieżki (zwykle mniej walki niż Puppeteer):
- **Vivliostyle** (HTML/CSS paged media, nastawione na publikacje): blisko Twojego mentalnego modelu (CSS), ale z naciskiem na skład książkowy.
- **Quarto/Pandoc → PDF (LaTeX/Typst)**: mniej „ręcznego CSS”, więcej gotowych mechanizmów dla przypisów, TOC, numeracji, referencji, bibliografii.
- **Prince XML** (jeśli budżet jest): najmniej „edge-case’ów” w HTML→PDF dla książek.

## Dodatkowe uwagi krytyczne do samego planu
- „Automatyczny spis treści z markdown-it-toc-done-right lub ręczny HTML” — to jest niedoszacowane: TOC w książce to nie tylko lista linków, ale też układ, hierarchia, często numery stron (których w HTML nie masz bez paginacji).
- „Okładka w HTML/CSS” — OK, ale nie padło nic o grzbiecie, spadach, formacie papieru, marginesach pod druk. Jeśli to tylko PDF do ekranu, nazwij to wprost.
- „PDF w root repo” — brak wzmianki o GitHub Releases, artefaktach CI, wersjonowaniu po tagach i o tym, czy PDF jest generowany na release (ważne dla utrzymania).

