# Handoff: Studio Widoczni — strona główna

## Overview
Jednostronicowa witryna agencji Studio Widoczni (Kraków) sprzedająca projektowanie i wdrażanie stron dla lokalnych firm. Prowadzi użytkownika od problemu („większość stron nie zdobywa klientów"), przez interaktywną diagnozę i prezentację procesu współpracy, po ofertę, cennik, FAQ i formularz kontaktowy oraz darmowy „Audyt AI".

## About the Design Files
Pliki w tym pakiecie to **referencje projektowe wykonane w HTML** — prototypy pokazujące docelowy wygląd i zachowanie, a nie kod produkcyjny do skopiowania. Zadaniem jest **odtworzenie tych projektów w środowisku docelowego repozytorium** (React, Next.js, Vue, Astro, itp.) z użyciem jego wzorców, systemu stylów i bibliotek. Jeśli środowisko jeszcze nie istnieje, wybierz stack odpowiedni dla projektu (rekomendacja: Next.js + CSS Modules/Tailwind) i zaimplementuj tam.

Cały prototyp jest jednym plikiem `index.html` (HTML + CSS w `<style>` + 4 bloki vanilla JS). Nie ma zależności npm ani frameworka.

## Fidelity
**High-fidelity.** Kolory, typografia, odstępy, animacje i copy są finalne. UI należy odtworzyć wiernie (pixel-perfect), korzystając z bibliotek docelowego repo. Cała treść jest po polsku i **nie powinna być przepisywana**.

## Screens / Views
Strona to jeden dokument z sekcjami kotwiczonymi w nawigacji: `#problem`, `#realizacje`, `#proces`, `#oferta`, `#cennik`, `#faq`, `#kontakt`, `#audyt`.

### 0. Nawigacja + Hero
- Sticky top nav (wys. 70 px), tło `--bg`, hairline `--line` na dole; logo tekstowe „STUDIO WIDOCZNI", linki: Realizacje, Proces, Cennik, FAQ + CTA `.btn-primary`.
- Hero: h1 `clamp(2.6rem, 6vw, 5rem)`, Inter 600, `letter-spacing:-.04em`; jedno słowo w `Instrument Serif` italic. Pod spodem lead `--ink-2`, dwa CTA (pełny + ghost), mikro-dowód (ocena, liczba realizacji).
- Poniżej hero pasek zaufania (logotypy/rzędy tekstowe) — opcjonalny w implementacji.

### 1. `#problem` — „Dlaczego większość stron nie zdobywa klientów."
Dwie kolumny (`grid-template-columns: 1fr 1.15fr`, gap `clamp(28px,4vw,58px)`):
- **Lewa**: eyebrow mono „01 — Diagnoza", h2 `clamp(1.95rem,4.2vw,3.2rem)`, akapit, oraz karta audytu: nagłówek „Audyt strony · salon.widoczni.pl", tytuł „Co osłabia tę stronę", lista pięciu problemów pojawiających się sekwencyjnie (0,28 s + 0,48 s odstępu): Nie wiadomo, od czego zacząć / Strona ładuje się za długo / Brakuje dowodów zaufania / Niewygodnie na telefonie / Google jej nie pokazuje. Każdy wiersz: ikona ✕ w kółku `--acc`, tytuł 0,95 rem, opis 0,84 rem `--ink-3`.
- **Prawa**: makieta przeglądarki (radius 18 px, cień `--sh-lg`) z pełną stroną salonu (topbar, nav, hero, karta rezerwacji, pasek cennika, galeria, stopka) przewijającą się wolno; nad nią segmentowany przełącznik **„Przed" / „Po współpracy"** (pigułka, przesuwający się thumb, szer. thumba liczona z aktywnego przycisku). Przełączenie animuje wszystkie sekcje makiety (900 ms) i zamienia listę problemów na zielone ✔.
- Zamknięcie: „Większość stron kończy się na wyglądzie." + serif italic „My projektujemy takie, które zdobywają klientów."

### 2. `#realizacje` — „Nasze realizacje"
Siatka kart projektów (2 kolumny na desktopie, 1 na mobile), każda: gradientowy „shot" 290 px, tag mono, nazwa 2,5 rem, opis, meta z linkiem „Zobacz →" (hover: `gap` rośnie).

### 3. `#proces` — „Jak pracujemy" (kluczowa sekcja)
Scroll-driven storytelling. Struktura: `.jr-track` (wys. 520 vh) → `.jr-sticky` (`position:sticky; top:70px; height:calc(100svh - 70px)`) → `.jr-in` (grid `.92fr 1.08fr`).
- **Lewa kolumna**: bloki etapu (`.jr-st`, stackowane w gridzie 1×1, aktywny `.on`): numer + nazwa (mono, `--acc`), h3 `clamp(1.5rem,2.9vw,2.35rem)`, 1–2 akapity, karta podpowiedzi, zielony chip statusu.
- **Prawa kolumna**: MacBook — `.jr-lid` z `transform-origin:bottom`, otwiera się z `rotateX(-84deg)` → `0` (1,6 s, `cubic-bezier(.22,1,.24,1)`); ekran 16:10, radius 13 px, notch; ekran startowy (logo „W", „Widoczni", pasek ładowania) znika po wejściu w sekcję.
- **Pięć aplikacji** (`.jr-app[data-a]`, crossfade: opacity + `scale(.985)` + `blur(12px)`, 0,85 s):
  1. **Spotkanie online** — pasek „Widoczni Studio / Spotkanie projektowe / Salon Fryzjerski Nova / ● Na żywo / 00:18:42 / Zakończ spotkanie"; kafel Google Meet z awatarem „SN" i falą audio; karta „Przebieg rozmowy" z transkrypcją AI (8 wpisów ze znacznikami czasu, wchodzą co 0,5 s); karta „AI tworzy brief projektu" — pasek do 68 %, sześć wierszy z zielonymi ✓ (Cel strony, Grupa docelowa, Lokalizacja, Najważniejsze usługi jako chipy, Funkcje strony jako lista, Termin realizacji), na końcu zielony kafel „Brief gotowy". Dolny pasek sterowania rozmową z czerwonym rozłączeniem.
  2. **Projekt / Design Review** — panel „Widoczni Studio" (ciemny rail: Przegląd projektu, Brief, Projekt, Realizacja, Testy, Publikacja + stopka „WK · Wojtek, Project Manager"); lista sekcji (Hero, Usługi, Galeria, Opinie, FAQ, Kontakt) przechodzących ze spinnera na „✓ Zaakceptowane"; uwagi klienta zamieniające się w „✓ Wdrożone"; pierścień postępu 45 %.
  3. **Realizacja / Development** — paski postępu (Strona główna 100 %, O nas 80 %, Rezerwacje 70 %, Animacje 85 %, SEO 90 %), lista ostatnich zmian z ✓, pierścień 78 %.
  4. **Testy / Review** — checklista (Desktop, Tablet, Mobile, Formularze, Wydajność, SEO) ze spinnerów na ✓, podgląd gotowej strony (auto-scroll), pierścień 92 %, po ~2,2 s modal „Projekt gotowy." z przyciskami „Poproś o poprawki" / „Akceptuję projekt" → klik daje confetti + „✓ Projekt zaakceptowany".
  5. **Publikacja / Launch** — zadania wdrożenia (domena, SSL, Analytics, Search Console, publikacja) kończące się ✓, wyniki liczone od zera (127 odwiedzających, 18 rezerwacji, 4,9 ★, +43 % konwersji), toast „Nowe zapytanie z formularza", finał „🎉 Strona działa", pierścień 100 %.
