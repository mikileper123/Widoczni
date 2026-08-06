# Widoczni

Strona-portfolio studia **Widoczni** — nowoczesne strony internetowe dla lokalnych firm.

## Struktura

```
index.html                              ← strona główna studia
realizacje/                             ← demo i portfolio (linkowane ze strony głównej)
    salon-urody-rosa/index.html         ← salon fryzjersko-kosmetyczny ROSA
    kawiarnia-ziarno/index.html         ← kawiarnia ZIARNO
klienci/                                ← produkcyjne strony klientów (patrz klienci/README.md)
```

Podział jest celowy: `realizacje/` to materiał sprzedażowy studia, `klienci/` to prawdziwe
wdrożenia, które docelowo trafiają na własne domeny. Szczegóły konwencji —
[`klienci/README.md`](klienci/README.md).

Każda strona jest samodzielna — cały CSS i JS znajduje się wewnątrz jej `index.html`,
bez zewnętrznych zależności (poza Google Fonts).

## Podgląd lokalny

Ścieżki do realizacji są katalogowe (`realizacje/salon-urody-rosa/`), więc otwarcie pliku
przez `file://` nie rozwiąże ich poprawnie. Uruchom lokalny serwer:

```bash
python3 -m http.server 8000
```

i wejdź na <http://localhost:8000>.
