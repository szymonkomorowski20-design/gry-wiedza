# Tematy GitHuba, bezpieczeństwo i zasoby dla bota

## Tematy — tym razem w całości

W fali 03 z tematów GitHuba wzięto tylko pierwszą stronę (20 repozytoriów). W fali 04 pobrano przez API wyszukiwania **wszystkie repozytoria** 13 tematów, łącznie 2333 wyniki. Do katalogu trafiły repozytoria z co najmniej 3 gwiazdkami, których nie było we wcześniejszych falach. Pełna lista, z opisem, licencją i datą ostatniej zmiany, jest w [zrodla/tematy-github.json](../zrodla/tematy-github.json).

| Temat | Repozytoriów na GitHubie | Najpopularniejsze (gwiazdki) |
|---|---:|---|
| sound-effects | 523 | SoLoud (silnik audio), bfxr, ZzFX, jsfx |
| sfx | 179 | Godot-GameTemplate, uisfx (dźwięki UI, MIT) |
| 3d-animation | 410 | MocapNET (mocap z kamery do BVH), Puppeteer (rig + animacja AI) |
| rigging | 250 | mGear (Maya), Duik (After Effects), GameRig |
| auto-rigging | 20 | UniRig, SkinTokens, RigAnything |
| 2d-animation | 125 | Slate (edytor pixel art), Spine Animation AI |
| 3d-model | 348 | ChatdollKit, FLAME (modele głowy) |
| 3d-assets | 78 | LUMEN-PS (tekstury ze skanera), QtMeshEditor |
| game-assets | 349 | godot-shaders (GDQuest), game-icon-pack (800+ ikon CC0) |
| game-asset | 14 | godot-visual-effects (GDQuest) |
| free-assets | 29 | 3d-resources (devanshutak25), rejestr ToxSam |
| animation-rigging | 4 | przykłady Unity (TPS, IK) |
| free-3d-models | 4 | nieliczne pojedyncze modele |

Tematy nadaje sam autor repozytorium. Temat nie jest recenzją i nie sprawdza licencji. Repozytoria z 1–2 gwiazdkami to często projekty studenckie. Wyniki zapisano wraz z datą: zmieniają się codziennie.

## Czego NIE dodano i dlaczego

Filtr pominął [11 repozytoriów](../zrodla/pominiete-podejrzane.json), m.in.:
- „darmowe pełne wersje” płatnych programów (Aseprite, Poser, Hydrogen, Rhino 3D, crack Altium) — to typowe przynęty z instalatorem zawierającym malware; część ma podejrzanie dużo gwiazdek jak na repozytorium bez kodu;
- narzędzia do masowego pobierania z Mixamo, Flaticon i Epidemic Sound (naruszają warunki tych serwisów);
- spam SEO.

Zasada dla Ciebie i dla bota: **nie uruchamiaj instalatorów `.exe` ani skryptów z przypadkowych repozytoriów**. Sprawdzaj, czy repozytorium ma kod źródłowy, historię zmian i prawdziwe zgłoszenia (issues). Wysoka liczba gwiazdek przy braku kodu jest sygnałem ostrzegawczym.

## Zasoby dla przyszłego bota do tworzenia gier

- **Skill + MCP 3dassets.dev** ([paczka](../paczki/kod-3dassets-mcp.zip), CC0): gotowy wzór skilla dla agenta. Opisuje API wyszukiwania modeli CC0 bez klucza (`/api/v1/assets?q=…&style=low-poly`), limity zapytań i zasady (zachowuj atrybucję; nie kopiuj całego katalogu; nie wypisuj kluczy API).
- **Baza devanshutak25/3d-resources** (CC0): 3533 wpisy z typem, licencją (Free/Paid/Open Source/Freemium) i datą weryfikacji linku. Po deduplikacji do katalogu weszło 2935 nowych wpisów z opisami. To najlepiej ustrukturyzowane źródło tej fali dla RAG.
- **Rejestr modeli ToxSam + pliki Polygonal Mind**: bot może filtrować modele po kategorii i rozmiarze, a potem podać ścieżkę do lokalnego GLB. Spis lokalny: `BAZA-AI/fala-04/katalog-modeli.md`.
- **Nazwy klipów animacji** (odczytane z GLB Mesh2Motion) są w [opracowaniu Mesh2Motion](03-mesh2motion.md), więc bot może dobrać animację po nazwie.
- **Spine Animation AI** pokazuje strukturę skilla (SKILL.md, szablony, skrypty); licencja pozwala tylko na użycie niekomercyjne.

Lokalna wyszukiwarka `BAZA-AI` działa teraz także w Node.js (`node dla-ai/szukaj.mjs "…"`), bez instalowania Pythona. Obejmuje dokumenty fali 04 i osobny indeks plików assetów (dźwięki, modele, animacje), dzięki któremu wyszukasz np. „explosion wav”.

[Źródła fali 04](../zrodla/README.md) · [Katalog](../katalog/README.md)
