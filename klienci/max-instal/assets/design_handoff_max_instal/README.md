# Handoff: Max-Instal — strona firmowa (one-page)

## Overview
Strona firmowa Max-Instal (instalacje HVAC, Skierniewice, od 2005): hero z wizualizacją "X-Ray" budynku, statystyki, sekcja O firmie, Realizacje (4 karty), interaktywna Oferta (5 etapów procesu), pasek producentów, Uprawnienia oraz sekcja kontaktowa pełniąca rolę stopki.

## About the Design Files
Pliki w tym pakiecie to **referencje projektowe wykonane w HTML** — prototyp pokazujący docelowy wygląd i zachowanie, NIE kod produkcyjny do skopiowania 1:1. Zadanie: **odtworzyć ten projekt w docelowym środowisku** (Next.js/Astro/WordPress itd.) z użyciem jego konwencji. Jeśli środowisko nie istnieje, wybierz framework odpowiedni dla prostej, szybkiej strony wizytówkowej (np. Astro lub Next.js ze statycznym exportem).

Uwaga techniczna: `Max-Instal v7.dc.html` otwiera się w przeglądarce (wymaga `support.js` i `image-slot.js` obok). Markup strony znajduje się między `<x-dc>` a `</x-dc>`, logika interakcji w `<script type="text/x-dc">` na dole pliku (klasa `Component`). `<image-slot>` to placeholder na zdjęcia — w produkcji zastąp zwykłym `<img>`/`<picture>`.

## Fidelity
**High-fidelity.** Kolory, typografia, odstępy, treści i interakcje są docelowe — odtworzyć pixel-perfect.

## Screens / Views (kolejność sekcji)

