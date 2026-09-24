# Grafika 2D, modele 3D i animacja

**Zastosowanie:** przygotowanie spójnych zasobów i ich import do gry.

## Grafika 2D

Sprite to obraz używany przez obiekt; atlas łączy wiele obrazów w jeden plik. Tileset dostarcza elementów do budowania mapy. Zanim zmieszasz paczki, porównaj wielkość kafelków, perspektywę, paletę i grubość konturu. Dla pixel art dobierz filtrowanie i skalę tak, aby zachować zamierzony wygląd pikseli.

W edytorze map oddziel wygląd kafelków od właściwości: ściana, podłoże, obrażenia lub przejście. Grafika drzewa nie musi oznaczać kolizji z całym prostokątem obrazu.

## Model 3D

Po imporcie sprawdź skalę, orientację osi, materiały i punkt obrotu. Dodaj odpowiednią kolizję. Szczegółowy model wizualny i prosty kształt kolizyjny mogą pełnić różne role. Wiele wariantów formatu w jednej paczce oznacza ten sam obiekt, a nie dodatkowe modele.

Rig jest strukturą sterowania postacią. Animacja przypisana do jednego szkieletu nie musi pasować do innego bez dopasowania. Dane mocap również wymagają sprawdzenia szkieletu, skali i warunków użycia.

**Ćwiczenie:** zbuduj jedną małą scenę z jednego tilesetu albo zestawu modeli. Dodaj postać, kolizję i trzy stany animacji: spoczynek, ruch, akcja. Sprawdź czytelność z faktycznej odległości kamery.

Materiały do wyboru: [2D](../katalog/05-grafika-2d.md), [3D](../katalog/06-modele-3d.md), [pobrane paczki](../paczki/README.md). Użyj oryginalnych plików licencji z paczek. Ilustracje referencyjne w artykule o grze nie są automatycznie assetami do ponownego użycia.
