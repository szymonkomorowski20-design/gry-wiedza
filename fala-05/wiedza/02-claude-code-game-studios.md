# Claude Code Game Studios — analiza i wnioski dla game-buildera

Źródło: [`Donchitos/Claude-Code-Game-Studios`](https://github.com/Donchitos/Claude-Code-Game-Studios), commit `7ed2c3e`, licencja **MIT** (wolno kopiować i przerabiać z zachowaniem noty o prawach autorskich). Pełna kopia lokalnie: `BAZA-AI/fala-05/zrodla/Donchitos--Claude-Code-Game-Studios`.

## Czym jest

Szablon repozytorium, który zamienia sesję Claude Code w „studio”: **49 agentów** w trzech poziomach (dyrektorzy → kierownicy działów → specjaliści), **74 skille** (komendy `/start`, `/brainstorm`, `/design-system`, `/create-stories`, `/dev-story`, `/story-done`, `/gate-check`, `/playtest-report`, `/release-checklist`…), **12 hooków**, **13 reguł** przypisanych do ścieżek i **39 szablonów** dokumentów (GDD, ADR, plany sprintów, HUD, dostępność). Obsługuje Godot 4, Unity 6 i Unreal 5 (osobne zestawy agentów-specjalistów).

## Najcenniejsze ustalenia (zmierzone przez autora, nie deklaracje)

1. **Więcej dokumentów ≠ lepsza gra.** Z jednego briefu zbudowano gry przy różnych poziomach rygoru. Tryb `minimal` (1 dokument przed kodem) i `standard` (30 dokumentów, 58 minut) dały działające, przetestowane gry, ale dwóch niezależnych recenzentów i człowiek-tester ocenili wersję `standard` **najgorzej**. Dodatkowe dokumenty dały śledzalność, nie jakość. Dlatego domyślny jest `minimal`.
2. **Gra musi zostać uruchomiona i obejrzana.** Zadanie zmieniające cokolwiek widocznego dla gracza nie jest zamknięte bez uruchomienia gry w oknie i zachowanego zrzutu ekranu (`production/qa/evidence/`). „Parse check to nie uruchomienie.” Obowiązuje nawet w trybie `minimal`, gdzie testy automatyczne są zniesione.
3. **Godot bez rusztowania:** `godot --path . --windowed --resolution 1280x720 --write-movie shots/x.png --quit-after 60 res://scena.tscn` — tryb Movie Maker zapisuje klatki `x00000000.png…`, bierze się ostatnią. Nigdy `--headless` do dowodu wizualnego.
4. **Jedna linijka wyniku:** `Run result: OBSERVED — <co widać>` z ścieżką zrzutu / `NOT VERIFIED — <powód>` (blokuje zamknięcie historii wizualnej) / `N/A — <powód>` (tylko gdy naprawdę nic nie widać; „to logika” nie jest powodem).
5. **Zrzut nie pokazuje „feelu”** — czasu reakcji, animacji, synchronizacji dźwięku. To zostaje dla człowieka.
6. **`model:` w skillach nie działa** — autor zmierzył, że Claude Code ignoruje model zadeklarowany w SKILL.md i używa modelu sesji. W agentach (`.claude/agents/*.md`) to osobny mechanizm, niezmierzony.
7. **Referencje silnika z datą weryfikacji** (`docs/engine-reference/godot/`): wersja, luka wiedzy modelu, lista zmian 4.4–4.6, przestarzałe API, moduły (audio, fizyka, rendering, UI…). Ostrzeżenie w obie strony: model może nie znać nowych API, a referencja może wyprzedzać zainstalowany edytor.

## Porównanie z game-builderem

| Obszar | CCGS | game-builder (stan 0.4.x) | Wniosek |
|---|---|---|---|
| Proces | 7 faz, epiki → historie → sprinty, 3 poziomy rygoru | SPEC → HUMAN → VERIFIED → PLAYABLE → GATED, drabina zakresu | Dodać jawny przełącznik rygoru; domyślnie lekki |
| Weryfikacja | testy + obowiązkowy zrzut ekranu | `gb verify`: import, check, lint, run, GUT, scenariusze z botem, powtórki z sygnaturą stanu | game-builder jest mocniejszy w automatach; brakuje obowiązkowego **dowodu wizualnego** przy historii |
| Zrzuty | `--write-movie` (zero kodu w grze) | `gb shot` przez harness (wymaga okna) | Dodać ścieżkę `--write-movie` jako drugą metodę w `gb shot` |
| Agenci | 49 ról z hierarchią i eskalacją | brak ról (etap 6 roadmapy) | Wziąć **mało** ról: projektant, programista-Godot, QA, audio, producent; nie kopiować 49 |
| Skille | 74 | 8 | Dobrać brakujące: `playtest-report`, `bug-report/triage`, `balance-check`, `scope-check`, `asset-audit`, `release-checklist`, `changelog/patch-notes` |
| Testowanie skilli | `/skill-test` (7 kontroli statycznych, rubryki, specyfikacje zachowań), `/skill-improve` | `evals/` (8 scenariuszy, nieuruchomione) | Przejąć ideę kontroli statycznej SKILL.md + katalogu pokrycia |
| Hooki | commit/push/assety/sesja/kompaktowanie/audyt agentów | guard ścieżek, check-on-edit, session-start | Dodać `pre-compact`/`post-compact` (zachowanie stanu) i log agentów |
| Reguły | 13 reguł per ścieżka (`src/gameplay/**` → dane zamiast liczb, delta time, brak referencji do UI) | lint + AGENTS.md | Przenieść reguły do `.claude/rules` w szablonie gry |
| Referencje silnika | ręczne, z datą | lokalna dokumentacja 4.7 + przepisy z testami | Dodać plik „luka wiedzy 4.4–4.7” i sprawdzać go w `game-implement` |

## Co przejąć od razu (MIT — z notą o autorze)

1. Regułę **„Run result”** i dowód wizualny do skilla `game-implement` / `game-test` (bramka playtestu zostaje ludzka).
2. Metodę `--write-movie` do `gb shot` — działa bez harnessu i bez zmian w grze.
3. Plik referencji „co się zmieniło od wiedzy modelu” dla Godota 4.4–4.7 (baza: `docs/engine-reference/godot/*` z CCGS + dokumentacja 4.7 w BAZA-AI).
4. Lekki przełącznik rygoru w `project.yaml`/`.ai/` — domyślnie minimalny, z wyjątkami dla systemów krytycznych (u nich: zapis gry, ekonomia).
5. Katalog i statyczne kontrole skilli (frontmatter, sekcje, długość, odwołania) do `tests/release-hygiene`.

## Czego nie przejmować

- 49 agentów i trzech poziomów hierarchii — dla jednoosobowego twórcy to koszt kontekstu bez zysku (autor sam zmierzył, że cięższy proces dał gorszą grę).
- Dokumentów przed kodem ponad brief i spec.
- Deklaracji modeli w skillach (nie działają).

## Kopia i atrybucja

Fragmenty przeniesione do game-buildera muszą zachować notę: `Copyright (c) 2026 Donchitos — MIT License` (plik `LICENSE` z repozytorium źródłowego).