- **Nawigacja**: dolny stepper (5 przycisków: numer w kółku 22 px, tytuł 0,82 rem, podpis 0,72 rem) z linią postępu; przy prawej krawędzi pionowy indeks 01–05. Klik przewija do etapu.

### 4. `#oferta` — „Co robimy"
Sticky prezentacja usług: lista wyborów po lewej (Strony internetowe, Audyt AI, Opieka, Optymalizacja), po prawej makieta urządzeń.

### 5. `#cennik` — „Jasne widełki, zero niespodzianek"
Trzy pakiety (`.tier`), środkowy wyróżniony (`--ink` tło, `--bg` tekst), flaga „Najczęściej wybierany", lista cech, CTA.

### 6. `#faq` — „Częste pytania"
Akordeon (details/summary-like), hairline między pozycjami.

### 7. `#kontakt` — „Gotowy na stronę, która naprawdę sprzedaje?"
Dwie kolumny: lewa ciemna (`--ink`) z danymi kontaktowymi, prawa formularz (imię, e-mail, telefon, wiadomość) + walidacja inline.

### 8. `#audyt` — „Sprawdź swoją stronę w minutę"
Formularz z adresem URL → symulowany przebieg audytu: lista kroków z ✓, wynik punktowy, kategorie z paskami, lista problemów i poprawek.

