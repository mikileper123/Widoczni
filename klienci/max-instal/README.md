# Max-Instal — Skierniewice

Instalacje HVAC: wentylacja, klimatyzacja, ogrzewanie, chłodnictwo. Firma działa od 2005 roku.
Stara strona klienta: `maxinstal.pl`.

Strona jest **produkcyjnym odtworzeniem prototypu „Max-Instal v7"** z Claude Design.
Prototyp (`.dc.html` + `support.js` + `image-slot.js`) był referencją projektową, nie kodem
do skopiowania — jego runtime nie trafił tutaj.

## Pliki

| Plik | Opis |
|---|---|
| `index.html` | Cała strona — HTML, CSS i JS w jednym pliku |
| `polityka-prywatnosci.html` | Wymagana prawnie, linkowana ze stopki |
| `robots.txt`, `sitemap.xml` | Do wgrania w root domeny |
| `assets/` | Zdjęcia i logotypy (brakuje 4 zdjęć realizacji) |

Folder jest samodzielny. Można go wgrać na hosting w całości albo przenieść do osobnego
repozytorium bez zmian w kodzie.

## Zasoby graficzne

Pliki z pakietu projektowego leżą w `assets/`. Każdy jest w dwóch wersjach: oryginał
od klienta (master, do ewentualnego ponownego przetworzenia) oraz `.webp`, który
serwuje strona.

| Serwowany plik | Wymiary | Waga | Master |
|---|---|---|---|
| `hero-digital-twin-pion.webp` | 1024×1536 | 228 KB | `.png` 2673 KB |
| `foto-maszynownia.webp` | 1400×1867 | 293 KB | `.jpg` 425 KB |
| `logo-max-instal.webp` | 660×220 | 27 KB | `.png` 2172×724 |
| `logo-max-instal-white.webp` | 660×220 | 13 KB | `.png` 2172×724 |
| `producenci-logos.webp` | 1530×85 | 13 KB | `.png` 49 KB |

Razem serwowane: **573 KB** zamiast 3,8 MB. Sama grafika hero schudła o 91%,
co przy budżecie LCP poniżej 2,5 s na wolnym łączu ma znaczenie decydujące.
Logo przyszło w 2172 px szerokości, a wyświetla się w 54 px — przeskalowane
do 660 px daje trzykrotny zapas na ekrany o wysokiej gęstości.

`logo-max-instal-white.png` nie jest obecnie używany: logotyp występuje na białej
pigułce nawigacji i na jasnej karcie kontaktowej. Zostaje na wypadek ciemnego wariantu.

### Nadal brakuje — zdjęcia realizacji

Cztery kadry w sekcji „Realizacje" czekają na materiał. Pakiet projektowy ich nie
zawierał („klient dostarczy"). Do czasu dostarczenia kadr pokazuje etykietę zamiast
ikony zepsutego obrazka, a proporcje są zablokowane, więc podmiana nie ruszy layoutu.

| Ścieżka | Obiekt | Proporcje |
|---|---|---|
| `assets/realizacja-biurowiec.jpg` | Biurowiec klasy A, Warszawa | 4:3 |
| `assets/realizacja-szpital.jpg` | Szpital, Skierniewice | 4:3 |
| `assets/realizacja-hala.jpg` | Hala produkcyjna, Łódź | 4:3 |
| `assets/realizacja-galeria.jpg` | Galeria handlowa, Warszawa | 4:3 |

Po dostarczeniu warto przepuścić je przez tę samą konwersję do WebP i zaktualizować
`width`/`height` w `index.html` — atrybuty chronią przed przeskokiem layoutu.

## Dane firmy (NAP)

Zapis musi być **identyczny co do znaku** z Wizytówką Google.

```
Max-Instal
ul. Joachima Lelewela 16, lokal nr 9
96-100 Skierniewice
tel / fax +48 46 833 60 48
kom. 512 115 071
biuro@maxinstal.pl
Pon–Pt: 8:00–16:00
NIP: 727-244-94-79
REGON: 100112240
```

Uprawnienia: `LOD/0322/OWOS/05`, `FGAZ-P/14/0049/16`, `ŁOD-N9I-LWC-9LP`.

## Czym wersja produkcyjna różni się od prototypu

1. **Responsywność w CSS, nie w JavaScripcie.** Prototyp przeliczał kolumny siatek
   w handlerze `resize` (`applyResponsive`). To dawało błysk złego układu przed wykonaniem
   skryptu, a przy wyłączonym JS strona zostawała w układzie desktopowym na telefonie.
   Tutaj robią to media queries na progach 1120 / 900 / 760 / 700 / 480 px.
2. **`<image-slot>` → `<img>`.** Runtime prototypu (`image-slot.js`, 65 KB) służył do
   wrzucania zdjęć metodą przeciągnij-i-upuść w edytorze. W produkcji jest zbędny.
3. **Style inline → arkusz klasowy.** Atrybuty `style-hover` z prototypu nie są standardem
   HTML i działały tylko pod jego runtimem; zastąpione regułami `:hover`.
4. **Reveal startuje dopiero po wykryciu JS.** Bez skryptu strona pozostaje w całości
   czytelna, zamiast zostać pustą.
5. **Etapy oferty jako `tablist`** z obsługą strzałek i `aria-selected`. Przełączanie
   najechaniem działa tylko tam, gdzie istnieje wskaźnik (`hover:hover`) — na dotyku samo
   muśnięcie nie powinno podmieniać treści.
6. **`openingHoursSpecification` w JSON-LD** — godziny biura były w prototypie tylko jako
   tekst w karcie kontaktowej.

## Czego prototyp v7 nie renderował

README prototypu opisuje animację skanu w hero, siatkę blueprint, listę warstw instalacji
i kafle HUD. W markupie te elementy mają `display:none` (`[data-layers]`, `[data-hud]`) albo
skrypt szuka węzłów, których w pliku nie ma (`[data-scanline]`, `[data-grid]`,
`[data-hudlayer]`, `[data-hudbar]`, `[data-module]`, `[data-logos]`). Odtworzone zostało to,
co prototyp faktycznie pokazywał: nagłówek, akapit, dwa CTA i grafika po prawej.

Jeśli te elementy mają wrócić, trzeba je zaprojektować od nowa — w v7 nie ma czego kopiować.

## Do decyzji

- **Brak formularza kontaktowego.** Prototyp prowadzi do telefonu i maila. Jeśli formularz
  ma być, dochodzi obowiązek klauzuli RODO i checkboxa zgody niezaznaczonego domyślnie.
- **Współrzędne geograficzne** do pola `geo` w JSON-LD — wziąć dokładne z Wizytówki Google.
- **Rok w stopce** jest wpisany na sztywno („© 2026").

## Podgląd lokalny

```bash
python3 -m http.server 8000
```
