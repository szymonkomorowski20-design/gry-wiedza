# Źródła i zakres fali 05

Stan: 26 września 2026. Zlecenie: 10 linków od właściciela biblioteki — 4 repozytoria, 5 stron tematów GitHuba (`game-audio` również w wariancie tylko GDScript, `videogame-music`, `sound-effects`, `sfx`) i wątek z Reddita — z poleceniem pogłębienia się w kolejne linki.

## Linki od użytkownika

| Link | Stan |
|---|---|
| [Donchitos/Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) | MIT. W fali 03 był tylko jako wpis w katalogu — teraz pełna analiza ([wiedza/02](../wiedza/02-claude-code-game-studios.md)) i paczka `kod-ccgs-referencje-i-reguly`; wpisu w katalogu nie powtórzono. |
| [JimLynchCodes/Game-Sound-Effects](https://github.com/JimLynchCodes/Game-Sound-Effects) | **Powtórka z fali 04** (klon i opis już są) — pominięte. |
| [Citedy/game-sounds](https://github.com/Citedy/game-sounds) | Kod MIT; 594 dźwięki wycięte z gier komercyjnych — **usunięte** z lokalnej kopii razem z historią git. Zachowany kod hooków (paczka `kod-claude-code-dzwieki-hooki`). |
| [kapishdima/soundcn](https://github.com/kapishdima/soundcn) | Kod MIT; 703 dźwięki Kenney CC0, 110 dźwięków Blizzard (All Rights Reserved) — **usunięte** lokalnie. 6 paczek Kenney to dokładne powtórki fal 01–02 (SHA-256), 3 nowe opublikowano. |
| Tematy `game-audio` (+ `?l=gdscript`), `videogame-music`, `sound-effects`, `sfx` | Pobrane w całości przez API wyszukiwania GitHuba (wariant GDScript jest podzbiorem `game-audio`). `sound-effects` i `sfx` były już w fali 04 — w katalogu tylko nowe pozycje. |
| r/gamedev: „where to find open-source music and sound effects” | **Niedostępny** — Reddit blokuje automatyczne pobieranie (przeglądarka i fetch). Zamiast tego sprawdzono ręcznie serwisy typowe dla takich wątków; nowe są w katalogu 08b ([wiedza/01](../wiedza/01-dzwieki-i-muzyka-legalnie.md)). |

## Tematy GitHuba (z pokrewnymi)

Do tematów ze zlecenia dodano pokrewne, żeby pogłębienie było pełne: `game-music`, `game-sounds`, `sound-effect`, `game-sfx`, `chiptune`, `procedural-audio`, `audio-middleware`, `fmod`, `wwise`, `sound-design`.

| Temat | Na GitHubie | Pobrano |
|---|---:|---:|
| [game-audio](https://github.com/topics/game-audio) | 162 | 162 |
| [videogame-music](https://github.com/topics/videogame-music) | 5 | 5 |
| [sound-effects](https://github.com/topics/sound-effects) | 527 | 527 |
| [sfx](https://github.com/topics/sfx) | 179 | 179 |
| [game-music](https://github.com/topics/game-music) | 31 | 31 |
| [game-sounds](https://github.com/topics/game-sounds) | 5 | 5 |
| [sound-effect](https://github.com/topics/sound-effect) | 11 | 11 |
| [game-sfx](https://github.com/topics/game-sfx) | 0 | 0 |
| [chiptune](https://github.com/topics/chiptune) | 398 | 398 |
| [procedural-audio](https://github.com/topics/procedural-audio) | 120 | 120 |
| [audio-middleware](https://github.com/topics/audio-middleware) | 3 | 3 |
| [fmod](https://github.com/topics/fmod) | 206 | 206 |
| [wwise](https://github.com/topics/wwise) | 124 | 124 |
| [sound-design](https://github.com/topics/sound-design) | 345 | 345 |

Po połączeniu: 1886 unikalnych repozytoriów, z czego nowych względem fal 01–04: 1152. Pełne listy: [tematy-github.json](tematy-github.json).

## Pogłębianie

- **Poziom 1:** README 1215 repozytoriów (66 bez README) → linki do repozytoriów GitHub i stron zewnętrznych.
- **Poziom 2:** README 819 repozytoriów znalezionych na poziomie 1 (95 bez README lub usuniętych) → do katalogu tylko linki związane z audio lub grami (6124 niezwiązanych pominięto).
- Metadane (opis, licencja, gwiazdki) z API wyszukiwania GitHuba; README z raw.githubusercontent.com (gałąź domyślna, stan z 26.09.2026).
- Pominięto 320 linków pomocniczych (plakietki, licencje, zbiórki, issues, obrazki).

## Wykluczenia

56 repozytoriów z tematów i 22 linków wykluczono: przynęty z malware udające komercyjne programy (FL Studio, Kontakt, Serum, Sylenth1, Omnisphere, Ableton, Cubase, Adobe Audition, Auto-Tune, Waves…), „keygen music” i narzędzia do masowego pobierania cudzej muzyki. [Lista z powodami](pominiete-podejrzane.json).

## Lokalna kopia (BAZA-AI)

`BAZA-AI/fala-05/zrodla`: CCGS, Citedy (bez dźwięków), soundcn (bez Blizzarda), 8bit-sfx, piano kit, game-music-composer (2,2 GB), muzyka DST (692 utwory, 3 GB), dokumentacja Godota 4.7 i GUT. `BAZA-AI/assety/fala-05/8bit-sfx-wav`: 8888 wyrenderowanych WAV. README 2034 repozytoriów: `BAZA-AI/_narzedzia/fala-05/readmes`.

## Czego nie zrobiono

Nie uruchamiano pobranego kodu (poza generatorem 8bit-sfx, żeby wyrenderować WAV), nie oceniano jakości brzmienia, nie weryfikowano ręcznie licencji wszystkich 5128 wpisów — w katalogu jest deklaracja z metadanych. Strony spoza GitHuba sprawdzono tylko dla serwisów opisanych w opracowaniach.

[Reguły pomijania powtórek](DEDUPLIKACJA.md) · [Raport kontroli](../kontrola.json)