## Interactions & Behavior
- **Reveal on scroll**: `IntersectionObserver` (threshold 0.08, rootMargin `0px 0px -50px 0px`) dodaje `.in` do `.reveal`; przejście 0,8 s `--e-out` (opacity + translateY 20 px).
- **Sekcja proces**: handler `scroll` + `requestAnimationFrame` liczy postęp `p` w `.jr-track`; `p > 0.004` otwiera laptop; indeks sceny = `floor(((p-0.07)/0.93) * 5)`; `--prog` steruje paskiem; liczniki startują przy aktywacji sceny; modal akceptacji pokazuje się 2,2 s po wejściu w scenę 4.
- **Diagnoza (#problem)**: sekwencja startuje po wejściu w kadr; przełącznik Przed/Po animuje makietę i listę (900 ms, `--e-out`).
- **Audyt AI**: symulacja z opóźnieniami (kroki co ~700 ms, paski kategorii 1,3 s).
- **Hover**: karty podnoszą się o 6–8 px z cieniem `--sh-md`; linki „→" rozsuwają `gap` z 7 px na 12 px.
- **Responsywność**: 15 media queries. Kluczowe progi: 1180 px (dwie kolumny → jedna w diagnozie), 1080 px / wysokość 760 px (kompaktowy tryb sekcji proces: opis skrócony, laptop skalowany od wysokości, ukryty pionowy indeks), 980 px (nawigacja mobilna, siatki 1-kolumnowe), 720 px (ukryty rail aplikacji), 620 px wysokości (ukryte chipy).
- **prefers-reduced-motion**: wyłączone animacje pętlowe, otwieranie laptopa, parallax i sekwencje.

## State Management
- `activeScene` (0–4) w sekcji proces — pochodna scrolla; steruje: aktywnym ekranem, blokiem opisu, stepperem, indeksem, licznikami.
- `laptopOpen` (bool), `bootHidden` (bool).
- `approvalDone` (bool) — po kliknięciu „Akceptuję projekt".
- `compareMode` ('before' | 'after') w sekcji diagnozy.
- `auditState` ('idle' | 'running' | 'done') + wyniki (punkty, kategorie, lista poprawek) w sekcji audytu.
- `menuOpen` (bool) dla nawigacji mobilnej.
- Brak fetchowania danych — wszystkie treści są statyczne, audyt jest symulacją.

## Design Tokens
```css
/* kolory */
--bg:#faf6ef; --surface:#f4eee3; --surface-2:#ece4d6;
--ink:#1c1814; --ink-2:#544a40; --ink-3:#736758;
--line:rgba(28,24,20,.10); --line-2:rgba(28,24,20,.19);
--acc:#b0533a; --acc-2:#c26248; --acc-ink:#fdf7ee;
--gold:#b8925a; --gold-soft:rgba(184,146,90,.18);
--ok:#3f7d4f; --bad:#a32626; --focus:#b0533a;
/* cienie */
--sh-md:0 1px 2px rgba(58,40,24,.04),0 12px 28px -12px rgba(58,40,24,.16);
--sh-lg:0 2px 6px rgba(58,40,24,.05),0 38px 76px -28px rgba(58,40,24,.26);
/* easing */
--e-out:cubic-bezier(.16,1,.3,1); --e-std:cubic-bezier(.4,0,.2,1);
/* layout */
--max:1120px;  /* .wrap: max-width 1120px, padding 0 24px */
```
- **Typografia**: Inter 400/500/600 (UI), Instrument Serif italic (akcenty w nagłówkach), JetBrains Mono 400/500 (etykiety, liczby, terminal). Import: `https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Instrument+Serif:ital@1&family=JetBrains+Mono:wght@400;500&display=swap`.
- **Skala nagłówków**: h1 `clamp(2.6rem,6vw,5rem)`, h2 `clamp(1.95rem,4.2vw,3.2rem)`, h3 `clamp(1.5rem,2.9vw,2.35rem)`, body 1 rem / 1.6, mono 0,58–0,68 rem z `letter-spacing:.14–.2em`.
- **Promienie**: 999 px (pigułki), 24 px (duże karty/CTA), 18–20 px (karty, makieta przeglądarki), 12–14 px (pola, małe karty), 13 px (ekran laptopa).
- **Odstępy sekcji**: `padding: clamp(76px,10vw,150px) 0`; siatki gap `clamp(18px,3vw,32px)`.

## Assets
Brak plików graficznych — wszystkie „zdjęcia" to gradienty CSS (placeholdery). Ikony to inline SVG (stroke 1,5–2,8; `stroke-linecap/linejoin: round`). Emoji użyte celowo w dwóch miejscach („🎉", „🚀") jako element komunikatu sukcesu. Do wdrożenia produkcyjnego należy podmienić gradientowe placeholdery na realne zdjęcia salonów/realizacji (rekomendowane formaty: WebP/AVIF, lazy loading).

## Files
- `index.html` — kompletny prototyp (HTML + CSS + JS, ok. 207 kB).
Sekcje w pliku odnajdziesz po komentarzach CSS: `/* 03 — Proces: jeden projekt, jeden ekran */`, `/* ====== etap 01: spotkanie online ====== */`, `/* ====== aplikacja Widoczni Studio ====== */`, `/* ====== stepper na dole ====== */` oraz po identyfikatorach sekcji w markupie.
