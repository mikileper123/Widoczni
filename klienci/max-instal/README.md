# Max-Instal — Skierniewice

Wentylacja, klimatyzacja, ogrzewanie i chłodnictwo. Firma działa od 2005 roku.
Stara strona: `maxinstal.pl` (stopka „Max-Instal 2019").

## Pliki

| Plik | Opis |
|---|---|
| `index.html` | Cała strona — HTML, CSS i JS w jednym pliku |
| `polityka-prywatnosci.html` | Wymagana prawnie, linkowana ze stopki i z formularza |
| `robots.txt` | Do wgrania w root domeny |
| `sitemap.xml` | Do wgrania w root domeny |
| `assets/` | Miejsce na zdjęcia klienta (na razie puste) |

Folder jest samodzielny — nie zależy od niczego spoza siebie. Można go wgrać na hosting
w całości albo przenieść do osobnego repozytorium bez zmian w kodzie.

## Dane firmy (NAP)

Ten zapis musi być **identyczny co do znaku** z Wizytówką Google. Jeśli w wizytówce jest
inaczej — poprawiamy tutaj, nie tam.

```
Max-Instal
ul. Joachima Lelewela 16, lokal nr 9
96-100 Skierniewice
tel / fax +48 46 833 60 48
kom. 512 115 071
biuro@maxinstal.pl
NIP: 727-244-94-79
REGON: 100112240
```

## Do uzupełnienia przed wysłaniem klientowi

Świadomie nie wymyślałem tych danych — trzeba je zebrać od klienta.

1. **Zdjęcia.** Sekcja „Realizacje" ma 6 slotów z widocznymi placeholderami. Każdy ma opis,
   jakie zdjęcie tam pasuje. Podmiana:
   ```html
   <!-- z -->
   <div class="ph"><span>Zdjęcie — ...</span></div>
   <!-- na -->
   <img src="assets/realizacja-1.webp" width="1200" height="800" loading="lazy"
        alt="Centrale wentylacyjne na dachu budynku biurowego">
   ```
   Format WebP lub AVIF, `width` i `height` obowiązkowo (przeciw CLS), proporcje 3:2.
   Placeholder trzyma `aspect-ratio:3/2`, więc podmiana nie przesunie layoutu.

2. **Godziny otwarcia.** Nie było ich na starej stronie. Po otrzymaniu — dodać jako tekst
   w sekcji kontaktu oraz `openingHoursSpecification` w JSON-LD.

3. **Współrzędne geograficzne.** Do pola `geo` w JSON-LD. Wziąć dokładne z Wizytówki Google,
   nie przybliżać.

4. **Sekcja „Uprawnienia".** Na starej stronie było to rozwijane menu, którego zawartości
   nie widziałem — prawdopodobnie skany certyfikatów. Jeśli klient chce to zachować,
   potrzebne pliki PDF lub zdjęcia dokumentów.

5. **Backend formularza.** Teraz formularz waliduje pola i otwiera klienta pocztowego
   przez `mailto:`. Działa wszędzie, ale gubi zapytania od osób bez skonfigurowanej poczty
   na telefonie — a to jest realny odsetek ruchu. Docelowo podmienić na usługę typu
   Formspree / Web3Forms: dodać `action` i `method="POST"` do `<form>`, usunąć blok
   `window.location.href = 'mailto:...'` z handlera `submit`.

6. **Logo.** Obecnie logotyp jest złożony z tekstu (`MAX-INSTAL` z pomarańczowym łącznikiem).
   Jeśli klient ma plik wektorowy — podmienić na inline SVG.

## Decyzje projektowe

- **Mobile first.** Ponad 70% ruchu lokalnej firmy usługowej to telefon. Stąd stały pasek
  akcji przy dolnej krawędzi ekranu (`Zadzwoń` / `Zamów wycenę`) — numer jest w zasięgu
  kciuka na każdej wysokości strony, bez scrollowania do stopki. Na ekranach ≤400px numer
  znika z górnego paska, żeby się nie dublował.
- **Brak cennika.** Instalacje HVAC wycenia się z projektu, nie z tabelki. Widełki wymyślone
  z sufitu szkodzą bardziej niż ich brak — CTA prowadzi do rozmowy.
- **Producenci jako lista, nie „trusted by".** To producenci urządzeń, których firma używa
  i serwisuje, a nie klienci. Sekcja jest podpisana zgodnie z tym stanem.
- **Copy przepisane, fakty zachowane.** Tekst „O nas" ze starej strony powtarzał dwa zdania
  po dwa razy. Skróciłem, nie dodając ani nie usuwając żadnego faktu.
- **Brak banera cookies.** Strona nie ładuje analityki ani pikseli. Jeśli dojdzie Google
  Analytics lub Pixel — baner staje się obowiązkowy, a skrypty nie mogą się ładować
  przed zgodą.

## Podgląd lokalny

```bash
python3 -m http.server 8000
```
