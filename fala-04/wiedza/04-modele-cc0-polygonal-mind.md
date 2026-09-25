# 991 modeli CC0 Polygonal Mind — jak z nich korzystać

W fali 03 rejestr ToxSam (991 modeli) był tylko listą odnośników. W fali 04 pobrano same modele: repozytorium `ToxSam/cc0-models-Polygonal-Mind` (fork oficjalnego wydania Polygonal Mind), czyli GLB z miniaturami PNG na licencji CC0. Wszystkie 991 pozycji rejestru mają plik na dysku.

## Kolekcje

| Kolekcja | Modele | MB | Główne kategorie | Charakter | Gdzie |
|---|---:|---:|---|---|---|
| medieval-fair | 35 | 55,2 | konstrukcje, interaktywne, jedzenie | średniowieczny festyn | [GitHub](../paczki/polygonal-mind-medieval-fair.zip) |
| xyz | 60 | 7,4 | stwory | oteksturowane, zrigowane stwory | [GitHub](../paczki/polygonal-mind-xyz-stwory.zip) |
| crystal-crossroads | 64 | 21,9 | architektura, meble, technologia | pustynne ruiny z kryształami (Moebius) | [GitHub](../paczki/polygonal-mind-crystal-crossroads.zip) |
| transit | 23 | 33,4 | architektura, infrastruktura, pojazdy | retrofuturystyczna stacja | [GitHub](../paczki/polygonal-mind-transit.zip) |
| christmas | 40 | 12,9 | dekoracje, architektura | świąteczny sklep | [GitHub](../paczki/polygonal-mind-christmas.zip) |
| trash-polka | 30 | 3,0 | architektura, oświetlenie | graffiti, czerń i czerwień | [GitHub](../paczki/polygonal-mind-trash-polka.zip) |
| aero-system | 15 | 7,2 | architektura, infrastruktura | latający transport sci-fi | [GitHub](../paczki/polygonal-mind-aero-system.zip) |
| MomusPark | 72 | 54,0 | natura, teren, meble parkowe | park testowy | lokalnie |
| abm | 54 | 27,0 | architektura, natura | muzeum historii blockchain | lokalnie |
| avatar-garden | 126 | 779,2 | natura, otoczenie | krajobraz w stylu Gauguina | lokalnie |
| avatar-show | 48 | 204,6 | architektura, meble, biuro | studio wywiadów | lokalnie |
| ca-world | 68 | 134,1 | architektura, dekoracje | klasyczna rezydencja z awangardą | lokalnie |
| chromatic-chaos | 56 | 42,0 | dekoracje, technologia | vaporwave lat 80., kineskopy | lokalnie |
| cryptoavatars-retro-booth | 54 | 524,5 | architektura, szyldy | japońska ulica lat 80. | lokalnie |
| lunar-year | 52 | 39,1 | architektura, oświetlenie | Nowy Rok Księżycowy | lokalnie |
| tomb-chaser-1 | 55 | 57,5 | architektura, rekwizyty | egipska piramida, platformówka | lokalnie |
| tomb-chaser-2 | 50 | 42,9 | architektura, dekoracje | neonowe japońskie pagody | lokalnie |
| towers | 89 | 208,6 | architektura, natura, sci-fi | galeria w wieżach | lokalnie |

Kategorie i opisy pochodzą z rejestru `ToxSam/open-source-3D-assets`. Na GitHub trafiło 7 lżejszych kolekcji (ok. 138 MB w ZIP-ach). Pozostałe 11 jest w `BAZA-AI/fala-04/zrodla/ToxSam--cc0-models-Polygonal-Mind/projects/`. Lokalny, przeszukiwalny spis wszystkich modeli z kategoriami i rozmiarami: `BAZA-AI/fala-04/katalog-modeli.md`.

## Import

- **Godot 4**: GLB wrzuć do projektu. W oknie „Advanced Import Settings” włącz dla siatki generowanie fizyki (najlepiej prosty kształt kolizji zamiast siatki trójkątów) i sprawdź skalę.
- **Unity**: pakiet glTFast albo UnityGLTF. Materiały mogą wymagać przestawienia na URP/HDRP.
- **three.js / web**: `GLTFLoader`. Duże pliki (avatar-garden, cryptoavatars) kompresuj Draco/Meshopt, zanim trafią do przeglądarki.
- Miniatury `*_thumbnail.png` leżą obok modeli — przydają się w edytorze poziomów lub w wyszukiwarce bota.

## Uwagi praktyczne

1. Kolekcje powstały jako sceny do VR/metaverse (VRChat, galerie). Część obiektów ma dużo trójkątów lub duże tekstury, więc przed użyciem w grze mobilnej zrób LOD i zmniejsz tekstury.
2. Style kolekcji się różnią. Do jednej gry wybieraj jedną lub dwie sąsiednie stylistyki.
3. Stwory `xyz` projektowano pod druk 3D. Rig i animacje sprawdź przed użyciem jako przeciwników. Brakujące animacje możesz dodać przez [Mesh2Motion](03-mesh2motion.md).
4. CC0 nie wymaga atrybucji, ale warto zapisać źródło w rejestrze zasobów projektu.

[Katalog: Modele 3D](../katalog/06-modele-3d.md) · [Paczki](../paczki/README.md)