### 1. Nawigacja (fixed)
- Biała pigułka (border-radius 999px), max-width 1180px, wyśrodkowana, wysokość 80px (68px po scrollu > 60px — płynna tranzycja 300ms).
- Logo po lewej (54px → 44px po scrollu). Linki: Oferta, O firmie, Realizacje, Uprawnienia, Kontakt (15px, weight 600, #2A3540, hover #1E90FF). CTA "Skontaktuj się" — niebieska pigułka z okrągłą strzałką.
- < 1120px: linki i CTA znikają, pojawia się burger + rozwijane menu (biała karta, radius 24px) z linkami i małym przyciskiem "Skontaktuj się" (46px, inline).
- < 900px: dodatkowo fixed dolny pasek (callbar): "Zadzwoń" (niebieski, biały tekst) + "Kontakt" (obrys, biały tekst) na ciemnym blur-tle; body dostaje padding-bottom 84px.

### 2. Hero `#start` (tło #07111D, min-height 100vh)
- Po prawej obraz `hero-digital-twin-pion.png` (clamp(420px,56%,980px)) z gradientowymi maskami po bokach; animowana linia "skanu" (keyframes mi7-scan, 2600ms) i siatka blueprint pojawiające się ~950ms po załadowaniu.
- Po lewej: nagłówek, akapit, dwa CTA ("Skontaktuj się" niebieski, "Zobacz realizacje" szklany z obrysem), lista warstw instalacji sterowana scrollem (aktywna warstwa: kropka w kolorze akcentu, tekst biały; obserwowana IntersectionObserverem, rootMargin -46%).
- < 900px: jedna kolumna, obraz jako przygaszone tło (opacity 0.4).

### 3. O firmie `#o-firmie` (tło #FAFBFC + siatka blueprint 56px, rgba(30,144,255,0.025))
- Pas 4 statystyk (border-left między kartami #E7EAEE): ikona 44px w kolorze #1E90FF, licznik animowany (data-count, easing cubic, 1300ms), etykiety. Hover: translateY(-6px), górna niebieska linia scaleX 0→1.
  - 21+ lat na rynku · 500+ realizacji · "Projekt • Montaż • Serwis" (separatory • w 0.55em, #1E90FF, nie łamać linii przed •) · Pełne uprawnienia.
- Niżej grid 1fr/1.05fr: tekst (eyebrow MAX-INSTAL, H2 "Kompleksowo. Profesjonalnie. Niezawodnie.", 2 akapity, CTA "Poznaj naszą ofertę") + zdjęcie `foto-maszynownia.jpg` (4/3, radius 20px, parallax 0.03).

### 4. Realizacje `#realizacje` (tło #07111D)
- Nagłówek + link "Zobacz wszystkie realizacje" (pigułka z obrysem).
- 4 karty w rzędzie (desktop repeat(4,1fr); < 1120px 2 kolumny; < 760px 1 kolumna). Karta: wysokość clamp(360px,34vw,460px), radius 28px, zdjęcie cover, gradient przyciemniający dół, tekst (kategoria DM Mono #5FB0FF — widoczna dopiero na hover, tytuł, miasto, opis) + okrągła strzałka 46px.
- Hover: zdjęcie scale 1.08 (1000ms), siatka blueprint fade-in, tekst translateY(-6px), strzałka rotate(-45deg) z niebieskim obrysem.
- Treści kart: Biurowiec klasy A / Warszawa · Szpital / Skierniewice · Hala produkcyjna / Łódź · Galeria handlowa / Warszawa.
- Pod spodem centrowane CTA "Masz podobną inwestycję?" + przycisk "Skontaktuj się".

### 5. Oferta `#oferta` (tło #F4F6F8 + siatka blueprint)
- Grid 1fr/1.15fr. Lewa: eyebrow OFERTA, H2 "Kompleksowo od projektu po serwis.", akapit; nawigacja 5 etapów (01 Projektowanie, 02 Montaż, 03 Uruchomienie, 04 Serwis, 05 Nadzór). Element: numer DM Mono, ikona w kółku 44px, nazwa. Aktywny: border-left 3px #1E90FF, ikona na tle rgba(30,144,255,0.1) w kolorze #1E90FF, nazwa większa (1.375→1.625rem) i #101519; tranzycje 400ms. Wybór: hover/click/focus.
- Prawa: karta radius 32px, tło rgba(255,255,255,0.85) + backdrop-blur 18px, cień 0 60px 120px -95px rgba(16,21,25,0.55). Zawartość (podmieniana JS): H3, opis, blok "CO ROBIMY" (3 punkty z kropką 6px #1E90FF), "CO OTRZYMUJE KLIENT" (1 zdanie, weight 600), na dole "EFEKT" — border-left 3px #1E90FF, tekst 1.125–1.375rem weight 700. Zmiana: fade + translateY(12px), 320ms, treść podmieniana po 300ms.
- Pełne teksty paneli: w pliku HTML, tablica `panes` w `setupSvcNav()`.

### 6. Pasek producentów (tło #FFFFFF, padding pion ~14–22px)
- Marquee: obraz `producenci-logos.png` ×2 (wysokość clamp(52px,5.4vw,80px)), animacja translateX 40s linear infinite **reverse** (ruch w prawo), maska fade 6% po bokach, pauza na hover.

### 7. Uprawnienia `#uprawnienia` (tło #07111D)
- Grid 1fr/1.2fr. Lewa: eyebrow UPRAWNIENIA (#5FB0FF), H2 "Pełne uprawnienia budowlane bez ograniczeń", akapit.
- Prawa: lista 3 wierszy (border-top rgba(255,255,255,0.12)); każdy wiersz to grid `minmax(0,1fr) auto` — tytuł po lewej, numer DM Mono #5FB0FF po prawej (LOD/0322/OWOS/05, FGAZ-P/14/0049/16, ŁOD-N9I-LWC-9LP).

### 8. Kontakt / stopka `#kontakt` (tło #FFFFFF, border-top #E7EAEE)
- Grid 1.15fr/1fr, duży padding (do 150px górny). Lewa: eyebrow KONTAKT, H2 "Porozmawiajmy / o Twojej inwestycji.", akapit, CTA "Skontaktuj się" (tel:), pod nim telefon 512 115 071 (weight 700, ikona słuchawki #1E90FF) i e-mail biuro@maxinstal.pl (ikona koperty).
- Prawa: karta #FAFBFC, border #E7EAEE, radius 24px, miękki cień; logo 32px; wiersze grid 110px/1fr (84px < 480px), etykiety DM Mono #1E90FF: ADRES (ul. Joachima Lelewela 16, lokal nr 9, 96-100 Skierniewice), BIURO (Pon–Pt: 8:00–16:00), NIP (727-244-94-79); przycisk "Otwórz w Google Maps" (pigułka z obrysem #DCE2E8, pełna szerokość, ikona pinezki).
- Dolny pasek (border-top #E7EAEE, DM Mono 12px #7A8593): "© 2026 Max-Instal" | "Polityka prywatności" · "Projekt i wykonanie: Studio Widoczni" (link do widoczni.pl).

## Interactions & Behavior
- Scroll-reveal: elementy [data-reveal] — opacity 0 + translateY(22px) → widoczne (720ms cubic-bezier(.22,1,.36,1)), IntersectionObserver, jednorazowo.
- Liczniki [data-count]: animacja 1300ms przy wejściu w viewport (threshold 0.6).
- Parallax [data-parallax]: translateY = offset · współczynnik · -100px, tylko ≥ 900px, wyłączony przy prefers-reduced-motion.
- Karty oferty/realizacji/statystyk: hovery opisane wyżej; karty modułów mają też tilt 3D (rotateX/Y do ~10°, tylko desktop).
- Smooth scroll (html: scroll-behavior smooth), kotwice #start/#oferta/#o-firmie/#realizacje/#uprawnienia/#kontakt.
- prefers-reduced-motion: wyłącza reveal, liczniki, parallax, skan hero.
- Tweaks (propsy DC — do odwzorowania jako motywy/konfiguracja): accent (kolor akcentu, domyślnie #1E90FF), corners (Zaokrąglone 999px / Techniczne 12px na pigułkach), motion (Pełny ruch / Wyciszony).

## State Management
- Aktywny etap oferty (int 0–4), aktywna warstwa hero (int), stan menu mobilnego (bool), stan scrolla (nav shrink), pozycje liczników. Brak fetchowania danych — wszystko statyczne.

## Design Tokens
- Kolory: granat tła #07111D i #08121F; karty ciemne #0E1B2A; biel #FFFFFF; jasne tła #FAFBFC, #F4F6F8, #F8FAFC; tekst główny #101519, wtórny #5A6470, muted #7A8593/#9AA2AB; akcent #1E90FF (hover #3FA5FF, jasne warianty #5FB0FF/#5FD0FF); pomarańcz pomocniczy #FF8A3D; linie jasne #E7EAEE/#EDF0F3, ciemne rgba(255,255,255,0.08–0.12).
- Typografia: **Manrope** (400–800; nagłówki 800, letter-spacing -0.03 do -0.04em) + **DM Mono** (etykiety uppercase, letter-spacing 0.14–0.24em, 11–13px). Google Fonts.
- Radius: pigułki 999px, karty 20–32px. Grid blueprint: 56px, rgba(30,144,255,0.025).
- Cienie: bardzo miękkie, np. 0 26px 54px -22px rgba(30,144,255,0.95) (CTA), 0 60px 120px -95px rgba(16,21,25,0.55) (karta oferty).
- Breakpointy JS: 1120px (compact), 900px (stack), 760px/700px/640px/480px (siatki drobne).

## Assets
- `logo-max-instal.png` / `logo-max-instal-white.png` — logotypy klienta.
- `producenci-logos.png` — pas logotypów producentów (jeden plik; docelowo warto zastąpić osobnymi SVG dla hoveru per logo).
- `hero-digital-twin-pion.png` — wizualizacja hero.
- `foto-maszynownia.jpg` — zdjęcie sekcji O firmie.
- Sloty na zdjęcia realizacji (4) — klient dostarczy.
- Ikony: inline SVG stroke 1.2–1.8, currentColor.

## Files
- `Max-Instal v7.dc.html` — kompletny prototyp (markup + style inline + logika interakcji na dole pliku).
- `support.js`, `image-slot.js` — runtime prototypu (tylko do podglądu, nie przenosić do produkcji).
- Grafiki wymienione w Assets.
