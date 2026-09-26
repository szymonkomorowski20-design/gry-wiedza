# Jak pominięto powtórki (fala 05)

## Adresy

Falę porównano z katalogami fal 01–04, indeksem wiki fali 02, rejestrem `linki-osobno.jsonl` z BAZA-AI, **wszystkimi adresami wymienionymi w plikach Markdown i JSON fal 01–04** oraz z pełnymi listami tematów GitHuba pobranymi w fali 04 — razem 31233 znormalizowanych adresów. Normalizacja jak w falach 03–04: HTTPS, bez `www`, bez końcowego ukośnika, małe litery hosta i nazw repozytoriów GitHuba, bez `utm_*`, `fbclid`, `gclid`, `.git` i `#readme`.

Pominięto 489 wystąpień adresów obecnych wcześniej. Kolejne 889 wystąpień w obrębie fali dopisano jako dodatkowe źródła pierwszego wpisu (kolumna „Znaleziono w”, liczba „+N”).

## Linki od użytkownika

`JimLynchCodes/Game-Sound-Effects` było w fali 04 — pominięte w całości. `Donchitos/Claude-Code-Game-Studios` był w fali 03 tylko jako wpis katalogu — dodano opracowanie i paczkę, bez powtórzenia wpisu.

## Paczki

Każdy plik w nowych ZIP-ach porównano (SHA-256) z plikami 48 paczek z `BAZA-AI/manifest-assetow.json` oraz paczek fal 03 i 04. Sześć paczek audio Kenney z soundcn (casino, digital, impact, interface, RPG, sci-fi) okazało się identycznych z paczkami fal 01 (impact, interface) i 02 (casino, digital, RPG, sci-fi) — 472 pliki — i nie zostało opublikowanych ponownie. W opublikowanych paczkach nie ma żadnego powtórzonego pliku — wynik w [raporcie kontroli](../kontrola.json).

Reguły nie wykrywają tego samego materiału pod różnymi domenami ani tego samego dźwięku w innym formacie.
