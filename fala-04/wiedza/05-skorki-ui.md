# Skórki interfejsu (libGDX Scene2D i nie tylko)

`czyzby/gdx-skins` zbiera ok. 40 gotowych skórek GUI dla libGDX. Na GitHub trafiło [35 skórek z jawną licencją](../paczki/gdx-skins-cc.zip) (głównie CC BY 4.0, autor większości: Raymond „Raeleus” Buckley). Pominięto `default`, `extras`, `gdx-holo`, `holo` i `vis`: ich README nie podaje jednoznacznej licencji, a `vis` zawiera niepobrane pliki LFS. Wszystkie skórki są w lokalnej BAZA-AI.

## Z czego składa się skórka

| Plik | Rola |
|---|---|
| `*.atlas` + `*.png` | atlas tekstur: przyciski, suwaki, okna, ikony (często 9-patch) |
| `*.json` | style widżetów Scene2D: jakie regiony, kolory i fonty ma `TextButton`, `Window`, `ScrollPane` itd. |
| `*.fnt` + PNG | fonty bitmapowe (BMFont) |
| `raw/` | pojedyncze PNG przed spakowaniem atlasu — najwygodniejsze do przeniesienia do innego silnika |
| `README.md` | licencja, autor, informacja o fontach |

## Użycie w libGDX

```java
Skin skin = new Skin(Gdx.files.internal("arcade/skin/arcade-ui.json"));
TextButton play = new TextButton("Graj", skin);
```

Nazwy plików różnią się między skórkami, więc sprawdź folder konkretnej skórki. Skórki tworzone w Skin Composer da się dalej edytować w tym narzędziu.

## Użycie w Godot, Unity i web

Atlasów libGDX te silniki nie czytają, ale PNG z `raw/` można użyć bezpośrednio:
- **Godot**: `StyleBoxTexture` z marginesami 9-patch (patch margins) i motyw `Theme` dla `Button`, `Panel`, `LineEdit`.
- **Unity UI**: Sprite z ustawionym Border (9-slice) w Sprite Editorze, obraz typu Sliced.
- **CSS**: `border-image` z tymi samymi marginesami.

Marginesy 9-patch odczytasz z plików `.9.png` (czarne linie na krawędzi) albo dobierzesz ręcznie.

## Obowiązki licencyjne

- **CC BY 4.0** wymaga atrybucji: dodaj do napisów końcowych np. „UI skin: Arcade UI by Raymond "Raeleus" Buckley, CC BY 4.0”.
- **Fonty** mają osobne licencje (np. OFL). Pliki licencji fontów zostały w folderach skórek.
- Pełne fragmenty licencji każdej skórki: [licencje/gdx-skins-cc.txt](../licencje/gdx-skins-cc.txt).

## Dobór skórki do gry

Skórka ma pasować do gry, a nie odwrotnie. Retro i pixel art: `commodore64`, `pixthulhu`, `kenney-pixel`, `arcade`. Sci-fi: `neon`, `quantum-horizon`, `star-soldier`, `tracer`. Neutralne narzędzia i edytory: `clean-crispy`, `plain-james`, `shade`, `glassy`. Sprawdź czytelność tekstu w najmniejszej rozdzielczości i kontrast przycisku aktywnego.

[Katalog: UI](../katalog/11-ui-lokalizacja.md) · [Paczki](../paczki/README.md)
