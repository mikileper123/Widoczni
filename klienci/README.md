# Strony klientów

Ten folder zawiera **produkcyjne strony płacących klientów**. Każdy klient dostaje własny
podfolder z plikiem `index.html`:

```
klienci/
  nazwa-klienta/
    index.html      ← cała strona (HTML + CSS + JS w jednym pliku)
    assets/         ← zdjęcia klienta, jeśli są (opcjonalnie)
```

## Zasady

- **Nazwa folderu**: małe litery, myślniki zamiast spacji, bez polskich znaków —
  np. `piekarnia-pod-lipa`, `warsztat-mkauto`.
- **Samodzielność**: strona klienta nie może zależeć od plików spoza swojego folderu.
  Dzięki temu folder da się w każdej chwili wynieść do osobnego repo i podpiąć pod własną
  domenę bez zmian w kodzie.
- **Link zwrotny**: stopka może linkować do `https://widoczni.pl` (pełny URL, nie ścieżka
  względna) — strona klienta docelowo mieszka na innej domenie.
- **Bez linkowania z `index.html` studia**: strony klientów nie są automatycznie portfolio.
  Jeśli klient zgodzi się na publikację, zrób osobną kopię demo w `realizacje/`.

## Czym to się różni od `realizacje/`

| | `realizacje/` | `klienci/` |
|---|---|---|
| Co to jest | Demo i portfolio studia | Prawdziwe strony klientów |
| Linkowane ze strony głównej | Tak | Nie |
| Docelowa domena | `widoczni.pl/realizacje/...` | Własna domena klienta |
| Link w stopce | `../../` (do studia) | Pełny URL `https://widoczni.pl` |
