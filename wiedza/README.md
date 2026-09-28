# Wiedza przekrojowa o tworzeniu gier

Dokumenty referencyjne, które nie należą do jednej fali biblioteki. Pisane są po angielsku, bo czytają je
przede wszystkim agenci AI pracujący z pluginem [game-builder](https://github.com/szymonkomorowski20-design/game-builder).
Plugin pobiera je komendą `gb doc <nazwa>` z lokalnej kopii tego repozytorium.

| Dokument | Nazwa dla `gb doc` | O czym |
|---|---|---|
| [design-theory.md](design-theory.md) | `design-theory` | Teoria projektowania gier: MDA, pętle, decyzje, zabawa jako nauka, flow i krzywa trudności, game feel, level design, odbiorcy, playtesty. Każda idea ze źródłem i miejscem w procesie |
| [platforms.md](platforms.md) | `platforms` | Web, itch.io z butlerem i Android dla Godota 4.7, według dokumentacji gałęzi 4.7. Czego nie ma w przeglądarce, jak podpisywać Androida, co robi człowiek |
| [asset-pipeline.md](asset-pipeline.md) | `asset-pipeline` | Import grafiki i dźwięku do Godota 4.7: pixel art, audio, Blender → glTF, przyrostki nazw, edycje odporne na reimport, mapy kafelkowe, importery Aseprite/Tiled/LDtk |
| [starter-packs.md](starter-packs.md) | `starter-packs` | Paczki z tej biblioteki dobrane do szablonów gier, ze stronami autorów do rejestru licencji i znanymi lukami |
| [reference-games.md](reference-games.md) | `reference-games` | 17 otwartych gier w Godocie 4, z licencjami kodu i assetów sprawdzonymi w ich repozytoriach |
| [genre-action-roguelite.md](genre-action-roguelite.md) | `genre-action-roguelite` | Gatunek jak Hades (akcja z góry, roguelite): walka, wrogowie, różnorodność buildów, struktura runu, postęp między runami, bossowie, wprowadzenie gracza, pułapki. Zasady ze źródłami, powiązane z przepisami game-buildera 47–52 |
| [genre-military-fps.md](genre-military-fps.md) | `genre-military-fps` | Gatunek jak Call of Duty (kampania FPS): odczucie broni, AI z osłonami, zdrowie z regeneracją, poziomy i starcia („problem drzwi”), wspomaganie celowania i FOV, czytelność, pułapki. 87 faktów z 47 źródeł, powiązane z przepisami 53–57; osobna lista rzeczy, których nie udało się ustalić |

Stan: 28 września 2026. `platforms.md` i `asset-pipeline.md` sprawdził niezależny agent, porównując je z
dokumentacją Godota 4.7 i stronami itch.io, a znalezione błędy poprawiono.

## Licencje
- **Teksty w tym folderze:** CC BY 4.0 (zob. [LICENSE.md](../LICENSE.md)).
- **Fakty z dokumentacji Godota** (w `platforms.md` i `asset-pipeline.md`) są streszczone i przeformułowane.
  Źródło: © Juan Linietsky, Ariel Manzur i społeczność Godota, licencja
  [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/).
- Nazwy produktów, gier i paczek należą do ich właścicieli. Licencje gier i paczek, o których piszemy, są podane
  przy każdej pozycji i dotyczą tamtych projektów, nie tego repozytorium.
